# Graph Workflow Builder Prompt Set

先判斷工作是否需要 Graph，再建立 Node／Edge／State 藍圖，以及 Gate、Verifier、Retry、人工批准與 Work Memory 契約。

分類：工作流、企業 AI 與自動化

## 工具原文

[開啟完整原文](../toolkits/graph-workflow.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/graph-workflow.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

準備設計多步驟 AI 工作流、檢查既有 Graph 是否過度設計，或替已確認藍圖補上控制層時。

## 前置需求

- 可建立 Markdown 檔案的 Codex、Claude Code、Cursor Agent 等 AI；每個工作流使用專屬資料夾。一般聊天工具可改為輸出完整 artifact 並自行按指定檔名保存。

## 使用方法

1. 先用 Prompt 1 提供交付物、執行頻率與失敗成本，確認是否值得建立 Graph。
2. 確認需要 Graph 後，將完整 Audit 交給 Prompt 2，建立最小 Node、Edge 與 State 藍圖。
3. 將已確認 Blueprint 交給 Prompt 3，補上驗證、重試、人工批准及可重用記憶。
4. 三份 artifact 保存在同一工作流專屬資料夾，沿用固定檔名；Audit 不通過時採用較簡單替代方案。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Task-to-Graph Suitability Audit | Prompt | 以真實依賴、控制需求、重用價值與複雜度判斷 Graph、單一 Loop、一般程式、checklist 或單一 Prompt 哪個最適合。 | [工具檔案](../toolkits/graph-workflow.md) |
| Node / Edge / State Mapper | Prompt | 把已批准的最小工作範圍轉成 Node Contract、真實 Edge、State schema 與 Mermaid 工作圖。 | [工具檔案](../toolkits/graph-workflow.md) |
| Gate / Verifier / Retry Designer | Prompt | 為重要輸出建立驗收、證據、Gate、有限局部重試、Fallback、Rollback、批准與 Work Memory 規則。 | [工具檔案](../toolkits/graph-workflow.md) |

### Task-to-Graph Suitability Audit

多步驟任務尚未決定如何編排時。

1. 貼上 Prompt 1，回答交付物、頻率、風險及缺少的流程事實。
2. 確認理解摘要，取得 01-graph-suitability-audit.md。
3. 人工確認最小 Graph 範圍後才進 Prompt 2；不需要 Graph 時停止串接。

### Node / Edge / State Mapper

Audit 已確認需要 Graph，且最小範圍取得確認時。

1. 貼上 Prompt 2 並提供完整 01-graph-suitability-audit.md。
2. 補充工具、資料、權限、輸出結構及儲存選項。
3. 確認契約與一致性檢查，保存 02-graph-blueprint.md。

### Gate / Verifier / Retry Designer

Node、Edge、State 已確認，但缺乏完整控制與恢復設計時。

1. 貼上 Prompt 3 及完整 02-graph-blueprint.md。
2. 提供失敗成本、可用證據、重試上限、停止條件與批准角色。
3. 確認控制策略與 red-team cases，保存 03-graph-control-layer.md。

## 使用重點

Prompt 1 可能建議不用 Graph；這是正常決策結果。每個工作流需獨立資料夾，避免固定檔名彼此覆蓋。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/L8WkwWDWVi2gqokkFtOc7NKQn9b)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/Dz1gw2vZHi0QAakC4KbcSVrjnQf)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
