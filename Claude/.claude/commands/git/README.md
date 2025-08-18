# Git 工作流程指令集總覽

MPV-GeomUX 專案的完整 Git 工作流程自動化系統，基於業界最佳實踐設計。

## 🎯 指令分層設計

### 核心指令（按使用頻率排序）

| 指令           | 用途             | 適用場景         | 自動化程度 |
| -------------- | ---------------- | ---------------- | ---------- |
| `/commit`      | WIP 暫存提交     | 日常開發進度保存 | ⭐⭐       |
| `/publish`     | **完整發佈流程** | 正式版本發佈     | ⭐⭐⭐⭐⭐ |
| `/push`        | 純代碼推送       | 功能完成但未發佈 | ⭐⭐⭐     |
| `/version`     | 版本標籤管理     | 手動版本控制     | ⭐⭐⭐⭐   |
| `/release`     | GitHub Release   | 基於現有標籤發佈 | ⭐⭐⭐⭐   |
| `/story-check` | Story 完成檢查   | 發佈前驗證       | ⭐⭐⭐     |

## 🔄 典型工作流程

### 日常開發流程

```
1. 開發功能 → /commit "Add feature X"
2. 繼續開發 → /commit "Fix issue Y"
3. 功能完成 → /story-check 1 1
4. 正式發佈 → /publish
```

### 分階段發佈流程

```
1. 推送代碼 → /push
2. 建立版本 → /version auto
3. 製作 Release → /release latest
```

### 緊急修復流程

```
1. 快速修復 → /commit "Hotfix: critical bug"
2. 立即發佈 → /publish v0.1.2
```

## 📋 業界最佳實踐整合

### ✅ 已實現的業界標準

- **Semantic Versioning**: v0.{epic}.{story} 版本命名
- **Conventional Commits**: 標準化提交訊息格式
- **Automated Changelog**: 自動生成版本變更記錄
- **GitHub Releases**: 豐富的發佈頁面和資產管理
- **Squash Merge**: 保持乾淨的提交歷史
- **Branch Protection**: 自動分支管理和清理

### 🚀 自動化功能

- **版本推斷**: 基於 BMad Method 進度自動判斷版本號
- **Release Notes**: 結構化發佈說明自動生成
- **Asset Packaging**: 可攜版和文檔自動打包上傳
- **Cross-linking**: 自動生成版本比較和文檔連結
- **Quality Gates**: 發佈前自動驗證和檢查

## 🛠️ 環境設置要求

### 必須安裝

```bash
# GitHub CLI 安裝 (WSL/Ubuntu)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh

# 或使用 Windows 內的 gh (透過 WSL 互通)
# 如果你已在 Windows 安裝 GitHub CLI
alias gh='/mnt/c/Program\ Files\ \(x86\)/GitHub\ CLI/gh.exe'

# 驗證安裝
gh --version
```

### 首次配置

```bash
# GitHub 認證
gh auth login

# 設定預設編輯器
gh config set editor "notepad"

# 驗證設定
gh repo view
```

### Git 別名設定

```bash
# 設定美化的 git log
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

## 📊 版本控制架構

### Git Tags vs GitHub Releases

```
Git Tag (v0.1.1)
    ↓
GitHub Release (v0.1.1)
    ├── Release Notes (自動生成)
    ├── Assets (自動打包)
    │   ├── MPV-GeomUX-Portable-v0.1.1.zip
    │   ├── config-examples.zip
    │   └── docs-bundle.pdf
    └── Links (自動連結)
        ├── User Story 文檔
        ├── 版本比較
        └── 完整 Changelog
```

### 版本號意義

```
v0.{epic}.{story}
  │    │      │
  │    │      └── Story 編號 (功能增量)
  │    └── Epic 編號 (大功能模組)
  └── 主版本 (專案成熟度: 0=開發中, 1=正式版)
```

## 🔗 相關文檔

- **工作流程規範**: [workflow.md](workflow.md)
- **BMad Method 整合**: [story-check.md](story-check.md)
- **專案 CLAUDE.md**: [../../CLAUDE.md](../../CLAUDE.md)
- **開發規範**: [../../docs/development-standards.md](../../docs/development-standards.md)

## 🎉 特色功能

### 智慧版本推斷

```yaml
# 讀取專案狀態
core-config.yaml:
  current:
    epic: 1
    story: 2

# 自動推斷版本
$ /version auto
→ 建議版本: v0.1.2
```

### 豐富的 Release Notes

```markdown
# Story 1.1: Rotation Control Complete

## 📋 功能概述

完整的影片旋轉控制功能...

## ✨ 新增功能

- 旋轉控制: r/Shift+r 鍵綁定
- OSD 顯示: 即時角度顯示

## 💾 下載檔案

- [可攜版 ZIP](自動打包連結)
- [配置範例](自動生成)

## 🧪 測試狀態

- [x] 15 項驗收標準全數通過
```

---

**這就是現代化的 Git 工作流程！**
**從開發到發佈，一條龍自動化！** 🚀✨
