# Workflow 啟動指令包：Bug 掃描、Code Review、計畫壓測

三條 dynamic workflow 觸發 Prompt，以並行廣度、獨立驗證及單一收斂三層，執行 codebase Bug 掃描、多維審查或動工前方案壓力測試。

分類：程式開發、審查與 Hooks

## 工具原文

[開啟完整原文](../toolkits/dynamic-workflows.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/dynamic-workflows.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

需要廣泛掃描並控制假陽性、從多角度審查明確變更，或在重大決策實作前比較競爭方案時。

## 前置需求

- 原文指定使用支援 dynamic workflows 的 Claude Code（標示 research preview、v2.1.154 以上與付費方案）；使用前需核對目前功能可用性。另需明確範圍、評估重點與 Token 預算。

## 使用方法

1. 在可使用 dynamic workflows 的 Claude Code 選擇對應 Prompt，完整貼上。
2. 依序回答範圍、問題／評分維度、模型路由與 Token 預算；第一次掃描先用單一子資料夾。
3. 核對理解摘要，查看 workflow 計畫並確認執行。
4. 用 /workflows 查看進度，檢查最終報告；依原文可在成功跑過後存為可重用指令。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Codebase Bug Sweep | Prompt | 便宜模型按檔案並行找候選問題，每項派三個獨立 skeptic 對抗驗證，再由強模型去重並整理 audit。 | [工具檔案](../toolkits/dynamic-workflows.md) |
| Multi-Dimensional Code Review | Prompt | 按 correctness、security、performance、可維護性與簡化等不同維度並行審查單一變更，獨立驗證後產出合併建議。 | [工具檔案](../toolkits/dynamic-workflows.md) |
| Plan Stress-Test Panel | Prompt | 由不同最佳化角度獨立提案，以 judge panel 按使用者標準評分，再綜合最佳方案與落選方案的具體優點。 | [工具檔案](../toolkits/dynamic-workflows.md) |

### Codebase Bug Sweep

接手陌生 codebase，或大改前需找出潛在 Bug、安全問題與 unsafe patterns 時。

1. 貼上 Prompt 1，提供 repo／資料夾、問題類型、預算與模型路由。
2. 先以小範圍查看計畫並確認執行。
3. 檢查 audit 的掃描範圍、Token 消耗、通過驗證問題與檔案行號。

### Multi-Dimensional Code Review

PR 或分支合併前，或想建立可重用的多角度 review 流程時。

1. 貼上 Prompt 2，指定 PR、分支或完整 diff。
2. 選擇審查維度、預算及是否要保存指令，確認計畫再執行。
3. 閱讀逐維度發現、跨維度重點與 merge 建議。

### Plan Stress-Test Panel

架構選型、遷移或產品方向等重大決策投入實作之前。

1. 貼上 Prompt 3，提供決策、硬限制、評分標準、對立切角與預算。
2. 確認計畫再執行獨立提案與 panel 評審。
3. 檢查候選評分、真實分歧、嫁接改良及推薦仍依賴的風險前提。

## 使用重點

本次僅完整保存原文，沒有執行任何 workflow。版本、模型、research preview 可用性與 Token 硬上限能力未在本次重新查證，採用前需依目前工具與官方文件核對。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/GoPhw9WrsiYo3YkkQfqc2437nah)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/LpgwwpRaSiRzy5kEiAgcnG1ynEg)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
