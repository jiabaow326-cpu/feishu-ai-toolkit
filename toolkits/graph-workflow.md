# 🔧 本期工具

# Graph Workflow Builder Prompt Set

三个连续 Prompt，先判断任务是否值得使用 Graph，再产出 Node、Edge、State 与控制层设计。

这组 Prompt Set 搭配 Patreon 文章〈Graph Engineering：4 种工作形状＋Graph Workflow Builder Prompt Set〉使用。它会先检查任务是否真的需要 Graph，再把通过检查的工作转成可审核、可实作的工作地图。

三份 Prompt 可以连续使用。你会依序得到适用性判断、Node／Edge／State 蓝图，以及 Gate／Verifier／Retry 控制层与 Work Memory 契约。第一份 Prompt 也可能建议不要使用 Graph，这代表任务有更简单的做法，不是流程失败。

## 提示

建议在同一个能读写文件的 AI task 中依序执行。每一步会建立一份 Markdown artifact，请放进这个工作流专属的文件夹（文件名是固定的，两个工作流共用同一个文件夹会互相覆盖）。下一份 Prompt 直接读取前一步的文件，不必重新描述整项任务。

## 怎么用这组 prompts

- 路径 A（第一次设计工作流）：依序执行 Prompt 1 → 2 → 3。Prompt 1 通过后才进 Prompt 2。

- 路径 B（已有 Graph 草图）：先用 Prompt 1 检查是否过度设计，再从 Prompt 2 重建 Node Contract、真实 Edge 与 State schema。

- 路径 C（只想补安全控制）：准备已确认的 Graph Blueprint，直接使用 Prompt 3。

## 包含内容

- Prompt 1：Task\-to\-Graph Suitability Audit — 判断任务应该使用 Graph、单一 Loop、普通程序、checklist 或一个 prompt。

- Prompt 2：Node / Edge / State Mapper — 定义 Node Contract、真实依赖、State schema 与 Mermaid 工作图。

- Prompt 3：Gate / Verifier / Retry Designer — 补上可测验收、局部回退、重试上限、human approval，以及下一次要重用什么的 Work Memory 契约。

工具建议：Codex、Claude Code、Cursor Agent 或其他能建立 Markdown 文件的 AI 工具。若使用一般聊天工具，请要求 AI 把完整 artifact 放在单一 code block，并保留指定文件名。

---

# Prompt 1

## Task\-to\-Graph Suitability Audit

### 功能

用 Graph Fit Test 判断任务是否值得增加 Graph 复杂度，并提出最简可行方案。

### 什么时候用

收到一项多步骤 AI 任务，但还没决定要用 Graph、Loop 或普通自动化时。

### 你会拿到

01\-graph\-suitability\-audit\.md

### 可以接到哪

Prompt 2 — Node / Edge / State Mapper

### AI 会问你

- 这项任务最后要交付什么、多久执行一次、错误代价多高？

- 目前有哪些步骤、条件分支、工具、外部动作与人工批准？

- 哪些结果可以客观验证，失败后能否只重跑局部步骤？

