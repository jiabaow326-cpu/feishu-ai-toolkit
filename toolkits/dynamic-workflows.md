# 🔧 本期工具

# Workflow 启动指令包：Bug 扫描、Code Review、计划压测

三条可直接贴进 Claude Code 的 dynamic workflow 触发指令：Codebase Bug Sweep 用便宜模型并行找雷再对抗验证、Multi\-Dimensional Code Review 对一个变更多视角体检、Plan Stress\-Test Panel 用 judge panel 在动工前压测方案。广度、验证、收敛、模型路由、预算上限都帮你写好。配套那篇深拆 Claude Code Dynamic Workflows 的 Patreon 文章。

这组工具配套那篇深拆 Claude Code Dynamic Workflows 的文章。文章把 workflow 的运作机制、六种品质模式、还有成本怎么控讲透，这三条 prompt 就是把那些分析变成你可以直接贴进 Claude Code、为自己的场景触发一个结构良好 workflow 的指令。

三条指令各对应一个最有价值的场景，全代码库的 Bug 扫描、多维度的 Code Review、还有动手前的计划压力测试。它们不是 JavaScript 脚本，是你贴给 Claude 的一段话。贴上之后 Claude 会先问你几个关键问题，范围要圈多大、预算上限多少、用哪个模型撒网，然后才帮你把 workflow 的脚本写出来、跑起来。每一条都已经替你把广度、验证、收敛三层，加上模型路由跟预算控制都写进去了，你不用每次自己重讲一遍。

## 提示

这三条都要在 Claude Code 里跑，因为 dynamic workflows 是 Claude Code 的功能（research preview，需要 v2\.1\.154 以上、付费方案）。贴上指令后，Claude 第一次一定会把计划摊给你看、问你要不要跑，不会偷偷烧钱。跑起来打 /workflows 看进度，跑得顺可以按 s 存成你自己的斜线指令复用。

## 怎么用这组 prompts

- 全代码库找雷：跑 Prompt 1（Codebase Bug Sweep），第一次先指一个文件夹试水温，看花多少再放大。

- PR 或分支 merge 前体检：跑 Prompt 2（Multi\-Dimensional Code Review），跑顺可以存成每周对新分支复用的指令。

- 重大决策动工前：跑 Prompt 3（Plan Stress\-Test Panel），让多个方案互相竞争再选一个。

## 包含内容

- **Prompt 1：Codebase Bug Sweep** — 便宜模型按文件并行找 bug，每个发现派 skeptic 对抗验证过滤假阳性，强模型收敛成 audit 报告

- **Prompt 2：Multi\-Dimensional Code Review** — 对一个 PR 或 diff 按多个维度平行审查，每个发现独立验证，收敛成分维度报告，可存成复用指令

- **Prompt 3：Plan Stress\-Test Panel** — 同一个决策让多个 agent 从不同角度各出方案，平行评审打分，从赢家收敛并嫁接落选方案的好点子

## 工具建议

三条都必须在 Claude Code 跑，因为 dynamic workflows 是它独有的功能。建议把 session 的预设模型设成 Opus 或 Sonnet 当收敛层，撒网层在指令里已经指定走 Haiku 省钱。产出都是纯文字报告，可以直接贴进你的 issue tracker、PR comment 或决策文件。

---

## Prompt 1

### Codebase Bug Sweep

**功能：**

对一个既有的 repo 或文件夹，用便宜模型大量并行找出散落的 bug、安全问题跟 unsafe pattern，再对每个发现派独立 agent 对抗验证、过滤假阳性，最后用强模型收敛成一份你可以直接行动的 audit 报告。

**什么时候用：**

你接手一个不熟的 codebase、或想在大改之前先摸清楚有多少雷；任务大到一个对话扫不完、又怕假阳性把你淹没的时候。

**你会拿到：**

一份 audit 报告，每个确认的问题附严重度、文件位置、为什么是真的（含对抗验证的票数）、跟建议修法；通不过验证的发现会先被滤掉、不进报告。

**可以接到哪：**

独立使用

**AI 会问你：**

- 要扫的范围，哪个 repo 或文件夹，建议先指一个子文件夹试水温

- 想找的问题类型，一般 bug、安全漏洞、效能、还是特定 pattern

- 这次的 token 预算上限

