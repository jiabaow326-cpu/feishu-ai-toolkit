# Loop 工程工具包

先判斷任務適不適合做成 Loop，再建立可檢查的驗收標準與九欄位執行規格。

分類：任務定義與品質評估

## 工具原文

[開啟完整原文](../toolkits/loop-engineering.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/loop-engineering.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

有重複任務想自動化，但缺乏目標、邊界、驗收與停止條件，或完成標準十分主觀時。

## 前置需求

- 支援多輪追問的 Claude 或 ChatGPT 對話介面。生成的 Loop Spec 可交給 Claude Code、Codex、Cursor 等支援長任務的 agent 工具。

## 使用方法

1. 不確定是否適合時先使用 Loop Readiness Auditor。主觀品質任務再用 Verifier Rubric Builder 產出 rubric 或 checklist，最後交給 Loop Spec Writer 組成一頁規格。已有明確任務可直接寫 Loop Spec。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Loop Readiness Auditor | Prompt | 用十個問題檢查真實重複任務的定義缺口，判定適合或先別做，推薦 Solo Loop、Maker-Checker 或 Manager-Helper 規模。 | [工具檔案](../toolkits/loop-engineering.md) |
| Loop Spec Writer | Prompt | 將任務整理成 Goal、Trigger、Sources、Actions、Verifier、Human Boundary、Memory、Hard Stop、Fallback 九欄位 Loop Spec。 | [工具檔案](../toolkits/loop-engineering.md) |
| Verifier Rubric Builder | Prompt | 把『文章更順』『UX 更好』等抽象完成標準拆成一至五分 rubric 或 yes/no checklist，並定義收斂條件。 | [工具檔案](../toolkits/loop-engineering.md) |

## 使用重點

這三組 Prompt 產出設計與驗收規格；實際 agent 執行仍須依工具權限、人工確認與 Hard Stop 驗證。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/GDfAwxCEqiMUBEkvR2dcp9sNnTc)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/ANPDwqy3AirP6HkwQICcr8pknSd)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