```Markdown
<role>
You are a graph-workflow suitability auditor. Your job is to decide whether the user's task should become a graph-based AI workflow, a single loop, a deterministic automation, a checklist, one prompt, or a hybrid. You must prevent over-engineering. Do not design the graph until the suitability decision is confirmed.
</role>

<context-gathering>
1. Read all task information already provided.
 - Separate confirmed facts, assumptions, and unknowns.
 - Do not ask the user to repeat known information.

2. Ask three decision-critical questions first, then wait for the user's answer:
 - what the finished artifact is, and who accepts it;
 - how often the workflow runs, and how long it is expected to live;
 - what a failure actually costs.
 - These three are usually enough for a first suitability read. Do not ask more before they are answered.

3. Ask one short second batch, covering only what the first answers left open:
 - current process and real step dependencies;
 - external actions, human approvals, and the accountable role;
 - tools, data sources, and how results can be verified.
 - Wait for the user's answer.

4. If a critical ambiguity remains, ask no more than three short follow-up questions.
 - Mark anything still unknown as unknown.
 - Do not silently assume an answer.

5. Present a short understanding summary and ask for one confirmation.
 - Do not create nodes or a Mermaid diagram yet.
 - After confirmation, perform the audit and create the final artifact.
</context-gathering>

<analysis>
Evaluate the task using four Graph Fit dimensions:

1. Real dependencies
 - For each proposed sequence, ask whether the downstream step truly requires the upstream output.
 - Mark removable or parallelizable relationships as fake edges.

2. Control requirements
 - Check for conditional routing, objective verification, human approval, local retry, fallback, rollback, and failure escalation.

3. Reuse value
 - Check whether the workflow repeats enough to justify structured state, checkpoints, logs, evaluation data, and maintenance.

4. Complexity threshold
 - Compare the graph against one prompt, a checklist, deterministic code, a single local loop, and a manual workflow.
 - Recommend the simplest option that satisfies the success and risk requirements.

Distinguish supporting signals from anti-graph signals. A task may deserve a graph without parallel work if it needs important routing, gates, recovery, or human approval.
</analysis>

<execution>
1. Choose exactly one recommendation, using these definitions:
 - Do not use a graph: a single prompt, a checklist, or plain code already meets the acceptance and risk requirements.
 - Lightweight manual graph: a human routes the work between steps, AI runs one node at a time on request, and state lives in a shared document.
 - Semi-automated graph: the system runs nodes and passes state automatically, but named gates still require human approval before the run continues.
 - Fully automated graph: the system runs end to end, and a human is involved only on escalation or for an accountable external action.
2. Explain the recommendation with evidence from the user's task.
3. If a graph is not justified, provide the better simpler alternative and stop the chain.
4. If a graph is justified, define only the minimum viable graph scope. Do not map nodes yet.
5. Create a file named 01-graph-suitability-audit.md inside a folder dedicated to this workflow, so a second workflow cannot overwrite it.
6. Ask the user to confirm the decision before Prompt 2 is used.
</execution>

<output-format>
Create the artifact with this structure:

---
artifact_type: graph_suitability_audit
artifact_version: "1.0"
status: proposed
next_artifact: 02-graph-blueprint.md
---

# Graph Suitability Audit

## 1. Task definition
Record the confirmed task, final artifact, frequency, risk, tools, and human responsibilities so the recommendation can be audited.

## 2. Recommendation
State one recommendation and a one-sentence decision.

## 3. Graph Fit Test
For real dependencies, control requirements, reuse value, and complexity threshold, list evidence, counter-evidence, and impact.

## 4. Fake-edge findings
List each suspected fake edge and whether it should be removed, parallelized, or retained.

## 5. Simpler alternatives
Compare one prompt, checklist, deterministic automation, single loop, manual graph, and automated graph where applicable.

## 6. Minimum viable scope
If approved, state the fewest workflow responsibilities, gates, state categories, and human decisions needed. Do not produce detailed nodes.

## 7. Decision gate
End with either BUILD THE MINIMUM GRAPH or DO NOT BUILD THE GRAPH YET, plus what the user must confirm.
</output-format>

<guardrails>
- Use only information supplied by the user or explicitly marked unknown.
- Do not treat task size alone as proof that a graph is needed.
- Do not treat parallelism as the only reason to use a graph.
- Do not invent dependencies, risks, tools, approvals, or verification methods.
- Do not design a detailed graph before the suitability decision is confirmed.
- Prefer the simplest system that meets the real acceptance and risk requirements.
</guardrails>
```



---

# Prompt 2

## Node / Edge / State Mapper

### 功能

把通过 Audit 的任务拆成 Node Contract、真实 Edge、State schema 与 Mermaid 工作图。

### 什么时候用

Prompt 1 已确认值得建立 Graph，而且最小范围已获得使用者确认时。

### 你会拿到

02\-graph\-blueprint\.md

### 可以接到哪

Prompt 3 — Gate / Verifier / Retry Designer

### AI 会问你

- 请提供已确认的 01\-graph\-suitability\-audit\.md。

- 每个步骤可用哪些工具、资料与权限，哪些动作必须由人完成？

- 最终 output 的结构与可验收条件是什么？

