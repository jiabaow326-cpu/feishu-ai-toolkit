# Token 效率自我體檢

將四層 Token 浪費框架與 Agent KISS Checklist 套用到個人使用習慣，產出診斷、對話交接摘要或 Agent 架構審查報告。

分類：Token 與 Context 效率

## 工具原文

[開啟完整原文](../toolkits/token-efficiency-self-check.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/token-efficiency-self-check.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

Token 消耗偏高、長對話逐漸失去效率，或準備整理 Agent 的 system prompt、reference 與快取架構時。

## 前置需求

- 可閱讀長文字並進行多輪問答的 Claude、ChatGPT、Gemini 等 AI；第三個 Prompt 需提供 Agent 架構或 code，最好有實際 Token 與 cache hit rate 紀錄。

## 使用方法

1. 一般使用者先複製 Prompt 1 的完整區塊到 AI 對話，依提問提供平台、對話、文件與 Plugin 使用情況。
2. 如果長對話是主要問題，使用 Prompt 2，提供完整歷史、任務及必須保留的決策；核對摘要後貼到新對話。
3. Agent 開發者可直接用 Prompt 3，提供 system prompt、架構、reference 處理方式與可取得的用量紀錄。
4. 依報告的優先項目進行修改，使用真實用量紀錄驗證改動效果。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Token 浪費模式診斷 | Prompt | 分辨 PDF 膨脹、對話歷史累積、Context Dump 與 Plugin Boot Tax 的影響，整理優先修正順序。 | [工具檔案](../toolkits/token-efficiency-self-check.md) |
| 對話瘦身術 | Prompt | 把冗長對話整理成含任務、決策、參考資料、目前狀態與未定問題的 Context Handoff。 | [工具檔案](../toolkits/token-efficiency-self-check.md) |
| Agent Context 體檢 | Prompt | 依 Index、Prepare、Cache、Scope、Measure 五項 KISS 規則檢查 Agent Context 架構，產出具體修改建議。 | [工具檔案](../toolkits/token-efficiency-self-check.md) |

### Token 浪費模式診斷

知道 Token 消耗偏高，卻不清楚浪費發生在哪一層時。

1. 貼上 Prompt 1。
2. 回答使用平台、互動頻率、對話長度、文件輸入、Plugin 與 Agent 建置情況。
3. 核對情境摘要，再採用診斷報告中的第一步行動。

### 對話瘦身術

想開新對話繼續工作，同時保留已確立的決策與限制時。

1. 貼上 Prompt 2，說明目前任務。
2. 提供完整對話歷史；太長時分段並使用 [continue] 標記。
3. 列出不可遺漏的資訊，檢查摘要後貼到新對話。

### Agent Context 體檢

API Agent 的 input tokens 偏高，或想檢查 retrieval、穩定內容快取與觀測紀錄時。

1. 貼上 Prompt 3。
2. 提供框架、system prompt、Agent loop 或架構，以及 Token、快取與 reference 處理情況。
3. 確認審查範圍，依逐條報告修改並以真實紀錄比較前後用量。

## 使用重點

原文中的模型價格、Token 倍數與節省比例是診斷範例，實際效果需依當前平台與使用紀錄核對。原文含巢狀三反引號，內容已完整保留。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/K83LwINk9iuiNWkFr7zc6mUFnOc)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/QL14wIjwBiXadikiFSvcLFu8nee)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
