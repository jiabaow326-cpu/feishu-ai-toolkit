# Matt Pocock 工作流與寫作技能

複製文章介紹的官方開源技能，覆蓋需求釐清、原型、交接、大型決策地圖、需求分診、除錯、測試、審查與寫作；附官方安裝指令、現行更名版、setup 及直接依賴。

分類：程式開發、審查與 Hooks

## 工具原文

[開啟完整原文](../toolkits/matt-pocock-workflow.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/matt-pocock-workflow.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

希望用可重複的技能改善 Agent 工程流程，或透過反向提問整理靈感並逐段寫作時。

## 前置需求

- 支援 Agent Skills 與讀寫檔案的 coding agent；本快照未執行或安裝。
- 入口技能需保留同目錄參考文件與被呼叫的依賴；工程工作先執行 setup 選 tracker 與文件配置。
- 三個寫作技能目前是 in-progress，disable-model-invocation: true，需使用者明確呼叫及持續參與選擇。
- 選 GitHub／GitLab tracker 時需對應 CLI 與使用者帳號；也可選本機 Markdown。除錯與驗證需可實際重現的環境。

## 使用方法

1. 按需求表選技能；要使用官方現行版，可選 Claude Code 插件，或 npx skills@latest add mattpocock/skills。
2. 需要這份固定快照時，複製完整技能目錄與直接依賴到該 Agent 支援的 skill 目錄，保留參考／設定／腳本／LICENSE。
3. 工程工作在每個 repo 初次使用時明確呼叫 /setup-matt-pocock-skills，依提問選 tracker、標籤與文件位置。
4. 提供真實目標、資料與可驗證環境，再明確呼叫對應入口；writing-great-skills 歷史版與 writing-for-agents 現版依需求擇一。
5. 寫作先用 writing-fragments 收集素材，再選 writing-beats 逐拍組裝或 writing-shape 逐段成文；親自參與選開頭及接續方向。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| grill-me | Skill | 連續追問想法、計畫或設計，釐清每個分支與未定決策。 | [工具檔案](../assets/matt-pocock/grill-me/SKILL.md) |
| prototype | Skill | 以拋棄式 UI 或狀態／邏輯原型回答設計問題，附兩類原型指引。 | [工具檔案](../assets/matt-pocock/prototype/SKILL.md) |
| handoff | Skill | 將對話濃縮成存於作業系統暫存區的交接文件，引用已有文件並移除敏感資訊。 | [工具檔案](../assets/matt-pocock/handoff/SKILL.md) |
| grill-with-docs | Skill | 透過追問同步建立共用術語，更新 GLOSSARY.md 與 ADR。 | [工具檔案](../assets/matt-pocock/grill-with-docs/SKILL.md) |
| wayfinder | Skill | 將大型工作建立成 issue tracker 決策地圖，逐票解決問題並整理新發現的路徑。 | [工具檔案](../assets/matt-pocock/wayfinder/SKILL.md) |
| triage | Skill | 分類、查驗與追問 issue 或外部 PR，維持類別／狀態角色並產出 Agent brief。 | [工具檔案](../assets/matt-pocock/triage/SKILL.md) |
| diagnosing-bugs | Skill | 先建立能抓到真實症狀的重現迴圈，再縮小案例、驗證假設、修正與回歸驗證。 | [工具檔案](../assets/matt-pocock/diagnosing-bugs/SKILL.md) |
| tdd | Skill | 以 red-green-refactor 驅動逐個垂直切片，附測試與 mocking 參考。 | [工具檔案](../assets/matt-pocock/tdd/SKILL.md) |
| code-review | Skill | 平行審查固定範圍的修改，分別檢查 coding standards 與原需求忠實度。 | [工具檔案](../assets/matt-pocock/code-review/SKILL.md) |
| writing-great-skills | Skill | 保存文章所提歷史技能；說明觸發、context load、cognitive load 與漸進式揭露。 | [工具檔案](../assets/matt-pocock/writing-great-skills/SKILL.md) |
| writing-for-agents | Skill | writing-great-skills 的現行替代，指導 skills、AGENTS.md／CLAUDE.md 等 Agent 文件寫法。 | [工具檔案](../assets/matt-pocock/writing-for-agents/SKILL.md) |
| writing-fragments | Skill | 反向提問挖出寫作素材，逐次附加片段到 Markdown，尚不訂文章結構。 | [工具檔案](../assets/matt-pocock/writing-fragments/SKILL.md) |
| writing-beats | Skill | 以讀者已知概念為起點，每次提出候選 beat，使用者選擇後逐拍組成文章。 | [工具檔案](../assets/matt-pocock/writing-beats/SKILL.md) |
| writing-shape | Skill | 素材檔唯讀，選開頭、論點與形式，逐段討論並另存成文。 | [工具檔案](../assets/matt-pocock/writing-shape/SKILL.md) |
| setup-matt-pocock-skills | Skill | 每個 repo 初次使用工程技能時，設定 issue tracker、triage 標籤及文件位置。 | [工具檔案](../assets/matt-pocock/setup-matt-pocock-skills/SKILL.md) |

## 附件與其他原文

- [assets/matt-pocock/README.md](../assets/matt-pocock/README.md)
- [assets/matt-pocock/LICENSE](../assets/matt-pocock/LICENSE)
- [assets/matt-pocock/sources.json](../assets/matt-pocock/sources.json)
- [assets/matt-pocock/grill-me/SKILL.md](../assets/matt-pocock/grill-me/SKILL.md)
- [assets/matt-pocock/prototype/SKILL.md](../assets/matt-pocock/prototype/SKILL.md)
- [assets/matt-pocock/handoff/SKILL.md](../assets/matt-pocock/handoff/SKILL.md)
- [assets/matt-pocock/grill-with-docs/SKILL.md](../assets/matt-pocock/grill-with-docs/SKILL.md)
- [assets/matt-pocock/wayfinder/SKILL.md](../assets/matt-pocock/wayfinder/SKILL.md)
- [assets/matt-pocock/triage/SKILL.md](../assets/matt-pocock/triage/SKILL.md)
- [assets/matt-pocock/diagnosing-bugs/SKILL.md](../assets/matt-pocock/diagnosing-bugs/SKILL.md)
- [assets/matt-pocock/tdd/SKILL.md](../assets/matt-pocock/tdd/SKILL.md)
- [assets/matt-pocock/code-review/SKILL.md](../assets/matt-pocock/code-review/SKILL.md)
- [assets/matt-pocock/writing-fragments/SKILL.md](../assets/matt-pocock/writing-fragments/SKILL.md)
- [assets/matt-pocock/writing-beats/SKILL.md](../assets/matt-pocock/writing-beats/SKILL.md)
- [assets/matt-pocock/writing-shape/SKILL.md](../assets/matt-pocock/writing-shape/SKILL.md)
- [assets/matt-pocock/writing-for-agents/SKILL.md](../assets/matt-pocock/writing-for-agents/SKILL.md)
- [assets/matt-pocock/setup-matt-pocock-skills/SKILL.md](../assets/matt-pocock/setup-matt-pocock-skills/SKILL.md)
- [assets/matt-pocock/writing-great-skills/SKILL.md](../assets/matt-pocock/writing-great-skills/SKILL.md)
- [assets/matt-pocock/grilling/SKILL.md](../assets/matt-pocock/grilling/SKILL.md)
- [assets/matt-pocock/domain-modeling/SKILL.md](../assets/matt-pocock/domain-modeling/SKILL.md)
- [assets/matt-pocock/research/SKILL.md](../assets/matt-pocock/research/SKILL.md)
- [assets/matt-pocock/codebase-design/SKILL.md](../assets/matt-pocock/codebase-design/SKILL.md)

## 使用重點

官方原始 SKILL.md、code／settings／同目錄參考文件均保留 bytes；原 MIT LICENSE 在每個技能目錄與包根目錄保存。

writing-great-skills 在官方已更名；保存更名前 commit 的原檔，另存現行 writing-for-agents。

文章舊版與現行工具存在差異：CONTEXT.md 慣例已改為 GLOSSARY.md，wayfinder 以 tracker 決策票為主，writing-fragments 首次寫入帶 H1 工作標題。

三個寫作技能在 upstream in-progress；這份快照保留原文，不將工具內容改成符合文章的敘述。

僅複製文章涉及技能、現行替代、官方 setup 與四個直接依賴，未複製整個官方 repository。

飛書匯出中的私密圖片未收入公開包。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/ZWIgwxFMMi7tQokVmKoc2KrfnAh)
- [官方工具來源](https://github.com/mattpocock/skills)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
