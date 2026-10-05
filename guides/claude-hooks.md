# Claude Code Hooks：15 個情境與專屬推薦 Prompt

提供 15 支建立 Hook 的原始需求 Prompt，另用只讀 Prompt 從本機 session 找出重複提醒和固定流程，產出帶證據的 Hook 推薦清單。

分類：程式開發、審查與 Hooks

## 工具原文

[開啟完整原文](../toolkits/claude-hooks-recommender.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/claude-hooks-recommender.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

經常提醒 AI 同樣規則，想讓特定時機固定檢查，或不知道該先建立哪個 Hook 時。

## 前置需求

- Hook 推薦需 Claude Code、Codex 或 Cursor Agent 能讀本機 session。
- 依推薦 Prompt 先確認專案與時間範圍；其本身不安裝任何 Hook。
- 15 個 Hook 情境需由所在 Agent 依實際支援的事件與設定建置、測試。

## 使用方法

1. 要直接建置，從 claude-hooks-15.md 選擇對應情境，把 Prompt 全文貼給 Agent。
2. 不確定先裝哪個時，在日常專案貼入推薦 Prompt，確認產品、專案範圍與回溯天數。
3. 依實際證據選擇推薦，另複製其建置需求來建立；要求說明安裝位置、觸發與不觸發案例及卸載方式。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Hook 推薦 Prompt | Prompt | 從至少三個獨立 session 的重複行為，篩出可定位時機、縮小範圍、觀測結果與指定失敗處置的推薦。 | [工具檔案](../toolkits/claude-hooks-recommender.md) |
| 載入 STATUS.md | Prompt | 新對話、恢復或 /clear 後補回目標與待辦。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 套件管理工具檢查 | Prompt | 執行套件操作前確認 npm、pnpm 或 yarn。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 寫入前程式風格 | Prompt | 套用已有格式規範，不改程式邏輯。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 提交前敏感資料檢查 | Prompt | 擋下 .env、私鑰、憑證與疑似金鑰。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 危險指令防呆 | Prompt | 對刪除、覆蓋或清掉未存修改等難以復原指令先確認。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 保護文件 | Prompt | 對指定文件或資料夾的修改逐次確認。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 新文件位置與命名 | Prompt | 檢查新檔名及位置並調整，不動既有文件。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| Slack 事件通知 | Prompt | 指定重要事件才通知指定頻道，通知失敗不影響工作。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 子代理啟動背景 | Prompt | 依子代理種類補上必要目標、規則、決策與文件位置。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 子代理成果查驗 | Prompt | 依指定完成標準驗證交回結果，設定退回上限。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 收工格式與語法檢查 | Prompt | 一次檢查本輪修改過的程式碼。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 寫作 Skill 複查 | Prompt | 收工前用指定 Skill 檢查全文，設定重試上限。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| Prompt-based 完成度檢查 | Prompt | 由另一 AI 逐項檢查明確需求及完成證據。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 需要回應／完成通知 | Prompt | 分別使用明顯和柔和桌面通知。 | [工具檔案](../toolkits/claude-hooks-15.md) |
| 壓縮前保存決策 | Prompt | 保存已確認目標、決策、進度與禁止事項，壓縮後補回。 | [工具檔案](../toolkits/claude-hooks-15.md) |

## 附件與其他原文

- [toolkits/claude-hooks-15.md](../toolkits/claude-hooks-15.md)

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/BnjOw2RteiyhBZkeP6NcDhCCnMf)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/GWWvw1H54iELDQkzxJBcxksInBe)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
