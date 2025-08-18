# Git 工作流程指南

MPV-GeomUX 專案的 Git 工作流程與版本控制指南，定義了標準化的 WIP 暫存和正式上版流程。

## 1. 核心工作流程概覽

AI 主要依據使用者的指令，執行兩種核心工作流程：

1.  **WIP 暫存流程**: 當使用者下達「暫存」、「commit」等指令時觸發。將當前的工作進度以 `WIP` 的形式提交到功能分支上。
2.  **正式上版流程**: 當使用者下達「上版」、「release」等指令時觸發。將功能分支上的所有 `WIP` 提交壓平成一則高品質的正式提交，合併回 `main` 分支，並清理環境。

---

## 2. WIP 暫存流程

### 步驟 1: 智慧分支判斷
當接收到暫存指令時，AI 必須首先執行以下判斷：

1.  **檢查當前分支**:
    - **若在 `main` 分支**: 自動產生功能分支名稱 (格式為 `epic-{number}-story-{number}-{feature-name}` 或 `story-{number}-{feature-name}`)，並建立該新分支。
    - **若在功能分支**: 通常直接在此分支上進行操作。若變更內容與分支名稱有顯著落差，向使用者反饋確認。

### 步驟 2: 建立 WIP 提交
1.  **加入異動**: 將當前對話中涉及的所有檔案變更加入暫存區 (`git add`)。
2.  **建立提交**: 建立一筆 `WIP` 提交。
3.  **訊息格式**: 提交訊息應為**簡潔的英文描述**，直接說明該次進度的核心內容。
    - *範例*: `git commit -m "Add rotation control module"`
    - *範例*: `git commit -m "Fix 180-degree rotation rendering issue"`
    - *範例*: `git commit -m "Update Story 1.1 documentation"`

---

## 3. 正式上版流程 - 全自動流程

### 步驟 1: 切換並更新主幹
```bash
git checkout main
git pull origin main
```

### 步驟 2: 壓平合併 (Squash Merge)
```bash
git merge --squash {feature-branch-name}
```

### 步驟 3: 正式提交
使用符合規範的訊息，將暫存區的變更提交至 `main` 分支：
```bash
git commit -m "[type] Subject"
```

### 步驟 4: 推送與清理
1.  **推送主幹**: `git push origin main`
2.  **刪除功能分支**: `git branch -D {feature-branch-name}`

### 步驟 5: 最終驗證
```bash
git branch
git status
git lg -5
```

---

## 4. 正式提交訊息規範

### 4.1 格式
`Subject Part 1 | Subject Part 2`

- **範例 (句子式)**: `Complete Story 1.1 rotation control implementation. | Add OSD display and fix rendering issues.`
- **範例 (標題式)**: `Complete Story 1.1 Rotation Control Implementation`

### 4.3 主題 (Subject) 撰寫規則
- **智慧化提煉**: AI 應分析功能分支上所有 `WIP` 提交的訊息，提煉總結出所有核心修改主題。
- **Story 導向**: 優先描述完成的 User Story 或 Epic 進度。
- **主題分隔**: 若有多個核心主題，使用 ` | ` (空格+豎線+空格) 進行分隔。
- **格式二選一 (強制)**:
    1.  **句子式 (Sentence case)**:
        - 句首單字大寫，其餘小寫。
        - **每個**由 `|` 分隔的獨立句子，**句尾都必須加上句點 `.`**。
        - *範例*: `Complete Story 1.1 rotation control implementation. | Fix 180-degree rotation rendering issue.`
    2.  **標題式 (Title Case)**:
        - 主要單字首字母大寫 (如 `of`, `a`, `the` 等助詞可小寫)。
        - 句尾**不得**加句點。
        - *範例*: Complete Story 1.1 Rotation Control Implementation

---

## 5. 版本標籤自動化

### 5.1 版本編號規則
- **格式**: `v0.{epic}.{story}`
- **範例**: 
  - Story 1.1 完成 → `v0.1.1`
  - Story 1.2 完成 → `v0.1.2`
  - Story 2.1 完成 → `v0.2.1`

### 5.2 自動標籤流程
正式上版時，AI 會自動：
1. 根據提交內容判斷完成的 Story
2. 生成對應的版本標籤
3. 推送標籤到遠端倉庫
```bash
git tag v0.{epic}.{story}
git push origin v0.{epic}.{story}
```

---

## 6. 分支命名規範

- **Epic/Story 開發**: `epic-{number}-story-{number}-{feature-name}`
- **單純功能**: `story-{number}-{feature-name}`
- **Bug 修復**: `fix-{issue-description}`
- **文檔更新**: `docs-{update-type}`

---

## 7. 指令參考

### 7.1 Git 別名設定
```bash
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

### 7.2 常用指令
- **狀態檢查**: `git status`
- **分支檢查**: `git branch --show-current`
- **日誌檢查**: `git lg -5`

---

**版本**: 1.0.0  
**建立日期**: 2024-01-17  
**適用專案**: MPV-GeomUX