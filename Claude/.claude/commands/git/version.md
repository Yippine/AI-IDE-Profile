# /version - 版本標籤管理

建立和管理 Git 版本標籤，支援語意化版本控制和自動版本推斷。

## 使用方式

```
/version [version-number]     # 手動指定版本
/version auto                 # 自動推斷版本（基於 Story 完成狀態）
/version                      # 互動式版本選擇
```

## 自動版本推斷規則

基於 BMad Method 的 Epic/Story 進度：

- **格式**: `v0.{epic}.{story}`
- **範例**:
  - Story 1.1 完成 → `v0.1.1`
  - Story 1.2 完成 → `v0.1.2`
  - Story 2.1 完成 → `v0.2.1`

## 執行流程

1. **版本號確定**:

   - 手動指定：使用提供的版本號
   - 自動模式：分析 `core-config.yaml` 當前進度
   - 互動模式：提供選項供用戶選擇

2. **版本驗證**:

   - 檢查版本號格式（語意化版本控制）
   - 確認版本號未被使用
   - 驗證版本號遞增合理性

3. **標籤建立**:
   ```bash
   git tag -a v0.{epic}.{story} -m "Version v0.{epic}.{story}: Story {epic}.{story} Complete"
   git push origin v0.{epic}.{story}
   ```

## 標籤訊息格式

```
Version v0.{epic}.{story}: Story {epic}.{story} Complete

Epic {epic}: {Epic Name}
Story {epic}.{story}: {Story Title}

Changes in this version:
- {主要功能1}
- {主要功能2}
- {Bug 修復}

Technical Details:
- {技術實作重點}
- {重要變更說明}
```

## 版本歷史管理

- 自動讀取 `core-config.yaml` 獲取 Epic/Story 資訊
- 生成版本比較連結
- 維護版本歷史記錄

## 範例

```bash
/version auto              # 自動推斷：分析當前 Story 完成狀態
/version v0.1.1           # 手動指定：Story 1.1 完成
/version                  # 互動模式：提供選項菜單
```

## 與其他指令的關係

- **獨立使用**: 僅建立 Git Tags，不推送代碼
- **配合 /push**: 先 push 代碼，再建立版本標籤
- **配合 /release**: 建立標籤後，製作 GitHub Release
