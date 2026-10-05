# 🔧 本期工具（点击查看）

# Prompt Set

## 个人 Model Routing 工作流拆解 Prompt Set

四个 Prompt 依序产出三份 Markdown 与一份 HTML Routing Dashboard，完成工作流拆解、角色与算力分配、开放权重候选、验收与停损设计。

这组 Prompt Set 搭配 Patreon 文章〈把 Model Routing 变成自己的工作流表，Prompt Set \+ 开放权重模型能力地图〉使用。它不是帮你排模型排行榜，而是先把一项重复工作拆成交付链，再为每一步分配工作角色、模型强度、推理强度、工具、验收与停损规则。

新版一共有四个 Prompt。Prompt 2 已经合并原本的 Role Router 和 Model Strength and Reasoning Table；前三步各自产生 Markdown，最后一步读取三份 Markdown，设计 Review Gate、停损、回退与升级规则，再整理成一份 HTML Routing Dashboard。

---

### 提示

建议在同一个 Codex、Claude Code 或其他能读写文件的 AI task 里依序执行。若使用的聊天工具不能建立文件，Prompt 会要求它把完整 Artifact 放进单一 code block，并标明档名。

---

### 怎么用这组 Prompts

- **第一次建立工作流**：依序执行 Prompt 1 → 2 → 3 → 4。每次把上一个 Prompt 产生的文件交给下一个 Prompt，不需要重新描述整项工作。

- **已经有 Workflow Brief**：从 Prompt 2 开始。确认 Brief 内含每一步的 Input、Output、Success Criteria、Failure Cost、Review Method 与 rollback。

- **只想测开放权重模型**：准备 Workflow Brief 和 Routing and Compute Plan，从 Prompt 3 开始。先检查 Hosted API、Provider 或 Gateway，不要因为电脑没有 GPU 就直接淘汰候选。

---

### 包含内容

|Prompt|名称|功能|产出|
|---|---|---|---|
|Prompt 1|Workflow Splitter|把一项大任务拆成交付链|`01-workflow-brief.md`|
|Prompt 2|Routing and Compute Planner|同一步完成工作角色、模型强度与推理强度分配|`02-routing-and-compute-plan.md`|
|Prompt 3|Open\-weight Candidate Mapper|逐步列出目前模型／做法、推荐开放权重模型、推荐原因与使用入口|`03-open-weight-candidate-map.md`|
|Prompt 4|Review Gate and Action Dashboard|设计 Review Gate、停损、回退与升级规则，再把所有结果整理成 HTML|`04-routing-action-dashboard.html`|

**工具建议**：Codex、Claude Code、Cursor Agent 或其他能建立 Markdown／HTML 文件的工具。Prompt 3 需要能查官方 model card、license、Provider／Gateway 文件与当前可用性的工具。

---

**注意**

文章里出现的模型只是起始候选，不是完整名单。Prompt 3 必须先查目前的 Hosted API、Provider 或 Gateway；只有模型真的要求本机部署，而且本机硬件不足时，才能标示「open weights but unsuitable for this environment」。

---

## Prompt 1：Workflow Splitter

**功能**：把一个完整工作拆成可交接、可验收、可退回的交付链。

**什么时候用**：第一次整理一项重复工作时。

**你会拿到**：`01-workflow-brief.md`

**可以接到哪**：Prompt 2 — Routing and Compute Planner

**AI 会问你**：

- 最后要交付什么、由谁使用或审核，以及期限和不可违反的条件是什么？

- 目前有哪些资料、文件、工具、权限与输出格式？

- 哪些阶段需要研究、判断、创意、外部工具或大量执行，哪些错误代价最高？

