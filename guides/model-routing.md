# 個人 Model Routing 工作流拆解 Prompt Set

四支 Prompt 將重複工作拆成交付鏈，分配角色、模型強度與推理強度，查開放權重候選，設計審查與停損儀表板。

分類：工具選擇與模型分工

## 工具原文

[開啟完整原文](../toolkits/model-routing.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/model-routing.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

想建立自己的模型分工表，或讓較便宜模型接手可驗收步驟時。

## 前置需求

- Codex、Claude Code、Cursor Agent 或能建立 Markdown／HTML 的工具。
- Prompt 3 必須能查官方 model card、license、Provider／Gateway 與當前可用性。
- 無法建立檔案的聊天工具會改以標示檔名的單一 code block 輸出。

## 使用方法

1. 第一次建立流程依序跑 Prompt 1 → 2 → 3 → 4。
2. 每次將上一步產生的 Markdown 交給下一步，勿重新猜測需求。
3. 最後在瀏覽器開啟 04-routing-action-dashboard.html 檢查每步驗收、停損、回退與升級規則。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Workflow Splitter | Prompt | 產出 01-workflow-brief.md，明定逐步 Input、Output、成功條件與退回位置。 | [工具檔案](../toolkits/model-routing.md) |
| Routing and Compute Planner | Prompt | 產出 02-routing-and-compute-plan.md，分配角色、模型強度及推理強度。 | [工具檔案](../toolkits/model-routing.md) |
| Open-weight Candidate Mapper | Prompt | 產出 03-open-weight-candidate-map.md，列候選、理由、可用入口及限制。 | [工具檔案](../toolkits/model-routing.md) |
| Review Gate and Action Dashboard | Prompt | 產出 04-routing-action-dashboard.html，呈現審查門檻、停損、回退與升級。 | [工具檔案](../toolkits/model-routing.md) |

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/GEdawmZu0ihQpkkK2zbcRLPGnAG)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/GraPwa4yYiEp0qkVbUfcOgAAnpc)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