- 撒网层要不要用便宜模型（预设 Haiku），收敛层用哪个强模型（预设 Opus）

```SQL
<role>
You are orchestrating a Claude Code dynamic workflow that performs a codebase-wide bug sweep with adversarial verification. Your job is NOT to scan the code yourself in this conversation. Your job is to gather the scope and cost constraints from the user, then create and run a dynamic workflow that fans out cheap parallel finders, adversarially verifies every finding to filter false positives, and converges the survivors into one actionable audit report.
</role>

<context-gathering>
Work through this one question at a time. Do NOT dump all questions at once. Wait for each answer before moving on.

1. Scope: "要掃哪個範圍？給我 repo 或資料夾路徑。第一次強烈建議先指一個子資料夾，看花多少再放大。"
 - Wait.
2. Issue types: "想找哪種問題？一般 bug、security 漏洞、效能、unsafe pattern，還是某個特定模式？可以多選。"
 - Wait.
3. Budget: "這次的 token 預算上限設多少？例如 100k、300k。我會把它寫成硬上限，跑到頂就停。"
 - Wait.
4. Model routing: "撒網的 finder 用便宜模型可以嗎（預設 Haiku）？收斂報告用哪個強模型（預設 Opus）？"
 - Wait.
5. Sanity check: play back scope, issue types, budget, and model routing. "我這樣理解對嗎？確認後我就把這個 workflow 的計畫攤給你看，再問你要不要跑。" Wait for confirmation. If the user points the first run at the whole repo, push back and suggest one directory first.
</context-gathering>

<execution>
After confirmation, create and run a dynamic workflow with this shape, and let Claude Code show the plan for approval before it runs:

- Stage 1, Find (breadth): enumerate the files in scope and fan out one finder agent per file or per small batch, running on the cheap model. Each finder reports candidate issues with file, line, type, and a one-line rationale. Use a pipeline so each file flows on to verification as soon as its own scan finishes, instead of waiting for every file.
- Stage 2, Adversarial verify: for each candidate issue, spawn 3 independent skeptic agents on the cheap model, each instructed to REFUTE the issue and to default to "not a real bug" when uncertain. Keep the issue only if a majority fail to refute it. Discard the rest.
- Stage 3, Converge: pass only the surviving issues to a single synthesis agent on the strong model, which dedupes them, ranks by severity, and writes the audit report.

Enforce the user's token budget as a hard ceiling on the run. If the budget is small, scan fewer files rather than skipping the verification stage.
</execution>

<output-format>
The report exists so the user gets a list of real, verified problems they can act on, not a wall of unfiltered guesses.

Section purposes:
- 摘要: how many candidates were found, how many survived verification, total spend, so the user can judge the run.
- 確認的問題: each verified issue, so it can be fixed.
- 已濾掉: a short note that refuted findings were dropped, so the user trusts the filter.

格式：

## 摘要
（候選問題數、通過驗證數、總花費 token、掃描範圍。）

## 確認的問題
### {問題標題}
- 嚴重度: {High / Medium / Low}
- 位置: {檔案:行}
- 為什麼是真的: {說明，含對抗驗證 N 票中通過幾票}
- 建議修法: {具體方向}

## 已濾掉
（一句話：有多少候選在對抗驗證被推翻、未列入報告。）
</output-format>

<guardrails>
- You orchestrate; the agents read the code. Do not scan files yourself in the main conversation.
- Always set the user's token budget as a hard ceiling on the run.
- Default the finder stage to a cheap model and the synthesis stage to a strong model unless the user overrides.
- Never report a finding that did not survive majority adversarial verification.
- If the first run is pointed at the whole repo, push back and suggest a single directory first.
- Do not fabricate issues or file paths. Only report what agents actually found.
- Do not use markdown tables. Use bullet blocks.
- Output in Traditional Chinese, keeping technical terms in English.
</guardrails>
```





---

## Prompt 2

### Multi\-Dimensional Code Review

**功能：**

对一个明确的变更（PR、diff 或分支）做多视角体检，按 correctness、security、performance、可维护性、简化机会等维度平行审查，每个发现独立验证后收敛成一份分维度报告。跑顺了可以存成每周复用的指令。

**什么时候用：**

你改完一个 PR 或分支、merge 之前想从多个专业角度审一遍；或想把 code review 变成每周固定跑的流程。

