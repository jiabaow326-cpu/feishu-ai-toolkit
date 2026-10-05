# 飛書 AI 工具庫

完整收錄飛書文章中的提示詞、Hook、Skill、Output Style 與安裝附件，並附上繁體中文的工具說明和使用方法。工具正文保留來源原文，可直接複製；不必先取得飛書來源頁的權限。

整理日期：2026-10-05。涵蓋 **29 篇文章、29 個工具包、116 項工具**。

## 開始使用

1. 從下方分類找到要完成的工作，開啟「說明與用法」。
2. 閱讀適用情境與前置需求，選擇包內對應工具。
3. 開啟工具原文，複製完整 Prompt 到適用的 AI；回答工具的提問並提供工作資料。
4. Hook、Skill、Output Style 請依該包說明取用 `assets/` 的原始檔案，確認安裝位置後再安裝。

## 分類目錄

| 分類 | 工具包 | 工具項目 |
| --- | ---: | ---: |
| [任務定義與品質評估](categories/planning.md) | 4 | 12 |
| [工作流、企業 AI 與自動化](categories/automation.md) | 7 | 25 |
| [程式開發、審查與 Hooks](categories/coding.md) | 5 | 42 |
| [AI 指令文件與 Skills](categories/instructions.md) | 3 | 6 |
| [工具選擇與模型分工](categories/routing.md) | 4 | 12 |
| [安全、權限與 API 金鑰](categories/security.md) | 2 | 3 |
| [輸出風格、HTML 與瀏覽器任務](categories/communication.md) | 3 | 13 |
| [Token 與 Context 效率](categories/context.md) | 1 | 3 |

## 所有工具包

