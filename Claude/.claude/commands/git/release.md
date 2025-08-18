# /release - GitHub Release 建立

基於現有的 Git Tag 建立正式的 GitHub Release，包含 Release Notes 和資產。

## 使用方式

```
/release [tag-name]           # 基於指定標籤建立 Release
/release latest               # 基於最新標籤建立 Release
/release                      # 互動式選擇標籤
```

## 執行流程

1. **標籤驗證**:

   - 確認指定的 Git Tag 存在
   - 檢查該 Tag 是否已有對應的 GitHub Release

2. **Release Notes 生成**:

   - 自動分析該版本的提交歷史
   - 基於 core-config.yaml 獲取 Epic/Story 資訊
   - 生成結構化的 Release Notes

3. **GitHub Release 建立**:
   ```bash
   gh release create {tag-name} \
     --title "Story {epic}.{story}: {Story Title}" \
     --notes-file release-notes.md \
     --latest
   ```

## Release Notes 自動生成格式

```markdown
# Story {epic}.{story}: {Story Title}

## 📋 功能概述

{從 User Story 自動提取的功能描述}

## ✨ 新增功能

- {功能 1}: {描述}
- {功能 2}: {描述}

## 🐛 Bug 修復

- {修復 1}: {描述}
- {修復 2}: {描述}

## 🔧 技術改進

- {改進 1}: {描述}
- {改進 2}: {描述}

## 📚 文檔更新

- {更新 1}: {描述}

## 🧪 測試狀態

- [x] 功能測試通過
- [x] 回歸測試通過
- [x] 效能測試達標

## 💾 下載檔案

- [MPV-GeomUX-Portable-v{version}.zip](下載連結)
- [Source Code (zip)](GitHub自動生成)
- [Source Code (tar.gz)](GitHub自動生成)

## 🔗 相關連結

- [User Story {epic}.{story}](連結到文檔)
- [完整變更日誌](比較連結)
- [安裝說明](README.md)

---

**完整提交歷史**: [查看所有變更](GitHub比較連結)
```

## 資產文件自動化

自動打包和上傳：

1. **可攜版 ZIP**: 
   ```bash
   # 執行現有打包腳本
   ./tools/build_portable.sh
   # 生成: MPV-GeomUX-Portable-v{version}.zip
   ```

2. **配置範例包**:
   ```bash
   # 打包 config/ 目錄
   zip -r "MPV-GeomUX-Config-Examples-v{version}.zip" config/
   ```

3. **文檔包** (可選):
   ```bash
   # 打包重要文檔
   zip -r "MPV-GeomUX-Documentation-v{version}.zip" \
     README.md \
     docs/stories/**/*.md \
     docs/development-standards.md \
     CLAUDE.md
   ```

4. **自動上傳到 GitHub Release**:
   ```bash
   gh release upload v{version} \
     MPV-GeomUX-Portable-v{version}.zip \
     MPV-GeomUX-Config-Examples-v{version}.zip \
     MPV-GeomUX-Documentation-v{version}.zip
   ```

## 前置條件

- 指定的 Git Tag 必須存在
- 已安裝並配置 GitHub CLI (`gh`)
- 具備倉庫的 Release 權限

## 與其他指令的關係

- **需要先執行**: `/push` 和 `/version`
- **完整流程**: 建議使用 `/publish` 指令
- **獨立使用**: 僅建立 GitHub Release，不影響代碼
