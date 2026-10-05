# AI Builder 縱軸工具包

從 workflow 拆解、五層 stack 審查、三維度評估，到是否採用 multi-agent 的四組診斷 Prompt。

分類：工作流、企業 AI 與自動化

## 工具原文

[開啟完整原文](../toolkits/ai-builder.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/ai-builder.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

想設計 agent 工作流、審查現有 prototype 或 production 的架構，補上評估方法，或判斷 multi-agent 是否必要。

## 前置需求

- 具推理能力的模型。來源建議 Claude 擴展思維、ChatGPT 推理或 Gemini 深度思考；stack 與 multi-agent 架構判斷需提供現有系統、工具與限制。

## 使用方法

1. 未上線時先跑 workflow 拆解器再跑 Eval 設計器；已有系統時先做 Stack Audit 再補 Eval。懷疑 single agent 不足時，用 Multi-Agent 決策篩判斷。可以將前一組輸出接到下一組。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| 纵轴 Workflow 拆解器 | Prompt | 把工作流拆成五至七步，標記 fuzzy 或 deterministic，推薦 LLM one-shot、RAG、Tool 或 Fine-tune，並說明工具選擇與下一步。 | [工具檔案](../toolkits/ai-builder.md) |
| 纵轴 Stack Audit | Prompt | 依 Prompt Engineering、Fine-tune、RAG、Agentic Workflow、Multi-Agent 五層審查 stack，評估耐久性與過度設計風險，給出自建、直接使用或觀望建議。 | [工具檔案](../toolkits/ai-builder.md) |
| 三维度 Eval 设计器 | Prompt | 依 component/end-to-end、objective/subjective、quantitative/qualitative 三維度建立評估矩陣，產出 LLM-as-Judge 草稿及二十筆 trace 的人工錯誤分析 checklist。 | [工具檔案](../toolkits/ai-builder.md) |
| Multi-Agent 决策筛 | Prompt | 用五個問題評估 multi-agent 的必要性，在 single agent + chain、hierarchical multi-agent、flat multi-agent 中提出建議與三個下一步。 | [工具檔案](../toolkits/ai-builder.md) |

## 使用重點

保留來源原文：最後一組標題附近原本誤標 Prompt 3，但其內容與清單對應第 4 組 Multi-Agent 決策篩。原始文件未改寫。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/Pjw2wHYibi0YbfkfxbZczVrVn6e)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/BvzTw23S2igAaUkcytscO5Vbnhh)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