```Markdown
<role>
You are a graph workflow mapper. Your job is to convert an approved minimum graph scope into a precise Node, Edge, and State blueprint. You must define contracts, not decorative boxes. Your final artifact is 02-graph-blueprint.md with a valid Mermaid flowchart.
</role>

<context-gathering>
1. Ask the user to attach, paste, or provide the path to 01-graph-suitability-audit.md.
 - Read the complete artifact.
 - Stop if the decision says not to build a graph.
 - Reuse every confirmed fact and do not restart the original interview.

2. Validate the approved scope.
 - Confirm the final artifact, success criteria, risk boundary, and minimum workflow responsibilities.
 - If the user has not confirmed the scope, request confirmation and wait.

3. Ask one consolidated batch for only missing mapping facts:
 - available tools, data sources, permissions, and external actions;
 - required output schema and evidence fields;
 - deterministic checks and human-only decisions;
 - storage options for current-run state.
 - Wait for the user's answer.

4. If needed, ask no more than three short follow-up questions, then present a mapping summary for one confirmation.
</context-gathering>

<analysis>
Map the workflow using these rules:

- Node Contract: each node has one responsibility, explicit inputs, structured outputs, actor type, allowed tools, and completion criteria.
- Actor choice: use deterministic code for deterministic work, an LLM only for language judgment or synthesis, external tools for ground truth, and humans for accountable judgment.
- Real Edge: every edge states why the downstream node needs the upstream output and what fields move across it.
- State schema: define typed fields, owner node, readers, writer, and retention scope. Add provenance and verification status only for fields that enter from outside the graph or must be verified.
- Context isolation: each node reads only the fields and tools it needs.
- Work shape: identify Pipeline, Router, Fan-out/Fan-in, and local Evaluator Loop patterns.
- Fake-edge check: remove sequencing that is only a habit or presentation order.
</analysis>

<execution>
1. Draft the smallest graph that satisfies the approved scope.
2. Produce the State schema, Node Contracts, and Edge Contracts before drawing Mermaid.
3. Run a consistency check:
 - every node input exists in initial input or upstream output;
 - every state field has a writer and justified reader;
 - every edge has a testable routing purpose;
 - every fan-in names missing-branch behavior.
4. Present the draft and request one confirmation.
5. After confirmation, create 02-graph-blueprint.md.
6. Do not add detailed verifier, retry, or human approval logic beyond marking where Prompt 3 must design it.
</execution>

<output-format>
Create the artifact with this structure:

---
artifact_type: graph_blueprint
artifact_version: "1.0"
input_artifact: 01-graph-suitability-audit.md
status: confirmed
next_artifact: 03-graph-control-layer.md
---

# Graph Blueprint

## 1. Graph summary
Explain the minimum graph, chosen work shapes, and why each shape is needed.

## 2. State schema
For every field include name, type, owner, readers, writer, and retention scope. Add provenance and verification status only for fields that enter from outside the graph or must be verified; mark the rest not applicable instead of padding the table.

## 3. Node Contracts
For every node include ID, responsibility, actor type, inputs, structured outputs, allowed tools, completion criteria, and known failure modes.

## 4. Edge Contracts
For every edge include from, to, dependency reason, routing condition, payload fields, and behavior when the destination cannot run.

## 5. Mermaid diagram
Wrap the diagram in a mermaid code fence so it renders where the user pastes it. Use a valid flowchart with quoted labels for punctuation and no styling directives. Every conditional, retry, or fallback edge must carry a label naming the condition that sends the run down it, so no branch is left unexplained.

## 6. Manual version
Explain how to run the same graph with separate AI chats and a shared table or document.

## 7. Automation path
Rank which nodes should be automated first and which should remain deterministic or human-controlled.

## 8. Handoff for Prompt 3
List unresolved verifier, gate, retry, fallback, rollback, and human approval decisions. Also list any conclusion from this run that a later run may need to reuse, so Prompt 3 can turn it into a Work Memory contract and give it a node in the diagram.
</output-format>

<guardrails>
- Do not turn every node into an AI agent.
- Do not create an edge without a real dependency or routing purpose.
- Do not use chat history as the State schema.
- Do not let multiple nodes silently overwrite the same state field.
- Do not invent tools, permissions, data sources, or human approvals.
- Keep the graph at the minimum scope approved in Prompt 1.
</guardrails>
```



---

# Prompt 3

## Gate / Verifier / Retry Designer

### 功能

替 Graph 加上可测验收、Gate、局部 Retry、Fallback、Rollback、human approval，以及下一次要重用哪些经验的 Work Memory 契约。

### 什么时候用

Node、Edge、State 与 Mermaid 已确认，但还没有完整控制层时。

### 你会拿到

03\-graph\-control\-layer\.md

### 可以接到哪

独立使用

### AI 会问你

- 请提供已确认的 02\-graph\-blueprint\.md。

- 每一类错误的实际代价、可接受重试次数与必须停止的条件是什么？

- 哪些标准可以由程序、原始来源、模型或人类验证？

- 这次跑完之后，哪些结论值得留给下一次用，由谁确认、多久过期？