| 工具包 | 作用 | 使用說明 | 原文 |
| --- | --- | --- | --- |
| Codex 任務指揮工具包 | 用四支 Prompt 完成交辦前判斷、整理工作資料夾、寫成可驗收任務與驗證成果。 | [說明與用法](guides/codex-task-command.md) | [完整工具](toolkits/codex-task-command.md) |
| Goal & Taste Toolkit | 將模糊任務寫成可驗證的長任務目標，並從對 AI 產出的修改歷史提煉品質標準。 | [說明與用法](guides/goal-taste.md) | [完整工具](toolkits/goal-taste.md) |
| Loop 工程工具包 | 先判斷任務適不適合做成 Loop，再建立可檢查的驗收標準與九欄位執行規格。 | [說明與用法](guides/loop-engineering.md) | [完整工具](toolkits/loop-engineering.md) |
| 任務交辦 Prompt Set：判斷階段、從零建立 Brief、送出前體檢 | 先判斷任務階段，再建立目標、背景、素材、邊界與完成定義五欄位 Brief，或檢查已有交辦訊息。 | [說明與用法](guides/task-brief.md) | [完整工具](toolkits/task-brief.md) |
| 2C 產品代理入口診斷提示集 | 把產品頁面流程拆成 agent 任務，找出值得 AI 化的情境，檢查服務資料與底層狀態、權限和責任。 | [說明與用法](guides/agent-ready-product.md) | [完整工具](toolkits/agent-ready-product.md) |
| AI Builder 縱軸工具包 | 從 workflow 拆解、五層 stack 審查、三維度評估，到是否採用 multi-agent 的四組診斷 Prompt。 | [說明與用法](guides/ai-builder.md) | [完整工具](toolkits/ai-builder.md) |
| 自動化交辦包 | 兩個完整 Coding Agent Prompt：從 Make／n8n 匯出 JSON 判斷搬移或保留，或從新需求訪談開始，依六欄 SPEC 完成實作、測試、部署與交接。 | [說明與用法](guides/automation-choice.md) | [完整工具](toolkits/automation-choice.md) |
| Workflow Asset Miner Prompt + AI Council Discussion Prompt | 從個人工作歷史挖掘可重用流程，並以五個角度審查重要決策的兩組 Prompt。 | [說明與用法](guides/codex-workflow-council.md) | [完整工具](toolkits/codex-workflow-council.md) |
| 企業 AI 實施工具包 | 五個 Prompt 從個人工作流到組織工具生態，協助盤點自動化介面、設計工具比較實驗、評估 Agent 基底、配置權限層級與計算依賴鏈可靠性。 | [說明與用法](guides/enterprise-ai-implementation.md) | [完整工具](toolkits/enterprise-ai-implementation.md) |
| Graph Workflow Builder Prompt Set | 先判斷工作是否需要 Graph，再建立 Node／Edge／State 藍圖，以及 Gate、Verifier、Retry、人工批准與 Work Memory 契約。 | [說明與用法](guides/graph-workflow.md) | [完整工具](toolkits/graph-workflow.md) |
| Human SOP → Agentic Workflow 拆解工具包 | 用五組可串接的 Prompt，把人類 SOP 拆成標準化節點，補齊隱性判斷並規劃工具接點與人工確認。 | [說明與用法](guides/human-sop-agentic-workflow.md) | [完整工具](toolkits/human-sop-agentic-workflow.md) |
| Brownfield 安全改動 Prompt Set | 四個 Prompt 串起既有專案探勘、帶邊界的改動規格、Diff 初審與影響範圍回歸檢查，保留人工最後驗收。 | [說明與用法](guides/brownfield-safe-change.md) | [完整工具](toolkits/brownfield-safe-change.md) |
| Claude Code Hooks：15 個情境與專屬推薦 Prompt | 提供 15 支建立 Hook 的原始需求 Prompt，另用只讀 Prompt 從本機 session 找出重複提醒和固定流程，產出帶證據的 Hook 推薦清單。 | [說明與用法](guides/claude-hooks.md) | [完整工具](toolkits/claude-hooks-recommender.md) |
| Cross-Model Review Kit | 提供 Claude Code 一鍵安裝與驗收 Prompt、Stop hook 和 codex-peer-review Skill，讓 plan／spec 在定稿前與 Codex 互審。 | [說明與用法](guides/cross-model-review.md) | [完整工具](toolkits/cross-model-review.md) |
| Workflow 啟動指令包：Bug 掃描、Code Review、計畫壓測 | 三條 dynamic workflow 觸發 Prompt，以並行廣度、獨立驗證及單一收斂三層，執行 codebase Bug 掃描、多維審查或動工前方案壓力測試。 | [說明與用法](guides/dynamic-workflows.md) | [完整工具](toolkits/dynamic-workflows.md) |
| Matt Pocock 工作流與寫作技能 | 複製文章介紹的官方開源技能，覆蓋需求釐清、原型、交接、大型決策地圖、需求分診、除錯、測試、審查與寫作；附官方安裝指令、現行更名版、setup 及直接依賴。 | [說明與用法](guides/matt-pocock-workflow.md) | [完整工具](toolkits/matt-pocock-workflow.md) |
| AI Instructions Rebuild Set | 逐條審查一份 CLAUDE.md、AGENTS.md、Custom Instructions 或 Skill，整理 KEEP、REWRITE、MOVE_TO_REFERENCE 與 DELETE_CANDIDATE，產出完整精簡候選版與待測清單。 | [說明與用法](guides/ai-instructions-rebuild.md) | [完整工具](toolkits/ai-instructions-rebuild.md) |
| CLAUDE.md／AGENTS.md 健檢 Prompt | 逐條核對有效指令載入來源、專案現況與可查證事實，按選擇對照目前模型官方提示指南，建議留、改、搬、刪或待驗。 | [說明與用法](guides/claude-md-checkup.md) | [完整工具](toolkits/claude-md-checkup.md) |
| Skill Craftsman Toolkit | 四支 Prompt 覆蓋 Skill 盤點、反推第一版 SKILL.md、觸發診斷及執行後迭代。 | [說明與用法](guides/skill-craftsman.md) | [完整工具](toolkits/skill-craftsman.md) |
| AI 分工系統建立 Prompt Kit | 評估新 AI 工具、審查目前工具組合，並把真實任務分配到合適工具的三組 Prompt。 | [說明與用法](guides/ai-routing-system.md) | [完整工具](toolkits/ai-routing-system.md) |
| Astra 實作體驗包 | 兩份原始繁體中文 Prompt，建立產品 Landing Page 或互動 3D 扭蛋機，附正式 Goal token 預算與操作驗收。 | [說明與用法](guides/astra-experience.md) | [完整工具](toolkits/astra-experience.md) |
| 個人 Model Routing 工作流拆解 Prompt Set | 四支 Prompt 將重複工作拆成交付鏈，分配角色、模型強度與推理強度，查開放權重候選，設計審查與停損儀表板。 | [說明與用法](guides/model-routing.md) | [完整工具](toolkits/model-routing.md) |
| Opus 工作流升級套件 | 三支獨立 Prompt 改善意圖表達、跨模型評審與每週模型分工，輸出可重用模板、審查清單及路由表。 | [說明與用法](guides/opus-workflow-upgrade.md) | [完整工具](toolkits/opus-workflow-upgrade.md) |
| API Key 止血包 | 依專案與外部服務盤點 API keys 及其他憑證的 metadata，檢查最小權限、花費上限、替身 key 與最壞損失，排出優先修整項目。 | [說明與用法](guides/api-key-blast-radius.md) | [完整工具](toolkits/api-key-blast-radius.md) |
| Codex Security Bridge Kit | 用兩個 Prompt 判讀 Security Finding 的證據，並把 repository 掃描與 staging、production、第三方及維運驗證串成有明確範圍的清單。 | [說明與用法](guides/codex-security-bridge.md) | [完整工具](toolkits/codex-security-bridge.md) |
| ChatGPT Chrome 六個實戰工具與使用方式 | 文章正文中的六組可複製 Prompt，涵蓋訂閱報帳、餐廳空位比較、App Store 送審、退款草稿、海報設計與公開資料整理。 | [說明與用法](guides/chatgpt-chrome.md) | [完整工具](toolkits/chatgpt-chrome.md) |
| 三套 Output Style 一鍵安裝包 | 三套 Claude Code Output Style 原始文件，以及安裝與專屬風格校準 Prompt。 | [說明與用法](guides/claude-output-styles.md) | [完整工具](toolkits/claude-output-styles.md) |
| 理解防護套件 | 用自我訪談檢查是否理解自己的作品，再把說明升級成可分享的單檔 HTML 工作頁。 | [說明與用法](guides/html-workpage.md) | [完整工具](toolkits/html-workpage.md) |
| Token 效率自我體檢 | 將四層 Token 浪費框架與 Agent KISS Checklist 套用到個人使用習慣，產出診斷、對話交接摘要或 Agent 架構審查報告。 | [說明與用法](guides/token-efficiency-self-check.md) | [完整工具](toolkits/token-efficiency-self-check.md) |

## 檔案位置

- `toolkits/`：飛書匯出的完整工具原文，以及從文章正文整理出的完整工具段落。
- `guides/`：每包的用途、前置需求、操作步驟與各項工具說明。
- `assets/`：原始 ZIP、Python、SKILL.md、Output Style 等可取用附件。
- `categories/`：依工作用途分類的索引。
- `data/tools.json`：完整工具索引，可用於搜尋、再整理或建立自己的工具目錄。
- `data/file-manifest.json`：公開檔案的 SHA256 與大小，方便核對下載內容。

## 來源與使用

各工具說明頁都保留來源。工具檔案沿用原文中的作者、出處及授權資訊；外部開源附件保留其授權文件。此整理不替原工具更改授權。來源中的模型、產品版本與操作介面依工具原文記載，使用時以實際環境為準。

本次整理核對了內容、附件及內部連結；未執行或安裝收錄的工具。飛書的臨時圖片授權連結未納入公開內容。

[查看來源與更新方式](CONTRIBUTING.md)
