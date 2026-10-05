# Matt Pocock 工作流與寫作技能

這組工具來自 [Matt Pocock 官方技能倉庫](https://github.com/mattpocock/skills)，對應飛書文章 [Matt Pocock 的 AI 工作流程深度分析：高级使用与被低估的“写作技能”](https://kcn4ucks9zgj.feishu.cn/wiki/ZWIgwxFMMi7tQokVmKoc2KrfnAh)。文章未提供自寫 Prompt 或安裝指令，因此收錄它介紹的官方技能原檔，並依官方安裝說明補上使用方式。

英文 `SKILL.md`、參考文件、設定與腳本範本保留原始內容。本文的繁體中文說明供選擇工具與操作時參考。

## 按需求選工具

| 需求 | 工具原檔 | 作用與輸入 |
| --- | --- | --- |
| 想法模糊、需求尚未說清楚 | [grill-me](../assets/matt-pocock/grill-me/SKILL.md) | 連續追問計畫或設計，逐一釐清分支。提供想法、目標與限制，並親自回答。需同時保留 `grilling`。 |
| 需要具體原型才能判斷 | [prototype](../assets/matt-pocock/prototype/SKILL.md) | 針對狀態／邏輯或 UI 設計問題製作拋棄式原型；附 `LOGIC.md`、`UI.md`。提供要驗證的問題，將結果作為設計決策。 |
| 對話太長，要交給下一個 Agent | [handoff](../assets/matt-pocock/handoff/SKILL.md) | 將對話濃縮成交接文件，參照已有規格、ADR、issue、commit 或差異，不重抄。可附上下一輪目標；文件存於作業系統暫存區。 |
| 工程需求需累積術語與決策 | [grill-with-docs](../assets/matt-pocock/grill-with-docs/SKILL.md) | 追問時建立共用語言，更新 `GLOSSARY.md` 與 ADR。需 `grilling`、`domain-modeling`。 |
| 工作超過一次對話能處理的範圍 | [wayfinder](../assets/matt-pocock/wayfinder/SKILL.md) | 在 issue tracker 建立決策地圖、子票與阻擋關係，先確定目的地，再逐票釐清。提供大型想法，或既有地圖連結。 |
| 零散需求、issue 與外部 PR 太多 | [triage](../assets/matt-pocock/triage/SKILL.md) | 分類、查驗、追問需求並寫成 Agent brief；每件需求維持一個類別角色與一個狀態角色。附 brief 與 out-of-scope 參考。 |
| 難以定位的 bug 或效能退步 | [diagnosing-bugs](../assets/matt-pocock/diagnosing-bugs/SKILL.md) | 先建立能對真實症狀報錯的回饋迴圈，再縮小重現、提出可驗證假設、加探針、修正與回歸驗證。提供症狀、觸發條件及可重現環境。 |
| 寫功能或修 bug，要用測試引導 | [tdd](../assets/matt-pocock/tdd/SKILL.md) | 以 red-green-refactor 一次做一個垂直切片；附測試與 mocking 指引。介面設計未定時會讀 `codebase-design`。 |
| 需要客觀審查修改是否合規與合題 | [code-review](../assets/matt-pocock/code-review/SKILL.md) | 固定比較起點，讓平行子代理分別檢查 coding standards 與原始 spec／issue。提供要比較的差異及原需求。 |
| 想改善 Skill 的提示結構 | [writing-great-skills：歷史版](../assets/matt-pocock/writing-great-skills/SKILL.md) | 保存文章提到的原技能與 `GLOSSARY.md`；說明 context load、cognitive load、觸發與漸進式揭露。現版已更名。 |
| 要建立或改寫 Agent 文件 | [writing-for-agents：現版](../assets/matt-pocock/writing-for-agents/SKILL.md) | `writing-great-skills` 的現行替代，涵蓋 skills、`AGENTS.md`／`CLAUDE.md` 與 Agent 經指引讀取的文件；附 `SKILL-MECHANICS.md`。 |
| 有靈感，尚未決定文章結構 | [writing-fragments](../assets/matt-pocock/writing-fragments/SKILL.md) | 反向提問、挖出素材並逐次附加到 Markdown；先收集句子、例子、片段與概念，不先訂大綱。 |
| 已有素材，要逐拍選擇文章走向 | [writing-beats](../assets/matt-pocock/writing-beats/SKILL.md) | 先確定讀者已知概念，每次提出 2–3 個可接續的 beat；你選擇後才寫那一拍。 |
| 已有素材，要逐段整理成完整文章 | [writing-shape](../assets/matt-pocock/writing-shape/SKILL.md) | 完整讀素材，選定開頭與論點，再逐段討論內容及形式；原素材唯讀，成文另存。 |
| 第一次在專案使用工程技能 | [setup-matt-pocock-skills](../assets/matt-pocock/setup-matt-pocock-skills/SKILL.md) | 設定 issue tracker、triage 標籤與文件配置，每個 repo 執行一次。可使用本機 Markdown tracker。 |

## 官方安裝方式

以下指令保留 [官方 README](https://github.com/mattpocock/skills/blob/24fe0ef7737efae15c87225755e9f6f5965e4888/README.md) 原文。本倉庫僅複製工具，整理時未執行安裝或技能。

Claude Code 插件安裝：

```bash
claude plugins install mattpocock-skills
```

或在 Claude Code 對話執行：

```text
/plugin install mattpocock-skills
```

Codex 或其他支援 Agent Skills 的工具，使用官方安裝器：

```bash
npx skills@latest add mattpocock/skills
```

在安裝器選擇需要的技能與 Agent，工程工作請包含 `setup-matt-pocock-skills`。Claude Code 的插件與 `skills.sh` 安裝方式擇一，避免同一技能重複出現。

每個 repo 初次使用工程技能時，在 Agent 中執行：

```text
/setup-matt-pocock-skills
```

依提問選 issue tracker、triage 標籤及文件位置。這一步會寫入你的專案設定；無線上 tracker 時可選本機 Markdown。

使用 `skills.sh` 安裝的檔案可自行編輯；需要跟進官方變更時使用：

```bash
npx skills update
```

若只使用這份固定快照，將想用的技能**整個目錄**放入你的 Agent 支援的 skill 目錄，保留其參考文件、`agents/`、`scripts/` 與 `LICENSE`。`grill-me` 需一併放入 `grilling`；`grill-with-docs` 另需 `domain-modeling`；`wayfinder` 需 `grilling`、`domain-modeling`、`research`、`prototype` 及 setup；`triage` 需 setup、`grilling`、`domain-modeling`，有 bug 時還會用 `diagnosing-bugs`；`tdd` 的設計參考需 `codebase-design`。各 Agent 的技能目錄與呼叫語法不同，請依該工具文件選擇安裝位置。

## 兩種常見使用流程

工程工作可先用 `grill-with-docs` 釐清需求；卡在設計問題時用 `prototype`，超大工作用 `wayfinder` 管理決策，零散需求用 `triage`。實作時用 `tdd`；遇到 bug 用 `diagnosing-bugs`；交付前用 `code-review`。對話需換新視窗時用 `handoff`，將產出的暫存文件交給下一個 Agent。

寫作時先明確呼叫 `writing-fragments`，指定素材檔並回答提問。已有素材後，可選 `writing-beats` 逐拍組裝，或 `writing-shape` 逐段成文。兩者都會先釐清讀者已懂什麼，再讓你決定開頭與接續內容；`writing-shape` 不改素材檔。你需要持續參與選擇與確認，這些技能會等待你的方向。

三個寫作技能目前位於官方 `in-progress` 目錄，且原檔設定 `disable-model-invocation: true`，需由使用者明確呼叫。官方最新安裝器的選項可能改變；需要本快照中的寫作技能時，可按上面的整目錄方式安裝。

## 版本與原文保存

本快照於 2026-10-05 取得，現行官方來源 commit 為 `24fe0ef7737efae15c87225755e9f6f5965e4888`。`writing-great-skills` 保留更名前 commit `6bcbcb09e2f1ed5fa20b4e890c732ecbb58c6b64` 的版本；[更名紀錄](https://github.com/mattpocock/skills/commit/1fc6573e0e300118ce342fb9365521c9c34eefd4) 可核對與現版的關係。

文章中的舊版細節與這次官方快照有差異：共用術語檔現為 `GLOSSARY.md`；`wayfinder` 的決策地圖以 issue tracker 為主，也支援本機 Markdown；`writing-fragments` 第一次寫入會建立一個 H1 工作標題，正文不加內部標題。原始技能未為了符合文章敘述而改寫。

共用依賴原檔：[grilling](../assets/matt-pocock/grilling/SKILL.md)、[domain-modeling](../assets/matt-pocock/domain-modeling/SKILL.md)、[research](../assets/matt-pocock/research/SKILL.md)、[codebase-design](../assets/matt-pocock/codebase-design/SKILL.md)。

全部官方原檔來源、commit、大小與 SHA256 見 [sources.json](../assets/matt-pocock/sources.json)。Matt Pocock 的原作以 [MIT LICENSE](../assets/matt-pocock/LICENSE) 授權；每個技能目錄也保留授權檔。這份包只含文章涉及的技能、現行替代與直接依賴。