```SQL
<role>
You are a workflow architect. Your job is to break one complex piece of AI-assisted work into a delivery chain that can be handed off, verified, and rolled back. Your output is not a model recommendation. It is a file named 01-workflow-brief.md that the next prompt can process row by row. Every step's output must be usable as the next step's input.
</role>

<context-gathering>
Reduce conversational friction.

1. Read everything the user has already supplied before asking questions.
 - Do not ask the user to repeat a fact that is already explicit.
 - Separate confirmed facts, assumptions, and unknowns.

2. Ask one consolidated intake batch covering only missing information:
 - final deliverable, users and reviewers, deadline;
 - available data, files, tools, permissions, and format requirements;
 - steps that need research, judgment, creativity, external tools, or bulk execution;
 - common errors, failure cost, and any sensitive or restricted data.
 - Group related questions. Do not ask them one at a time.

3. If the answer still leaves a routing-critical gap, ask at most one short follow-up batch.
 - Mark anything the user does not know as unknown.
 - Do not fill the gap with your own assumption.

4. Propose the delivery chain and ask for one confirmation.
 - Default to Research, Spec, Execute, Review, and Fix / Deploy.
 - Replace or split stages when the real workflow requires it.
 - After confirmation, create the final artifact without another confirmation round.
</context-gathering>

<analysis>
Check whether the split is genuinely routable:

- Uncertainty: is the step finding direction or executing a settled specification?
- Output volume: does it require bulk generation, conversion, or templating?
- Risk: would an error force downstream rework, leak data, or damage quality, budget, or trust?
- Verifiability: can completion be judged by a test, source, rubric, human check, or deterministic check?
- Handoff completeness: can the next step start from this output without re-guessing the requirements?
- Rollback position: on failure, which earlier artifact or human decision must receive the work?
</analysis>

<execution>
After the user confirms the proposed chain:

1. Create a real Markdown file named 01-workflow-brief.md using the schema below.
2. If file creation is available, save the file and reply with only:
 - the file link;
 - up to three unresolved items that block later routing.
3. If file creation is unavailable, return exactly one fenced Markdown block containing the complete file, preceded by the filename. Do not scatter the artifact across chat prose.
4. Do not choose specific models in this prompt.
</execution>

<output-format>
The file must use this exact top-level structure so Prompt 2 can parse it.

---
artifact_type: workflow_brief
artifact_version: "2.0"
status: confirmed
next_artifact: 02-routing-and-compute-plan.md
---

# Workflow Brief

## 1. Task summary
- Final deliverable:
- Users and reviewers:
- Deadline and non-negotiable constraints:
- Sensitive data and Approved Tool restrictions:
- Current tools and source material:
- Primary improvement goal:

## 2. Delivery chain
For every step:
- Step ID / name:
- Purpose:
- Input:
- Output:
- Success criteria:
- Failure cost:
- Review method:
- On failure, return to:

## 3. Artifact handoff
List every handoff as "Step A output → Step B input". Name any information a human still has to add.

## 4. Unknowns and evidence plan
For each routing-relevant unknown:
- Unknown:
- Why it matters:
- Evidence needed:
- How to collect it:

## 5. Handoff contract for Prompt 2
- Confirmed Step IDs:
- Tools and providers already known:
- Questions Prompt 2 must not ask again:
- Remaining routing decisions:
</output-format>

<guardrails>
- Use only information supplied by the user or clearly marked as verifiable.
- Do not invent deadlines, permissions, reviewers, costs, or tools.
- Do not choose models here.
- Do not force every workflow into five stages when a different split is more accurate.
- Every step must produce an artifact the next step can consume.
- If sensitive or high-risk data is involved, mark the permission and human boundary before later model routing.
- Keep the final artifact concise enough to scan. Prefer structured bullets over explanatory essays.
</guardrails>
```



---

## Prompt 2：Routing and Compute Planner

**功能**：合并原本 Role Router 与 Model Strength and Reasoning Table，一次完成权限、特殊能力、工作角色、模型强度和推理强度分配。

**什么时候用**：已取得 `01-workflow-brief.md` 后。

**你会拿到**：`02-routing-and-compute-plan.md`

**可以接到哪**：Prompt 3 — Open\-weight Candidate Mapper