**你会拿到：**

一份分维度的 review 报告，每个维度列出确认的问题（含位置、理由、修法建议），加一段跨维度总评跟 merge 建议。

**可以接到哪：**

独立使用（跑顺可存成 /review\-branch 每周复用）

**AI 会问你：**

- 要审的变更是是什么，PR 编号、分支名、还是一段 diff 或文件清单

- 你最在意哪些维度，correctness、security、performance、可维护性、简化，可全选

- 这次的 token 预算上限

- 跑顺之后要不要存成可复用的斜线指令

```SQL
<role>
You are orchestrating a Claude Code dynamic workflow that reviews one specific change across multiple independent dimensions and verifies each finding before reporting. Your job is to gather what is being reviewed and which dimensions matter, then create and run a workflow that fans out one reviewer per dimension, verifies each finding, and converges into a single multi-dimension review. You do not review the diff yourself in this conversation.
</role>

<context-gathering>
One question at a time. Wait for each answer.

1. Target: "要審的是什麼變更？給我 PR 編號、分支名、或一段 diff / 檔案清單。"
 - Wait.
2. Dimensions: "你最在意哪些維度？correctness、security、performance、可維護性、簡化機會。可以全選，也可以加你自己的。"
 - Wait.
3. Budget: "token 預算上限設多少？我會寫成硬上限。"
 - Wait.
4. Reuse: "如果這次跑得順，要不要我提醒你把它存成可複用的斜線指令，例如每週對新分支跑一次？"
 - Wait.
5. Sanity check: play back the target, the chosen dimensions, the budget, and whether to save for reuse. "對嗎？確認後我把計畫攤給你看再跑。" Wait.
</context-gathering>

<execution>
After confirmation, create and run a dynamic workflow with this shape, and let Claude Code show the plan for approval first:

- Stage 1, Review by dimension (breadth): fan out one reviewer agent per chosen dimension, each looking at the same change but only through its own lens (correctness, security, performance, maintainability, simplification). This is perspective-diverse coverage: different lenses, not duplicate reviewers. Use a pipeline so each dimension flows to verification as soon as it finishes.
- Stage 2, Verify each finding: for every finding a dimension raises, spawn an independent verifier that adversarially checks whether it is real and correctly scoped to this change. Drop findings that do not hold up.
- Stage 3, Converge: a single synthesis agent on the strong model merges the verified findings, removes duplicates that several lenses flagged, and writes one report grouped by dimension, ending with an overall merge recommendation.

Scope every agent strictly to the change under review, not the whole codebase. Enforce the token budget as a hard ceiling. If the user asked to save it, remind them after a clean run that they can press s in /workflows to save it as a command.
</execution>

<output-format>
The report exists so the user can decide whether to merge, with each concern traced to a dimension and already verified.

Section purposes:
- 總評: merge, hold, or needs-work, and why, up front.
- 各維度發現: the verified findings per lens, so concerns are organized by expertise.
- 跨維度重點: issues that more than one lens flagged, since those usually matter most.

格式：

## 總評：{可以 merge / 修完再 merge / 需要大改}
（兩三句說明。）

## 各維度發現
### {維度名稱，如 Correctness}
- 位置: {檔案:行}
- 問題: {說明}
- 建議: {修法}

## 跨維度重點
（被多個 lens 同時點到的問題，優先處理。）
</output-format>

<guardrails>
- You orchestrate; the agents read the diff. Do not review the change yourself in the main conversation.
- Give each dimension a genuinely different lens. Do not spawn duplicate identical reviewers.
- Scope all agents to the change under review, not the entire repository.
- Only report findings that passed verification.
- Always set the token budget as a hard ceiling.
- Do not fabricate line references. Only cite what agents actually read.
- Do not use markdown tables. Use bullet blocks.
- Output in Traditional Chinese, keeping dimension names and technical terms in English.
</guardrails>
```





---

## Prompt 3

### Plan Stress\-Test Panel

**功能：**

在动手实作之前，把一个还没做的决策或方案丢给多个 agent，从不同角度各自独立出一个版本，再用一批 judge 平行打分，最后从赢家收敛、嫁接落选方案的好点子，给你一个被压力测试过的方案。

**什么时候用：**

你面对一个重大决策（架构选型、迁移策略、产品方向），想在投入之前先把方案从多个角度想透，而不是锁死在第一个念头。

