# Skill Craftsman Toolkit

四支 Prompt 覆蓋 Skill 盤點、反推第一版 SKILL.md、觸發診斷及執行後迭代。

分類：AI 指令文件與 Skills

## 工具原文

[開啟完整原文](../toolkits/skill-craftsman.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/skill-craftsman.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

想把重複工作做成 Skill，或現有 Skill 不觸發、過度觸發、輸出不穩定時。

## 前置需求

- 原文建議 Claude；ChatGPT 或 Gemini 可產出 SKILL.md 後另部署。
- 準備流程描述、既有 session／產出，以及要診斷的 SKILL.md。

## 使用方法

1. 從零建立：Prompt 1 → 2 → 3，實跑任務後再用 Prompt 4 複盤。
2. 已有 Skill 出錯：先用 Prompt 3 判斷是否觸發問題，再用 Prompt 4 找具體 patch。
3. 將完整 Prompt 貼給 AI，依階段提供工作流、範例、SKILL.md 或失敗對話。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Skill Backlog Auditor | Prompt | 用重複性、專業知識及高出錯成本三種信號，產出按 ROI 排序的候選清單。 | [工具檔案](../toolkits/skill-craftsman.md) |
| Skill Reverse-Engineer | Prompt | 從 session、brain dump 或多份產出反推方法，產出完整 SKILL.md 和驗證提示。 | [工具檔案](../toolkits/skill-craftsman.md) |
| Skill Trigger Diagnostician | Prompt | 檢查 description 與觸發失敗例，產出可路由的修正版與驗證案例。 | [工具檔案](../toolkits/skill-craftsman.md) |
| Skill Retro Facilitator | Prompt | 將失敗按 body、references、scripts、subagent QA 分層，產出優先修正清單。 | [工具檔案](../toolkits/skill-craftsman.md) |

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/F1dowsAFBiBlmukE9Decn2MhnRg)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/Pd3mwf9oliTQDFkQ6tpcAtlfnbd)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