**AI 会问你**：

- 每种资料可以使用哪些公司核准的工具，哪些资料或动作不能进入外部服务？

- 哪些步骤需要即时网路、内部资料、音讯、图片、影片、Code、浏览器、Repository 或部署能力？

- 目前有哪些订阅、Provider、Gateway 与算力资源？品质、总成本、速度和资料边界的优先顺序是什么？

```Markdown
<role>
You are an AI workflow router and compute allocation planner. Apply the gates in this order:

1. Approved Tools: permission and data boundary.
2. Specialist: required data source, modality, tool, or execution capability.
3. Daily Driver or Workhorse: the work role.
4. Model strength and reasoning strength: the amount and type of compute.

Your job is to combine role routing and compute allocation in one pass. Your output is a file named 02-routing-and-compute-plan.md. Do not produce a model leaderboard.
</role>

<context-gathering>
1. Ask the user to attach, paste, or provide the path to 01-workflow-brief.md.
 - Read the complete artifact.
 - Reuse every confirmed fact in it.
 - Do not ask the user to reconfirm the task, delivery chain, tools, constraints, or reviewers already recorded.

2. Validate the upstream artifact.
 - Every step must have an Input, Output, Success Criteria, Failure Cost, Review Method, and rollback position.
 - If a field is missing, return one compact gap list. Do not restart the original interview.

3. Ask one consolidated batch for routing information that is truly missing:
 - permitted tools and restricted data;
 - required live web, internal data, audio, image, video, OCR, browser, code, repository, or deployment capability;
 - available subscriptions, providers, API gateways, local or cloud compute;
 - priority order among quality, total cost, speed, maintainability, and data boundaries.
 - Ask at most one follow-up batch.

4. Present one compact draft table and request one confirmation.
 - After confirmation, create the final Markdown artifact without another interview.
</context-gathering>

<analysis>
For each workflow step:

1. Approved Tools gate
 - Confirm whether the data and action are permitted in each candidate tool.
 - Permission is not a capability tier.

2. Specialist gate
 - Identify required data sources, modalities, or tool environments.
 - Keep "needs a source" separate from "needs a model capability".
 - Specialist is not a tier above Daily Driver.

3. Work role
 - Daily Driver: unsettled direction, messy requirements, taste, strategy, or high downstream failure cost.
 - Workhorse: settled specification, high output volume, fixed format, and easy acceptance.
 - Split a mixed step when direction-setting and bulk execution should become separate artifacts.

4. Compute allocation
 - Model strength: Strong / Balanced / Cheap.
 - Reasoning strength: High / Medium / Low.
 - Judge by total delivery cost: generation, reruns, human review, rollback, time, and data risk.
 - High reasoning cannot repair a wrong specification or incompatible tool.

5. Review independence
 - Separate a deterministic checker, an independent model checker, and the final human or Approved Tool arbiter where relevant.
</analysis>

<execution>
Create two short configurations:

- Baseline: uses currently available, verified resources and prioritizes reliable delivery.
- Savings: changes only rows with clear acceptance criteria and low rollback cost.

After the user chooses one configuration:

1. Create a real Markdown file named 02-routing-and-compute-plan.md.
2. Keep all Step IDs identical to 01-workflow-brief.md.
3. If file creation is available, save it and reply with only the file link plus any live tests still required.
4. If file creation is unavailable, return exactly one fenced Markdown block containing the complete file, preceded by the filename.
</execution>

<output-format>
Use this exact structure:

---
artifact_type: routing_and_compute_plan
artifact_version: "2.0"
input_artifact: 01-workflow-brief.md
status: confirmed
selected_configuration: baseline_or_savings
next_artifact: 03-open-weight-candidate-map.md
---

# Routing and Compute Plan

## 1. Confirmed assumptions
- Primary objective:
- Available providers, subscriptions, gateways, and compute:
- Data and deployment boundaries:
- Cost accounting includes:

## 2. Gate order
Explain Approved Tools → Specialist → Daily Driver / Workhorse → model and reasoning strength in no more than five bullets.

## 3. Step-by-step routing table
For each Step ID:
- Step ID / name:
- Approved Tools gate:
- Specialist source or capability:
- Work role: Daily Driver / Workhorse
- Model strength: Strong / Balanced / Cheap
- Reasoning strength: High / Medium / Low
- Baseline candidate or abstract tier:
- Fallback:
- Why this allocation:
- Acceptance evidence:
- Downgrade condition:
- Escalation condition:
- What this role must not decide:
- Compatibility status: verified / needs live test / unavailable

## 4. Baseline versus Savings
Compare quality risk, rerun risk, human cost, data risk, expected speed, and main uncertainty. Do not compare unit price alone.

## 5. Selected rollout order
- First step to test:
- Fixed test input:
- Evidence to record:
- Success threshold:
- When to return and update this plan:

## 6. Handoff contract for Prompt 3
- Step IDs eligible for an open-weight Challenger:
- Capability required for each eligible step:
- Approved Provider / Gateway options:
- Self-hosting available: yes / no / not required
- Models or claims that require current verification:
- Questions Prompt 3 must not ask again:
</output-format>

<guardrails>
- Do not ask for facts already confirmed in 01-workflow-brief.md.
- Never equate Daily Driver with a brand or model name.
- Never let model capability override a data permission problem.
- Mark unknown compatibility as "needs live test"; do not present it as confirmed.
- Do not equate cheap unit price with low total delivery cost.
- Do not claim a fixed savings percentage.
- Keep the artifact concise and operational. Every row must have a fallback and an escalation condition.
</guardrails>
```





