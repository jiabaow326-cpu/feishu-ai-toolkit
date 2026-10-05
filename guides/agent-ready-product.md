# 2C 產品代理入口診斷提示集

把產品頁面流程拆成 agent 任務，找出值得 AI 化的情境，檢查服務資料與底層狀態、權限和責任。

分類：工作流、企業 AI 與自動化

## 工具原文

[開啟完整原文](../toolkits/agent-ready-product.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/agent-ready-product.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

已有 App、小程式、網站、SaaS、電商或服務，準備增加 AI agent 入口，或正在接 API、MCP、Skill 前。

## 前置需求

- Claude、ChatGPT、Gemini 或 Codex。提供產品文件、API 文件、客服 SOP、流程截圖、訂單狀態表或後台欄位可讓診斷更具體。

## 使用方法

1. 成熟產品依序用第 1 組拆任務流、第 2 組挑一至三個情境，再用第 3、4 組查資料與底層能力。早期 MVP 可先找摩擦再拆任務；已準備接工具時直接檢查資料與 readiness。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| 任务流程与能力图 | Prompt | 將頁面流程拆成意圖、情境、資料對象、動作、狀態、例外、責任與完成證據，產出 Task Flow & Capability Map。 | [工具檔案](../toolkits/agent-ready-product.md) |
| 特工安置查找器 | Prompt | 依高頻、低風險、偏好穩定與錯誤可恢復四個準則，找出一至三個最值得先做的 AI agent 情境。 | [工具檔案](../toolkits/agent-ready-product.md) |
| 代理可读服务层 | Prompt | 審查 agent 能否讀懂能力、限制、價格、優惠、庫存、風險與信任證據，指出資料缺口及收據需求。 | [工具檔案](../toolkits/agent-ready-product.md) |
| 特工准备五部分评分卡 | Prompt | 檢查持久狀態、狀態機、所有權、明確動詞及審計歷史與權限，產出評分、交易責任檢查、上線前必修項及三十天改進順序。 | [工具檔案](../toolkits/agent-ready-product.md) |

## 使用重點

Prompt 只提供診斷與改進順序，不能取代實作、權限設計或實際操作驗證。原文中文名稱存在翻譯不一致，工具原文完整保留。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/Dfstwfxmciq13ZkBEzecvggYnnd)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/USWew9vlGigJ6Zk0AFJcXWTbnfb)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
