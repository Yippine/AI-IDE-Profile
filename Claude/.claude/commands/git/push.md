# /push - 純粹代碼推送

純粹的代碼推送，不涉及版本標籤或發佈。適合工作進度同步。

## 使用方式

```
/push
```

## 執行流程

1. 切換到 main 分支並同步最新狀態
2. 執行 squash merge 將功能分支壓平
3. 分析 WIP 提交，自動草擬提交訊息
4. 建立正式提交（使用規範化格式）
5. 推送到遠端倉庫
6. 刪除本地功能分支
7. 最終驗證

## 提交訊息格式

遵循 Conventional Commits 標準：

```
[type] Subject Part 1 | Subject Part 2
```

## 適用場景

- ✅ 中間進度推送
- ✅ 功能開發完成但未準備發佈
- ✅ 團隊協作同步
- ❌ 正式版本發佈（請使用 `/release` 或 `/publish`）

## 最終驗證指令

```bash
git branch
git status
git lg -5
```

## 注意事項

- 此指令**不會**建立 Git Tags
- 此指令**不會**建立 GitHub Releases
- 僅進行代碼推送和分支清理