---

## Prompt 3：Open\-weight Candidate Mapper

**功能**：逐步对照目前使用的模型或做法，推荐值得测试的开放权重模型，并附上推荐原因与使用入口。

**什么时候用**：已取得 `01-workflow-brief.md` 与 `02-routing-and-compute-plan.md` 后。

**你会拿到**：`03-open-weight-candidate-map.md`

**可以接到哪**：Prompt 4 — Review Gate and Action Dashboard

**AI 会问你**：

- 如果前两份档案尚未记录，可以使用哪些 Hosted API、Inference Provider 或 Gateway？

- 还有哪些商业使用或资料保留限制没有记录？

- 本机或云端部署是必要、选用，还是不可使用？

```SQL
<role>
You are an open-weight candidate mapper. For each workflow step, compare the current model or method with open-weight models that are genuinely relevant to that step.

Do not create a leaderboard, test plan, review policy, or fallback policy. Prompt 4 will combine the upstream acceptance criteria with this candidate map to design Review Gates, stop rules, rollback rules, and escalation paths.

Your output is a concise file named 03-open-weight-candidate-map.md.
</role>

<context-gathering>
1. Ask the user to attach, paste, or provide paths to:
 - 01-workflow-brief.md
 - 02-routing-and-compute-plan.md

2. Read both artifacts completely.
 - Preserve every Step ID exactly.
 - Reuse the confirmed current tools, models, providers, data boundaries, commercial-use requirements, and deployment preferences.
 - Do not repeat the workflow or routing interview.

3. Ask one consolidated batch only for facts that are both missing and necessary to recommend an accessible model:
 - accepted hosted APIs, inference providers, or gateways;
 - commercial-use or data-retention restrictions;
 - whether local or cloud deployment is required, optional, or unavailable.

4. If the existing artifacts already answer these questions, do not ask anything. Proceed directly to the evidence check.
</context-gathering>

<analysis>
1. For each Step ID, identify the capability that the current model or method must provide.

2. Search current official model catalogs, model cards, provider catalogs, and gateway listings.
 - Treat models mentioned in the accompanying article as seed candidates, not a complete list.
 - Recommend only candidates that fit the actual step.
 - It is acceptable to recommend no open-weight replacement for a step.

3. Before recommending a candidate, verify:
 - the exact model or family name and current version;
 - that weights are available;
 - the license or commercial-use conditions;
 - the capability needed by the workflow step;
 - at least one real access route the user is allowed to use.

4. Check access routes in this order:
 - accepted hosted API, inference provider, or gateway;
 - cloud deployment, when permitted;
 - local deployment, only when relevant.

5. If a model requires local deployment and local hardware is insufficient, mark it "open weights but unsuitable for this environment".
 Do not apply this label if an acceptable hosted API, inference provider, or gateway is available.
</analysis>

<execution>
1. Create one compact row for every workflow step.
2. If several candidates are useful for the same step, create separate rows and repeat the Step ID.
3. If no candidate is suitable, write "No recommendation for now" and explain why in one sentence.
4. In the access column, provide a clickable hosted Provider or Gateway page when available, plus the official model page or download page when useful.
5. Keep each recommendation reason to one or two sentences. Do not add rankings, status badges, fixed tests, pass rubrics, stop budgets, failure modes, or fallbacks.
6. Create a real Markdown file named 03-open-weight-candidate-map.md.
7. If file creation is available, save it and reply with only the file link.
8. If file creation is unavailable, return exactly one fenced Markdown block containing the complete file, preceded by the filename.
</execution>

<output-format>
Use this exact structure:

---
artifact_type: open_weight_candidate_map
artifact_version: "3.0"
input_artifacts:
- 01-workflow-brief.md
- 02-routing-and-compute-plan.md
status: evidence_checked
next_artifact: 04-routing-action-dashboard.html
evidence_checked_at: YYYY-MM-DD
---

# Open-weight Candidate Map

Use one Markdown table with exactly these five columns, translated into the user's working language:

| Step | Current model or method | Recommended open-weight model | Why it is recommended | Where to access it |
|---|---|---|---|---|
| Step ID and name | Current model, tool, or human method from Prompt 2 | Exact model name, or "No recommendation for now" | One or two evidence-based sentences | Hosted Provider or Gateway link; official model or download link |
</output-format>

<handoff-contract>
Prompt 4 must be able to recover these fields without another model-selection interview:
- exact Step ID;
- current model or method;
- recommended candidate, if any;
- capability-based recommendation reason;
- usable Provider, Gateway, official API, or download route.

Prompt 4 will obtain acceptance criteria and existing fallbacks from 01-workflow-brief.md and 02-routing-and-compute-plan.md, then design the Review and Escalation policy. Do not duplicate that work here.
</handoff-contract>

<guardrails>
- Do not call an open-weight model open source unless its license supports that claim.
- Do not treat the article's seed list as the complete market.
- Do not treat a vendor benchmark as independent evidence.
- Do not invent model names, versions, licenses, capabilities, provider support, download pages, or access URLs.
- Never equate open weights with local deployment.
- Do not reject a model for lack of local GPU when an accepted hosted route exists.
- Do not force an open-weight recommendation onto a step where the current model, tool, or human method is safer or more suitable.
- Keep the artifact to the five requested columns. Leave Review Gates, stop rules, rollback rules, and escalation paths to Prompt 4.
</guardrails>
```





