# 企業 AI 實施工具包

五個 Prompt 從個人工作流到組織工具生態，協助盤點自動化介面、設計工具比較實驗、評估 Agent 基底、配置權限層級與計算依賴鏈可靠性。

分類：工作流、企業 AI 與自動化

## 工具原文

[開啟完整原文](../toolkits/enterprise-ai-implementation.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/enterprise-ai-implementation.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

選擇個人 AI 工作流、評估組織 Agent 部署、設計操作權限，或想理解外部依賴造成的可靠性瓶頸時。

## 前置需求

- 可進行多輪訪談的 AI；需有實際工作與工具清單。組織路徑另需工具狀態、交接問題、Agent actions、現有核准規則與依賴服務資訊。

## 使用方法

1. 個人路徑：跑 Prompt 1，提供每週實際工具與任務；從結果挑一項工作交給 Prompt 2 設計一週比較實驗。
2. 組織路徑：跑 Prompt 3，提供六大 domain 的工具與交接問題。
3. 將 Agent Infrastructure 的 actions 交給 Prompt 4，確定 Tier 0–4、審核、升級與回復方案。
4. 把 action 的依賴鏈交給 Prompt 5，確認 uptime 數據或假設後計算三種場景。
5. 已有部分資料時，可直接選用對應的單一 Prompt。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Personal Workflow Auditor | Prompt | 把每週工具分成 API-Connected、GUI-Only、File-Based、Unknown，產出自動化部署分流與前三項 quick wins。 | [工具檔案](../toolkits/enterprise-ai-implementation.md) |
| Default vs Specialist Measurement Designer | Prompt | 選出能公平比較的重複任務，建立成功標準、共同輸入、量測紀錄與一週執行計畫。 | [工具檔案](../toolkits/enterprise-ai-implementation.md) |
| Organizational Substrate Auditor | Prompt | 依 persistent state、state machine、ownership、defined verbs、audit history 評估組織工具，找出工作狀態流失與系統交接斷點。 | [工具檔案](../toolkits/enterprise-ai-implementation.md) |
| Permission Tier Architect | Prompt | 依可逆性、影響範圍、頻率與可驗證性，把 Agent actions 分配到 Tier 0–4，設計審核、升級、回復與擴大自主權條件。 | [工具檔案](../toolkits/enterprise-ai-implementation.md) |
| Agent Reliability Stress Tester | Prompt | 將依賴 uptime 相乘，換算停機時間，辨識最弱依賴，並比較目前、加入 fallback 與額外依賴下降三種場景。 | [工具檔案](../toolkits/enterprise-ai-implementation.md) |

### Personal Workflow Auditor

訂閱 Agent、規劃自動化 rollout 或找出重複工作中的自動化機會之前。

1. 貼上 Prompt 1。
2. 提供角色、實際週工作、工具清單、每項任務、耗時與整合狀態。
3. 確認盤點結果，再閱讀 readiness scorecard 與 deployment triage map。

### Default vs Specialist Measurement Designer

想以資料比較公司預設 AI 與另一個工具，作為換工具的依據時。

1. 貼上 Prompt 2，提供預設工具、候選工具與週任務。
2. 確認頻率、耗時、品質判斷、受眾與兩工具能否用相同輸入。
3. 採用選出的任務、log template 與 run plan；每次完成後記錄時間、返工及品質。

### Organizational Substrate Auditor

組織評估 Agent readiness，或要決定哪些現有系統優先修整、暴露 API／MCP 時。

1. 貼上 Prompt 3。
2. 提供 engineering、sales、support、HR、finance、ops 工具，以及組織規模、產業和具體交接問題。
3. 確認盤點，保存三層工具地圖、gaps、fractures 與排序 action plan。

### Permission Tier Architect

Agent 即將操作實際流程，需要逐項定義授權與人工核准邊界時。

1. 貼上 Prompt 4，提供具體 action 清單。
2. 補充 stakeholders、現有人工核准規則、風險偏好與過往事故。
3. 確認背景後，檢查 tier assignments、escalation rules、review requirements 與 rollback plan。

### Agent Reliability Stress Tester

Agent 依賴多個外部服務，需要評估端到端可用性與改善瓶頸時。

1. 貼上 Prompt 5，列出全部外部依賴。
2. 提供實際 uptime，或逐項確認 Prompt 提出的預設假設。
3. 檢查乘法與停機換算，閱讀三場景比較後討論 fallback、SLA 或替代方案。

## 使用重點

原文的平台分流與模型版本屬文章框架；可靠性計算的 uptime 預設值是假設，必須先確認，不能當成特定服務的已核實 SLA。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/YjojwxVJhiXafSkhFXycJkAGnnc)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/FjM6wvNVUi3TFXkIoF6cic1anIk)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
