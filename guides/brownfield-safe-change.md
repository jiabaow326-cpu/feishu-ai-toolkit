# Brownfield 安全改動 Prompt Set

四個 Prompt 串起既有專案探勘、帶邊界的改動規格、Diff 初審與影響範圍回歸檢查，保留人工最後驗收。

分類：程式開發、審查與 Hooks

## 工具原文

[開啟完整原文](../toolkits/brownfield-safe-change.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/brownfield-safe-change.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

接手既有 codebase、Agent 每次重摸專案，或擔心一項改動破壞其他頁面與共用功能時。

## 前置需求

- Prompt 1 和 4 最適合能讀取整個 codebase 的 Claude Code、Cursor、Codex；網頁 AI 可依引導手動提供程式與搜尋結果。Prompt 2 和 3 可在能多輪追問的對話介面使用。

## 使用方法

1. 用 Prompt 1 從目標畫面出發探勘 codebase，核對並保存 CONTEXT_MAP.md。
2. 將 Context Map 和改動需求交給 Prompt 2，確認不可改動清單與驗收條件。
3. 將 Guardrail Spec 交給 coding agent 分塊實作；每交一塊用 Prompt 3 初審 diff。
4. 合併前用 Prompt 4 搜尋共用 symbol 的使用處，比對契約與測試，再完成按風險排序的人工檢查。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Codebase Recon & Context Map | Prompt | 只讀探勘目標區域的元件結構、資料流、共用資產使用處與專案慣例，產出可重用 Context Map。 | [工具檔案](../toolkits/brownfield-safe-change.md) |
| Guardrail Spec Generator | Prompt | 將 Context Map 與需求轉為可交辦規格，列出必讀檔案、沿用模式、重用元件、禁止區域、工作切片與驗收條件。 | [工具檔案](../toolkits/brownfield-safe-change.md) |
| Brownfield Diff Review | Prompt | 以既有專案規則初審 diff，辨識 guardrail 違反、未宣告行為變動、模式偏離、重造元件與健壯性缺口。 | [工具檔案](../toolkits/brownfield-safe-change.md) |
| Blast-Radius & Regression Check | Prompt | 逐使用處比對變更前後契約，標記 UNCHANGED／AFFECTED／UNKNOWN，對應既有測試、logging 規則與人工驗證。 | [工具檔案](../toolkits/brownfield-safe-change.md) |

### Codebase Recon & Context Map

既有專案動工前，或新 session 反覆重查同一架構時。

1. 貼上 Prompt 1，說明 agent／網頁模式、目標區域與技術棧。
2. 提供或讓 agent 讀取渲染檔案、既有規則與全部相關 symbol 使用處。
3. 核對地圖並保存 CONTEXT_MAP.md；相關架構變更後更新地圖。

### Guardrail Spec Generator

準備把既有專案的改動交給 coding agent 之前。

1. 貼上 Prompt 2，提供 Context Map、需求、紅線與分塊偏好。
2. 親自確認 Absolutely Do Not Touch 與 Acceptance Criteria。
3. 把完整最終 Guardrail Spec 作為 coding agent 的開工指令。

### Brownfield Diff Review

coding agent 每交出一小塊改動，使用者終審之前。

1. 貼上 Prompt 3，提供完整該塊 diff 及 Guardrail Spec 或 Context Map。
2. 確認改動宣稱的範圍。
3. 依 Blocker、Should-fix、Nit 閱讀證據與無法驗證部分，再進行人工終審。

### Blast-Radius & Regression Check

改動初審後、合併前，尤其涉及共用 hook、store、元件或 utility 時。

1. 貼上 Prompt 4，列出全部改動共用 symbol 與既有測試／logger 資訊。
2. 讓 agent 搜尋全部使用處，或手動執行指定搜尋並貼回結果。
3. 核對逐站判定，按報告順序跑測試、驗證頁面並重查修復後的 AFFECTED 位置。

## 使用重點

四個 Prompt 可以單獨使用。Context Map 只探勘不改 code；Diff Review 是初審，未核實使用處必須保留 UNKNOWN。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/Crr9wOW1QiUTBvk1l8dckgn8noh)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/TpB7wlDD8iDSPqk79g6c7CcTnKe)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