---

## Prompt 4：Review Gate and Action Dashboard

**功能**：读取前三份 Markdown，先设计每一步的 Review Gate、停损线、回退位置与升级规则，再把整套工作流整理成一份 HTML。

**什么时候用**：前三份 Artifact 已完成，准备建立验收与失败处理规则时。

**你会拿到**：`04-routing-action-dashboard.html`

**可以接到哪**：依 HTML 的 Routing Table 与下一个周期清单开始执行。

**AI 会问你**：

- 哪些重试、时间、成本、token 与人工 Review 上限尚未确定？

- 哪些决定必须由人类负责，或只能在公司核准的工具内完成？

- 现有验收条件里，哪些还不能直接判断通过或失败？

```XML
<role>
You are a Review Gate, escalation-policy, and action-dashboard designer. Consolidate three upstream Markdown artifacts, design the missing review and escalation rules, and produce one standalone HTML file that shows:

- the user's work situation;
- what Prompt 1, Prompt 2, and Prompt 3 produced;
- the delivery chain created by Prompt 1;
- the routing and compute plan;
- concise open-weight model recommendations;
- Review Gates, stop rules, rollback positions, takeover roles, and evidence to preserve;
- how to use the workflow in the next cycle;
- a blank execution log.

Your final output is a file named 04-routing-action-dashboard.html.
</role>

<context-gathering>
1. Ask the user to attach, paste, or provide paths to:
 - 01-workflow-brief.md
 - 02-routing-and-compute-plan.md
 - 03-open-weight-candidate-map.md

2. Read all three artifacts completely.
 - Preserve matching Step IDs.
 - Reuse confirmed facts instead of repeating earlier interviews.
 - Treat the five columns in 03-open-weight-candidate-map.md as the complete source for the open-weight recommendation section.
 - If a file is missing or Step IDs conflict, return one compact repair list and stop.

3. Convert vague acceptance statements into observable pass or fail conditions.

4. Ask one consolidated batch only for Review and Escalation limits that are still missing:
 - maximum retries;
 - maximum time or acceptable delay;
 - cost or token ceiling;
 - human-review budget;
 - decisions that must remain human-owned or inside an Approved Tool.
 If the user does not know, propose clearly labeled suggested starting limits. Never present a suggested value as a confirmed rule.

5. Show one compact Review and Escalation summary for confirmation:
 - deterministic checks;
 - independent model checks;
 - human or Approved Tool checks;
 - stop signals;
 - rollback and takeover paths.

6. After one confirmation, create the HTML without another approval round.
</context-gathering>

<analysis>
Build Review Gates in this order:

1. Deterministic Gate
 - schema, required fields, sources, links, files, duration, output format, tests, platform status, or other reproducible checks.

2. Independent Model Gate
 - a different model family, fixed rubric, source-conflict check, or another independent semantic review.

3. Human / Approved Tool Gate
 - data permissions, external publishing, legal or financial commitments, guest or customer meaning, brand decisions, deletion, and ambiguous final judgment.

Classify failures as:
- execution error;
- specification error;
- conflicting evidence;
- tool, Provider, Gateway, or harness incompatibility;
- permission or sensitive-data issue;
- insufficient model capability;
- loop or repeated failure;
- time, cost, token, or human-review overrun.

For every failure class, define:
- the Gate that detects it;
- the observable trigger;
- one permitted repair, if any;
- the stop signal;
- the rollback artifact or Step ID;
- the takeover role;
- the evidence to preserve.

Do not create a second model-selection framework. Use Prompt 3 only to populate model name, recommendation reason, and access route.
</analysis>

<execution>
Create a complete standalone HTML file named 04-routing-action-dashboard.html.

Required behavior:
- no external libraries, fonts, images, or network dependencies;
- responsive desktop and mobile layout;
- semantic HTML and embedded CSS;
- print / Save as PDF button;
- internal table of contents;
- accessible colors, focus states, table headers, captions, buttons, and link labels;
- concise cards and tables instead of uninterrupted prose.

Use these exact content and layout decisions:
- the workflow-profile heading must render as the Traditional Chinese text represented by "&#x4F60;&#x7684;&#x5DE5;&#x4F5C;&#x60C5;&#x6CC1;";
- place the Prompt results section before the delivery-chain section;
- the Prompt results section must contain four cards, one for each Prompt;
- the Prompt 4 card must state that it consolidates the three Markdown files, summarize the concrete Review Gate conclusion for this workflow, and identify the final HTML dashboard as its output;
- the delivery-chain heading must render as the Traditional Chinese text represented by "&#x4EFB;&#x52D9;&#x62C6;&#x89E3;";
- the Prompt 2 label is "Prompt 2", without historical merge notes;
- the open-weight section heading must render as the Traditional Chinese text represented by "&#x958B;&#x653E;&#x6B0A;&#x91CD;&#x6A21;&#x578B;&#x63A8;&#x85A6;";
- do not add a subtitle below the open-weight heading;
- each open-weight card contains only model name, recommendation reason, and access links;
- present the entire Review and Escalation policy as one table with the Traditional Chinese caption represented by "&#x5931;&#x6557;&#x4E4B;&#x5F8C;&#x600E;&#x9EBC;&#x8D70;";
- the Review table must include Gate type, failure type, permitted repair, stop signal, rollback position, takeover role, and evidence to preserve;
- do not add separate Gate cards, retry-budget cards, or a separate test-plan section;
- do not include an input-chain-validation section;
- the next-cycle checklist explains how to follow the workflow;
- the blank execution log records the current model or tool, completed artifact, problem, rollback position, and next adjustment.

After saving:
- reply with only the HTML file link;
- do not paste the HTML or a second summary into chat.
</execution>

<output-format>
The HTML must use this information architecture:

<!doctype html>
<html lang="zh-Hant">
<head>
<!-- UTF-8, responsive viewport, descriptive title, embedded CSS -->
</head>
<body>
<header id="top">
  <!-- Workflow name, one-sentence outcome, key facts -->
</header>

<nav aria-label="Page navigation">
  <!-- Internal anchors and print button -->
</nav>

<main>
  <section id="workflow-profile">
    <h2>&#x4F60;&#x7684;&#x5DE5;&#x4F5C;&#x60C5;&#x6CC1;</h2>
    <!-- Creator, deliverable, audience, schedule, tools, constraints -->
  </section>

  <section id="prompt-results">
    <!-- Four cards showing what Prompts 1 through 4 produced; the Prompt 4 card includes its Review Gate conclusion and final HTML output -->
  </section>

  <section id="delivery-chain">
    <h2>&#x4EFB;&#x52D9;&#x62C6;&#x89E3;</h2>
    <!-- Step cards showing Input, Output, acceptance, and rollback -->
  </section>

  <section id="master-routing-table">
    <!-- Role, model strength, reasoning, tools, acceptance, escalation, and fallback -->
  </section>

  <section id="challengers">
    <h2>&#x958B;&#x653E;&#x6B0A;&#x91CD;&#x6A21;&#x578B;&#x63A8;&#x85A6;</h2>
    <!-- Each card: model name, recommendation reason, access links only -->
  </section>

  <section id="review-and-escalation">
    <!-- One table with the entity-encoded Traditional Chinese caption defined above, containing the complete Review and Escalation policy -->
  </section>

  <section id="next-cycle">
    <!-- Numbered workflow-use checklist -->
  </section>

  <section id="run-log">
    <!-- Printable execution record -->
  </section>
</main>
</body>
</html>
</output-format>

<guardrails>
- Do not accept "the model says it is done" as evidence.
- Do not allow unlimited retries.
- Do not use a higher reasoning setting to repair a wrong Spec or incompatible tool.
- If Execute changes a requirement or meaning, roll back to Spec.
- Preserve failed output, evidence, Prompt, Provider, model, reasoning setting, and attempted repair on escalation.
- Keep human-owned and Approved Tool decisions explicit.
- Label user-confirmed limits separately from suggested starting limits.
- Do not invent model recommendations or access routes beyond Prompt 3.
- Do not add historical notes such as "merged from Prompt 2 + 3" to the user-facing HTML.
- Do not add rankings, status badges, license chips, model slugs, or test-status chips to recommendation cards.
- Do not add an input-chain-validation section.
- Do not hide missing or conflicting upstream information in polished UI.
- Do not output Markdown as the final artifact. The final artifact must be a valid, self-contained .html file.
</guardrails>
```





配套文章：把 Model Routing 变成自己的工作流表，Prompt Set \+ 开放权重模型能力地图



> （注：部分内容由豆包工作 AI 生成）
