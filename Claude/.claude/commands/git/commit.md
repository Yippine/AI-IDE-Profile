# /commit - WIP 暫存提交

將當前工作進度暫存為 WIP 提交。

## 使用方式
```
/commit [optional description]
```

## 執行步驟
1. 檢查當前分支，如果在 main 分支則自動建立功能分支
2. 將變更加入暫存區 (`git add .`)
3. 建立 WIP 提交，使用英文簡潔描述
4. 確認提交成功

## 分支命名規範
- Epic/Story 開發: `epic-{number}-story-{number}-{feature-name}`
- Bug 修復: `fix-{issue-description}`
- 文檔更新: `docs-{update-type}`

## 範例
```
/commit Add rotation control functionality
/commit Fix 180-degree rendering issue
/commit Update development standards
```

## 提交訊息格式
自動生成的提交訊息格式：`{description}` (簡潔英文描述)