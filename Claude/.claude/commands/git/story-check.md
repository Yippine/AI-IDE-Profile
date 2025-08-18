# /story-check - Story 完成驗證

檢查當前 Story 的完成狀態，包含驗收標準、文檔更新和測試驗證。與 BMad Method 流程兼容。

## 使用方式
```
/story-check [epic-number] [story-number]
```

## 檢查項目

### 1. 功能驗收
- [ ] 所有驗收標準是否通過
- [ ] 功能測試是否完成
- [ ] 回歸測試是否通過
- [ ] 效能要求是否達標

### 2. 文檔同步
- [ ] User Story 文檔更新狀態
- [ ] README.md 功能說明
- [ ] core-config.yaml 進度追蹤
- [ ] development-standards.md 規範更新

### 3. 代碼品質
- [ ] 符合 Lua 代碼規範
- [ ] 模組化設計檢查
- [ ] 錯誤處理完整性
- [ ] 日誌記錄充分性
- [ ] 無全域變數污染

### 4. 部署準備
- [ ] 打包腳本測試
- [ ] 可攜版配置驗證
- [ ] Windows 相容性確認
- [ ] 捷徑和啟動檔案正常

### 5. BMad Method 合規性
- [ ] core-config.yaml 狀態更新
- [ ] 任務完成標記
- [ ] 下一個 Story 準備就緒
- [ ] 品質門檻達標

## 範例
```
/story-check 1 1  # 檢查 Epic 1 Story 1 完成狀態
/story-check 1 2  # 檢查 Epic 1 Story 2 完成狀態
```

## 輸出格式
- ✅ **完成項目**: 已通過的檢查項目
- ⚠️ **待處理項目**: 需要補充的項目  
- ❌ **未完成項目**: 必須修正的問題
- 📋 **下一步建議**: 基於檢查結果的行動建議

## 與 BMad Method 整合
此檢查會自動：
- 讀取 `core-config.yaml` 當前狀態
- 驗證與 BMad Method 工作流程的一致性
- 建議下一個 Story 的準備工作
- 更新專案進度追蹤