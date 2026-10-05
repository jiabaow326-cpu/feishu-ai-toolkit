# Human SOP → Agentic Workflow 拆解工具包

用五組可串接的 Prompt，把人類 SOP 拆成標準化節點，補齊隱性判斷並規劃工具接點與人工確認。

分類：工作流、企業 AI 與自動化

## 工具原文

[開啟完整原文](../toolkits/human-sop-agentic-workflow.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/human-sop-agentic-workflow.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

有大量重複流程，想交給 agent；既有 SOP 跑不穩，或流程能跑但品質總是差一點時。

## 前置需求

- Claude、ChatGPT、Gemini 等對話介面；提供真實流程、SOP、判斷案例、工具環境及人工審查需求。

## 使用方法

1. 從零依序使用 SOP Triage → Format Standardizer → Pipeline Decomposer → Tacit Knowledge Extractor → Integration & Checkpoint Planner，將前一組輸出貼入下一組。已有 SOP 可從第二組開始；品質問題可直接使用第四組。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| SOP Triage | Prompt | 從重複流程候選中挑出最值得先拆的項目，評估是否足夠清楚並指出卡點與下一步。 | [工具檔案](../toolkits/human-sop-agentic-workflow.md) |
| Format Standardizer | Prompt | 把白話流程寫成參數化 SOP，標示 MUST、SHOULD、MAY，整理步驟與錯誤處理。 | [工具檔案](../toolkits/human-sop-agentic-workflow.md) |
| Pipeline Decomposer | Prompt | 將結構化 SOP 拆成獨立節點，定義節點規格與節點間 artifact schema，找出可單獨替換的部分。 | [工具檔案](../toolkits/human-sop-agentic-workflow.md) |
| Tacit Knowledge Extractor | Prompt | 挖掘資深人員沒寫出的判斷規則，將隱性知識補進 SOP 或節點，產出補丁清單與雙向開發 checklist。 | [工具檔案](../toolkits/human-sop-agentic-workflow.md) |
| Integration & Checkpoint Planner | Prompt | 把節點連到真實工具，規劃人工確認點、觸發與排程及一週評估 rubric。 | [工具檔案](../toolkits/human-sop-agentic-workflow.md) |

## 使用重點

工具產出是流程設計與規格，接真實工具、排程與上線仍要依環境實作和驗證。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/XsnFw6XYoizBrwkCqzQcMdbYnhn)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/RsdJwH0N5iDM6xkuUX4cGO7ZnVg)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
