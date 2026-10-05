# Opus 工作流升級套件

三支獨立 Prompt 改善意圖表達、跨模型評審與每週模型分工，輸出可重用模板、審查清單及路由表。

分類：工具選擇與模型分工

## 工具原文

[開啟完整原文](../toolkits/opus-workflow-upgrade.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/opus-workflow-upgrade.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

舊 Prompt 在新模型表現退步、高風險產出準備交付，或想重整一週 AI 工作流時。

## 前置需求

- 原文以 Opus 4.7、GPT-5.4 Pro、Gemini 3.1 Pro 為例。
- 跨模型評審需選擇與製作者不同的模型，並提供原任務與輸入素材。
- 原文模型版本與能力描述依原始工具保留，實際可用性需依帳號。

## 使用方法

1. Prompt 表現退步：跑意圖翻譯器，提供原 Prompt、受眾、失敗條件與品質範例。
2. 準備交付：用另一模型跑同行評審，提供製作者輸出、原任務與來源。
3. 規劃整週：跑模型路由器，提供工作類型、可用模型與風險。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Intent Translator（意圖翻譯器） | Prompt | 按目的、品質、對齊三層補齊缺漏，產出可貼用提示詞。 | [工具檔案](../toolkits/opus-workflow-upgrade.md) |
| Cross-Model Peer Reviewer（跨模型同行評審） | Prompt | 依完整性、指令忠實度、捏造與範圍四維評分，提出修正與人工升級決定。 | [工具檔案](../toolkits/opus-workflow-upgrade.md) |
| Model Router（模型路由器） | Prompt | 建立每類任務的製作者／評審者搭配與理由。 | [工具檔案](../toolkits/opus-workflow-upgrade.md) |

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/F5MLwbPCri91A4kUfdTcAoE3n5e)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/LEhqwr7e3ilnpXkN8rbcsux7nsd)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
