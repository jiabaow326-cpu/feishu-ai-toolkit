# Workflow Asset Miner Prompt + AI Council Discussion Prompt

從個人工作歷史挖掘可重用流程，並以五個角度審查重要決策的兩組 Prompt。

分類：工作流、企業 AI 與自動化

## 工具原文

[開啟完整原文](../toolkits/codex-workflow-council.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/codex-workflow-council.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

重複工作累積到值得打包成資產，或在產品方向、內容角度、商業判斷與工作流改動前需要檢查假設。

## 前置需求

- Workflow Asset Miner 最適合有權限讀取本機文件、工作記憶、專案資料及既有資產的 Codex；AI Council 可在 ChatGPT、Claude、Gemini 或 Codex 使用。獨立 subagent 審查需要環境支援並依原 Prompt 取得使用者同意。

## 使用方法

1. 複製需要的完整 Prompt 到 AI 對話中，依順序回答問題。挖掘流程時提供時間範圍、來源、敏感區域及既有資產；審查決策時提供決策問題、目前傾向、證據、限制與期望結果。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Workflow Asset Miner Prompt | Prompt | 檢查近期對話、筆記、專案文件與工作記錄，找出重複、耗時、容易出錯且尚未被既有資產涵蓋的流程，產出候選清單及高信心的 Prompt、模板、Skill、agent、automation、rule、SOP 或 checklist。 | [工具檔案](../toolkits/codex-workflow-council.md) |
| AI Council Discussion Prompt | Prompt | 用反方風險、假設、機會、外部理解與執行五個角度挑戰決策，產出證據與假設區分、分歧、假設風險表、最終建議及 Output Result。 | [工具檔案](../toolkits/codex-workflow-council.md) |

## 使用重點

證據不足時只產出候選清單，不應憑空建立資產；決策涉及市場、法律、價格或政策時，原 Prompt 要求驗證來源。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/YIpgwyVr5iE7LCkXYKocuuG4nOL)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/RcALwDEXEi55H4kAOxlcWKndndg)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