**你会拿到：**

一份方案压测报告，含推荐方案、每个候选方案的评分卡、从落选方案嫁接进来的改良、跟主要风险与前提。

**可以接到哪：**

独立使用

**AI 会问你：**

- 你要做的决策或方案是什么，连同已知的限制（时间、人力、技术栈、不能动的东西）

- 你最在意的评分标准，例如落地速度、风险、长期维护成本、使用者价值

- 想从哪几个角度生方案，预设用 MVP\-first、risk\-first、user\-first 等对立切角

- 这次的 token 预算上限

```Markdown
<role>
You are orchestrating a Claude Code dynamic workflow that stress-tests a plan or decision before any code is written. Your job is to gather the decision and its constraints, then create and run a judge-panel workflow: several agents each draft an independent plan from a distinct angle, a panel of judges scores them against the user's criteria, and a final agent synthesizes the strongest plan while grafting the best ideas from the runners-up. You do not design the plan yourself in this conversation.
</role>

<context-gathering>
One question at a time. Wait for each answer.

1. Decision: "你要做的決策或方案是什麼？連同你已知的硬限制一起講，例如時間、人力、現有技術棧、不能動的東西。"
 - Wait.
2. Criteria: "你最在意哪些評分標準？例如落地速度、風險、長期維護成本、使用者價值。我會讓 judge 照這些打分。"
 - Wait.
3. Angles: "想從哪幾個角度各生一版方案？預設我會用 MVP-first、risk-first、user-first 這種互相對立的切角，你也可以指定。"
 - Wait.
4. Budget: "token 預算上限設多少？寫成硬上限。"
 - Wait.
5. Sanity check: play back the decision, constraints, scoring criteria, angles, and budget. "對嗎？確認後我把計畫攤給你看再跑。" Wait.
</context-gathering>

<execution>
After confirmation, create and run a dynamic workflow with this shape, and let Claude Code show the plan for approval first:

- Stage 1, Draft (breadth): spawn one planner agent per angle, each working independently and blind to the others, each producing a complete plan optimized for its own angle (for example MVP-first, risk-first, user-first, cost-first). Run them in parallel.
- Stage 2, Judge: spawn a panel of judges that score every candidate plan against the user's stated criteria, each judge giving a score and a one-line reason per criterion. Use independent judges so a single judge's bias does not decide the outcome.
- Stage 3, Synthesize: a single agent on the strong model takes the highest-scoring plan as the base, grafts in the best specific ideas from the runner-up plans, and writes the final recommendation plus the key risks and assumptions it still rests on.

Enforce the token budget as a hard ceiling. The angles must be genuinely different optimization targets, not three versions of the same plan.
</execution>

<output-format>
The report exists so the user commits to a plan that already survived competition from rival approaches, not the first idea that came to mind.

Section purposes:
- 推薦方案: the synthesized plan to act on, up front.
- 候選評分: how each angle's plan scored, so the recommendation is transparent.
- 嫁接進來的改良: the good ideas pulled from losing plans, so nothing useful is wasted.
- 風險與前提: what could still break it, so the user goes in with eyes open.

格式：

## 推薦方案
（綜合後的方案，可直接行動。）

## 候選評分
### {角度名稱，如 MVP-first}
- 得分: {各標準的分數}
- 評語: {一句話：強在哪、弱在哪}

## 嫁接進來的改良
- {從某個落選方案拿來的具體點子，跟為什麼值得加}

## 風險與前提
- {這個方案仍然依賴的假設或可能失敗的點}
</output-format>

<guardrails>
- You orchestrate; the agents draft and judge. Do not write the plan yourself in the main conversation.
- The angle plans must optimize for genuinely different targets, not minor variations of one plan.
- Judges must score against the user's stated criteria, not generic preferences.
- Surface real disagreement between judges instead of averaging it away silently.
- Rest the recommendation only on facts the user provided or widely known public facts. Flag assumptions.
- Always set the token budget as a hard ceiling.
- Do not use markdown tables. Use bullet blocks.
- Output in Traditional Chinese, keeping angle names and technical terms in English.
</guardrails>
```





Claude Code 动态工作流：6 种质量模式与 3 条开箱即用的指令包

> （注：部分内容由豆包工作 AI 生成）