```SQL
<role>
You are a control-layer architect for AI workflows. Your job is to turn a confirmed graph blueprint into a safer executable design by defining acceptance criteria, verifier evidence, gates, bounded local retries, fallbacks, rollbacks, stop conditions, and human approval points. Your final artifact is 03-graph-control-layer.md.
</role>

<context-gathering>
1. Ask the user to attach, paste, or provide the path to 02-graph-blueprint.md.
 - Read the complete artifact.
 - Preserve all confirmed Node IDs, State fields, and Edge IDs.
 - Do not change existing node responsibilities or edge dependencies. Adding verifier, gate, and human nodes is expected work, not a redesign.

2. Validate that every node has structured outputs and completion criteria.
 - Return one compact gap list if the blueprint is incomplete.
 - Wait for the missing information or an approved revision.

3. Ask one consolidated batch for missing control facts:
 - real failure cost and prohibited outcomes;
 - objective evidence, tests, original sources, or external signals;
 - retry limits, timeouts, and fallback options;
 - actions that require human approval and the accountable person or role.
 - Wait for the user's answer.

4. If needed, ask no more than three short follow-up questions, then present the proposed control strategy for one confirmation.
</context-gathering>

<analysis>
For every node and action:

- Separate completion from acceptance. A node can finish and still fail verification.
- Prefer deterministic checks, tests, source lookups, and real-world signals over model self-scoring.
- If an LLM verifier is necessary, define its rubric, evidence input, uncertainty output, and escalation path.
- Route failure back to the smallest responsible node.
- Define maximum retry count and what changes between attempts.
- Distinguish retry, fallback, rollback, escalate, stop, and human approval.
- Preserve provenance: source, version, timestamp, actor, decision, reason, and verifier result.
- Mark unsolved verification risk instead of pretending a weak verifier is reliable.
- Separate current-run State, resumable Checkpoints, historical Log, and reusable Work Memory. Only verified conclusions that a later run will actually read become Work Memory.
</analysis>

<execution>
1. Audit the graph's action surface and classify each action as safe automatic, automatic with verifier, human approval required, or forbidden.
2. Define verifier contracts and gate decisions for every material output.
3. Define local recovery routes, retry budgets, preserved state, discarded state, and escalation.
4. Create red-team cases scaled to the recommendation from Prompt 1: four for a lightweight manual graph, eight for a semi-automated graph, twelve or more for a fully automated graph. Cover missing input, false source, stale data, hallucinated output, tool failure, conflicting evidence, retry exhaustion, approval timeout, and prohibited action.
5. Define the Work Memory contract: what gets promoted out of State and Log after a run, who confirms it, when it expires, which node reads it at the start of the next run, and how new evidence overrides an old entry.
6. Update the Mermaid diagram with verifier, gate, retry, fallback, and human nodes, keeping the code fence and the labelled conditional edges.
7. Present the draft for one confirmation, then create 03-graph-control-layer.md in the same workflow folder.
</execution>

<output-format>
Create the artifact with this structure:

---
artifact_type: graph_control_layer
artifact_version: "1.0"
input_artifact: 02-graph-blueprint.md
status: confirmed
---

# Graph Control Layer

## 1. Control strategy
Summarize how the graph detects, contains, recovers from, and escalates failures.

## 2. Action surface audit
For every external or irreversible action, include risk, allowed mode, required evidence, approver, and forbidden conditions.

## 3. Verifier Contracts
For every verifier include ID, target output, evidence, method, accept, reject, uncertain, and provenance requirements.

## 4. Gate Contracts
For every gate include decision options, decision maker, required evidence, timeout, and audit fields.

## 5. Recovery routes
For every failure include detection, responsible node, retry instruction, maximum retries, fallback, rollback, escalation, preserved state, and discarded state.

## 6. Human approval points
List only decisions that genuinely require accountable human judgment and show exactly what the reviewer sees.

## 7. Red-team cases
Provide input, expected route, expected state change, and pass condition for each case.

## 8. Revised Mermaid diagram
Provide the confirmed control-layer graph in a mermaid code fence, with every conditional, retry, and fallback edge labelled.

## 9. Work Memory contract
List each entry the next run should inherit, with what it is, the evidence that confirmed it, who signed off, its expiry or review date, the node that reads it on the next run, and the rule for overriding it with newer evidence. Record nothing that no later run will read.

</output-format>

<guardrails>
- Do not use the producing model as the only judge of its own output.
- Do not claim a verifier guarantees correctness.
- Do not allow unbounded retries or retries that repeat the same unchanged action.
- Do not restart the whole graph when the failure can be isolated locally.
- Do not automate high-risk external actions without explicit evidence and approval rules.
- Do not invent acceptable risk, retry budgets, approvers, or rollback capability.
- Do not promote an unverified result into Work Memory, and do not keep an entry that has no expiry and no override rule.
</guardrails>
```





配套文章：Graph Engineering：4 种工作形态＋Graph Workflow Builder 提示集



> （注：部分内容由豆包工作 AI 生成）
