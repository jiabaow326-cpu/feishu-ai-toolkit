# 自動化交辦包

兩個完整 Coding Agent Prompt：從 Make／n8n 匯出 JSON 判斷搬移或保留，或從新需求訪談開始，依六欄 SPEC 完成實作、測試、部署與交接。

分類：工作流、企業 AI 與自動化

## 工具原文

[開啟完整原文](../toolkits/automation-choice.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/automation-choice.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

既有視覺化流程常出錯或預計改版、需要判斷是否改由程式維護，或準備建立一項全新重複工作自動化時。

## 前置需求

- 在本機可讀寫檔案與執行程式的 Claude Code 或 Codex；為單一自動化建立空資料夾。舊流程另需完整 Make blueprint 或 n8n workflow JSON，以及可登入的相關服務帳號。

## 使用方法

1. 新建空資料夾，一項自動化一個資料夾；在其中啟動 Claude Code 或 Codex。
2. 既有 Make／n8n 流程選 Prompt 1，把完整匯出 JSON 放到本機資料夾；全新需求選 Prompt 2。
3. 把完整 Prompt 當作第一則訊息，依各階段問題確認健康報告、搬移決策或需求訪談。
4. 核對六欄 SPEC.md 後，讓 coding agent 在已授權範圍內實作並先做 dry-run 測試。
5. 按原文步驟自行處理金鑰與平台登入，確認首次執行、通知及 README；搬移流程還需依計畫新舊並跑後再停舊流程。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Blueprint 反推器 | Prompt | 分析 Make／n8n 匯出流程的健康狀況與搬留條件，反推六欄 SPEC；選擇搬移時，接續實作、測試、部署及一週新舊並跑。 | [工具檔案](../toolkits/automation-choice.md) |
| 自動化上線嚮導 | Prompt | 逐題收集新需求，建立六欄 SPEC，再引導本機建置、真實資料 dry-run、部署、首次執行與白話 README。 | [工具檔案](../toolkits/automation-choice.md) |

### Blueprint 反推器

手上有已運作的 Make／n8n 流程，想評估維護成本與遷移是否值得時。

1. 在獨立資料夾的 Claude Code／Codex 貼上 Prompt 1。
2. 提供完整匯出 JSON，回答過往故障及未來變更頻率。
3. 確認搬或留及六欄 SPEC；留在原平台時以 SPEC 交接結束。
4. 選擇搬移時完成 dry-run、已授權的首次真實執行、部署、新舊並跑與交接。

### 自動化上線嚮導

沒有現成流程但有重複任務想自動化，或已有 Prompt 1 產出的 SPEC，現在決定遷移時。

1. 在專用資料夾貼上 Prompt 2；已有 SPEC.md 時讓 agent 讀取並重新確認。
2. 說明觸發、輸入、人工步驟、理想結果及驗收方式。
3. 確認計畫與所需秘密名稱，再實作和執行 dry-run。
4. 依引導自行登入與填入平台秘密設定，確認部署、第一次執行、失敗通知與 README。

## 使用重點

完整 Prompt 是交給 coding agent 的工作規則，本次只保存原文，沒有執行其中的部署、寫檔或帳號操作。實際採用時，平台費用、介面及匯出內容仍需依當前情況核對。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/UF1jwg2Mbi2CT7kTHTtcnIe8nMd)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/SwhwwgnJci69ANkfZV2cktD6nOf)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
