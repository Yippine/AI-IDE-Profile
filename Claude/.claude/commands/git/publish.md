# /publish - 完整發佈流程

執行完整的正式發佈流程：代碼推送 → 版本標籤 → GitHub Release → 資產打包。一鍵完成所有發佈工作。

## 使用方式

```
/publish                      # 自動推斷版本並完整發佈
/publish v0.1.1              # 指定版本號完整發佈
/publish --dry-run           # 預覽模式，不實際執行
```

## 🚀 完整執行流程

### 階段 1: 代碼推送 (/push)

1. 切換到 main 分支並同步最新狀態
2. 執行 squash merge 將功能分支壓平
3. 分析 WIP 提交，自動草擬提交訊息
4. 建立正式提交（Conventional Commits 格式）
5. 推送到遠端倉庫
6. 刪除本地功能分支

### 階段 2: 版本標籤 (/version auto)

1. 自動分析 `core-config.yaml` 當前進度
2. 推斷版本號：`v0.{epic}.{story}`
3. 建立帶註解的 Git Tag
4. 推送標籤到遠端倉庫

### 階段 3: 資產打包

1. **可攜版打包**:
   ```bash
   ./tools/build_portable.sh
   ```
2. **文檔生成**: 匯出重要文檔為 PDF（如果可用）
3. **配置檔案**: 打包 config/ 目錄為範例
4. **CHANGELOG**: 自動生成版本間變更記錄

### 階段 4: GitHub Release (/release)

1. 自動生成結構化 Release Notes
2. 上傳所有打包資產
3. 建立 GitHub Release 並設為 latest
4. 生成版本比較連結

## 📝 自動生成內容

### Release Notes 範例

```markdown
# Story 1.1: Rotation Control Complete

## 📋 功能概述

實作完整的影片旋轉控制功能，支援四方向旋轉（0°/90°/180°/270°）與 OSD 顯示。

## ✨ 新增功能

- 旋轉控制: r 鍵順時針旋轉，Shift+r 逆時針旋轉
- OSD 顯示: 旋轉時顯示當前角度（如 "Rotation: 90°"）
- 重置功能: Alt+0 重置所有變換
- 滑鼠控制: 單擊暫停/播放，雙擊全螢幕

## 🐛 Bug 修復

- 修復 180 度旋轉時的「復古濾鏡」視覺問題
- 解決 Lua 模組載入路徑衝突
- 修正 Windows 批次檔中文編碼問題

## 🔧 技術改進

- 實作雙路徑模組載入機制
- 停用硬體解碼以避免渲染問題
- 建立完整的日誌與除錯系統
- 環境變數管理系統

## 💾 下載檔案

- [MPV-GeomUX-Portable-v0.1.1.zip](release-asset)
- [配置檔案範例.zip](config-examples)
- [開發規範文檔.pdf](docs-bundle)

## 🧪 測試狀態

- [x] 所有 15 項驗收標準通過
- [x] Windows 11 相容性測試
- [x] 效能測試達標
- [x] 回歸測試無問題

## 🔗 相關連結

- [User Story 1.1 完整文檔](docs/stories/epic-1/story-1.1-rotation-control.md)
- [開發規範與最佳實踐](docs/development-standards.md)
- [安裝與使用說明](README.md)
```

### Changelog 自動更新

```markdown
## [v0.1.1] - 2024-01-17

### Added

- Complete rotation control functionality
- OSD display for rotation angles
- Mouse interaction support
- Environment variable management system

### Fixed

- 180-degree rotation rendering issues
- Lua module loading path conflicts
- Windows batch file encoding problems

### Technical

- Dual-path module loading mechanism
- Hardware decoding optimization
- Comprehensive logging system
```

## 🎯 版本推斷邏輯

基於 BMad Method 進度自動推斷：

```yaml
# 讀取 core-config.yaml
current:
  epic: 1
  story: 1

# 推斷版本號
version: v0.1.1 # v0.{epic}.{story}
```

## ⚙️ 前置條件檢查

執行前自動驗證：

- [x] 所有功能已完成測試
- [x] User Story 狀態為 "completed"
- [x] core-config.yaml 已更新
- [x] 工作區乾淨無未提交變更
- [x] GitHub CLI 已配置
- [x] 打包腳本可執行

## 🔄 與其他指令的關係

```
/publish = /push + /version auto + /release latest + assets
```

**模組化使用**:

- 僅推送代碼: `/push`
- 僅建立版本: `/version`
- 僅建立 Release: `/release`
- 完整發佈: `/publish` ⭐

## 📊 執行報告

完成後提供詳細報告：

```
✅ MPV-GeomUX v0.1.1 發佈完成！

📈 發佈統計:
- Git 提交: 1 個正式提交
- Git 標籤: v0.1.1
- GitHub Release: 已建立
- 下載資產: 3 個檔案

🔗 重要連結:
- GitHub Release: https://github.com/user/MPV-GeomUX/releases/tag/v0.1.1
- 下載頁面: https://github.com/user/MPV-GeomUX/releases/latest
- 版本比較: https://github.com/user/MPV-GeomUX/compare/v0.1.0...v0.1.1

📋 下一步建議:
- 更新 core-config.yaml 準備下一個 Story
- 檢查 GitHub Release 頁面
- 分享發佈資訊給用戶
```

這就是業界標準的**完全自動化發佈流程**！🚀
