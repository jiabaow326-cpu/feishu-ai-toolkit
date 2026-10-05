# 🔧 本期工具

# Cross\-Model Review Kit

一段 install prompt，让 Claude 自动把 cross\-model review 的 stop hook 和 codex review skill 装进你的 Claude Code。

这是〈让 Claude 跟 Codex 自动互审〉这篇文章配套的安装包。它把文章里那套 cross\-model review，从零装进你的 Claude Code：每次你写完一份 implementation plan，Claude 会被强制先跟 Codex 逐轮 review 到两边有共识，才能结束这一轮。

主角是下面这段 install prompt。你把它贴进 Claude Code，它会先问你四个问题，然后自己把 stop hook、settings\.json 的注册、还有 codex review skill 全部装好，对齐到你的路径，再验证一次。你只要回答问题就好。

## 重要

开始之前你需要：已经装好 Claude Code、装好并登录 codex CLI（版本要支持 codex exec / \-\-json / resume）、以及本机有 Python 3。codex 的 reviewer 配置（model、reasoning effort 等）install prompt 会帮你写进 \~/\.codex/config\.toml（注意这是全局 codex 配置，会影响你所有 codex 用途，不只 review；安装时它会先跟你说明、有冲突先询问）。superpowers 框架是选配，有的话默认路径开箱即用，没有的话安装时会问你 plan 放在哪里。

## 一键安装

复制下面这段 prompt，贴进 Claude Code 直接发送。它会先问你四件事，然后把整套装好、验证一次。

**Prompt 1**

### 一键安装 Prompt

**功能：**

把 cross\-model review 的 stop hook、settings\.json 注册、跟 codex review skill 一次装进你的 Claude Code，并对齐到你的路径。

**什么时候用：**

你已经有 Claude Code 跟 codex CLI，想让每一份 plan 在定稿前自动被 Codex review。

**你会拿到：**

装好且通过验证的 stop hook、已并入的 settings\.json、就位的 codex\-peer\-review skill，以及一份它做了什么的报告。

**可以接到哪：**

无（一次性安装，装完即结束）

**AI 会问你：**

- codex CLI 装好、登录了吗（过不了 smoke test 会停下来带你修；reviewer 的 model / reasoning 配置它会帮你写好）

- 你用 superpowers 框架吗（决定默认监控哪些文件夹）

- 装在全局 \~/\.claude 还是只装这个项目 \.claude

- 你的 plan / spec 放在哪个文件夹

```SQL
<role>
You are setting up a "cross-model review" harness inside my Claude Code. Once installed, every time I finish writing an implementation plan or spec, you (Claude) must peer-review it with Codex before the turn can end, looping until both models reach consensus. The harness has two parts: a Stop hook that acts as a gate, and a codex-peer-review skill that runs the actual review. Install both, wired to my setup.
</role>

<context-gathering>
Work through this in order. Do not write any files until everything below is answered and confirmed.

1. Pre-check the prerequisite first, because the whole harness depends on a working codex CLI. Run "codex --version" (it must be recent enough to support codex exec, --json, and resume by session id). Then run a tiny smoke test to prove codex actually responds and is logged in: printf 'Reply with exactly: OK' | codex exec --sandbox read-only - and confirm it returns without error. If codex is not installed, not logged in (fix with codex login), or too old, STOP here and walk me through fixing it. Do not continue the install on a broken reviewer.

2. Once codex is confirmed, ask me these three setup questions and wait for my answers:
 a. Do you use the superpowers skill framework? If yes, the hook will watch docs/superpowers/specs/ and docs/superpowers/plans/ by default.
 b. Install globally (~/.claude, every project) or for this project only (.claude in the current repo)?
 c. Which folder(s) hold the plans/specs you want reviewed? Default for superpowers users: docs/superpowers/specs/ and docs/superpowers/plans/.

3. Echo back the install location and the watched path(s) you understood, and wait for my confirmation before writing anything.
</context-gathering>

<execution>
Pick the base dir from my answers: ~/.claude for global, or .claude in the current repo for project-only. Then:

1. Set up the reviewer's codex config. The skill calls codex with no -m flag and reads the model and reasoning from ~/.codex/config.toml, so these values are what make the review identical:
 model = "gpt-5.5"
 service_tier = "fast"
 model_reasoning_effort = "xhigh"
 model_context_window = 1000000
 Before you change anything, tell me this plainly: these are GLOBAL codex settings, so setting model = "gpt-5.5" changes the model for ALL my codex usage, not only these reviews. If ~/.codex/config.toml already sets a different model, show me the current value and ask whether to overwrite it before you do. If I do not have access to gpt-5.5, set model to the strongest reasoning model I can use instead, and note that review quality depends on it. MERGE these keys in, preserving every other setting and every [section] already there.

2. Download the Stop hook into <base>/hooks/codex-review-gate.py:
 curl -fsSL https://garytalksstuff.com/kits/codex-review-gate.py -o <base>/hooks/codex-review-gate.py
 If the download fails, tell me and I will paste the source from the kit page so you can write it instead.

3. In codex-review-gate.py, set WATCHED_DIR_SUBSTRS to the folder(s) I gave you, keeping trailing slashes, for example ("docs/superpowers/specs/", "docs/superpowers/plans/").

4. Register the hook in <base>/settings.json:
 - Back up the file first. If it is not valid JSON, stop and tell me.
 - Add to hooks.Stop, MERGING with any existing Stop hooks, never overwriting them:
   { "matcher": "", "hooks": [ { "type": "command", "command": "python3 <base>/hooks/codex-review-gate.py" } ] }

5. Download and unpack the skill:
 curl -fsSL https://garytalksstuff.com/kits/codex-peer-review.zip -o /tmp/codex-peer-review.zip
 Unzip it into <base>/skills so the result is <base>/skills/codex-peer-review/SKILL.md.

6. Align paths: make the watched-path references inside the skill's SKILL.md match the folder(s) you set in step 3, so the hook and skill agree.

7. Verify: create a throwaway one-line plan with no review marker under one watched folder, then try to end the turn. Confirm the hook blocks and asks for review. Then delete the throwaway file. (Or paste the separate verification prompt from the kit page, which dry-runs the gate without calling Codex.)

8. Report every file you created or edited, the watched paths you set, and exactly how I can test it myself.
</execution>

<guardrails>
- Back up settings.json before touching it. Never clobber an existing hook; merge into the Stop array.
- If the codex CLI is missing, not logged in, or fails the smoke test, stop and give me fix steps. Do not proceed with a broken reviewer.
- When editing ~/.codex/config.toml, merge the reviewer keys in. Never delete or overwrite my other codex settings, marketplaces, or MCP servers.
- Keep the hook's WATCHED_DIR_SUBSTRS and the skill's path references identical. If they drift, the marker handshake breaks and reviews stop triggering.
- Do not invent paths or settings I did not confirm. If anything is ambiguous, ask before writing.
- If any download fails, stop and ask me to paste the source from the kit page rather than guessing the file contents.
</guardrails>
```



## 想自己读，或手动安装

如果你想先读过源代码再装，或偏好自己手动放文件，下面两份都能在这页直接展开看、复制，或下载。



### Stop hook（单独一个 Python 文件，放进 \.claude/hooks/）：下载py

```Python
#!/usr/bin/env python3
"""Stop hook: block turn-end when a spec/plan was written but not yet codex-peer-reviewed.

Reads Stop event payload from stdin. Scans the session transcript for recent
Write/Edit calls touching docs/superpowers/specs/ or docs/superpowers/plans/.
For each such file, checks for a `<!-- codex-peer-reviewed: ... -->` marker.
If any file lacks the marker, outputs {"decision":"block","reason":"..."} so
Claude is re-invoked with instructions to run the codex-peer-review skill.

Fail-open on any error (bad input, missing transcript, etc.) — never block
Stop on infra issues. Respects `stop_hook_active` to avoid loops.
"""

from __future__ import annotations

import json
import os
import re
import sys
from pathlib import Path

WATCHED_DIR_SUBSTRS = ("docs/superpowers/specs/", "docs/superpowers/plans/")
# Marker must carry all three fields the skill emits. This avoids false positives
# when a spec body discusses the marker format in prose or examples — only a real
# completed marker has timestamp+rounds+verdict together.
MARKER_RE = re.compile(
  r"<!--\s*codex-peer-reviewed:\s*\S+\s+rounds=\d+\s+verdict=\S+\s*-->",
  re.IGNORECASE,
)
WRITE_TOOLS = {"Write", "Edit"}
LOOKBACK_MESSAGES = 80  # scan tail of transcript
MARKER_TAIL_BYTES = 1024  # only look for marker in last N bytes of file (it's always appended at EOF)


def _iter_tool_uses(transcript_path: str):
  """Yield (tool_name, input_dict) tuples for assistant tool_use blocks
  in the tail of the transcript. Robust to malformed lines."""
  try:
      with open(transcript_path, "r", encoding="utf-8") as f:
          lines = f.readlines()
  except (OSError, UnicodeDecodeError):
      return

  for raw in lines[-LOOKBACK_MESSAGES:]:
      raw = raw.strip()
      if not raw:
          continue
      try:
          entry = json.loads(raw)
      except json.JSONDecodeError:
          continue
      # Real Claude Code transcript entries are: top-level {type:"assistant", message:{role,content[...]}}
      if entry.get("type") != "assistant":
          continue
      msg = entry.get("message") or {}
      if msg.get("role") != "assistant":
          continue
      content = msg.get("content")
      if not isinstance(content, list):
          continue
      for block in content:
          if not isinstance(block, dict):
              continue
          if block.get("type") != "tool_use":
              continue
          tool = block.get("name", "")
          if tool not in WRITE_TOOLS:
              continue
          inp = block.get("input") or {}
          if isinstance(inp, dict):
              yield tool, inp


def _collect_spec_plan_paths(transcript_path: str, cwd: str) -> list[str]:
  """Find spec/plan absolute paths touched by Write/Edit in the transcript tail.
  De-dups, preserves most-recent-first order."""
  paths_in_order: list[str] = []
  seen: set[str] = set()
  for _tool, inp in _iter_tool_uses(transcript_path):
      fp = inp.get("file_path") or ""
      if not isinstance(fp, str) or not fp:
          continue
      if not any(sub in fp for sub in WATCHED_DIR_SUBSTRS):
          continue
      abs_fp = fp if os.path.isabs(fp) else os.path.normpath(os.path.join(cwd, fp))
      if abs_fp in seen:
          continue
      seen.add(abs_fp)
      paths_in_order.append(abs_fp)
  # Most-recent-first: transcript is chronological, so reverse
  paths_in_order.reverse()
  return paths_in_order


def _has_marker(path: str) -> bool:
  try:
      size = os.path.getsize(path)
      with open(path, "rb") as f:
          if size > MARKER_TAIL_BYTES:
              f.seek(size - MARKER_TAIL_BYTES)
          tail = f.read().decode("utf-8", errors="replace")
      return bool(MARKER_RE.search(tail))
  except OSError:
      # If we can't read the file, treat as reviewed to avoid spurious blocks.
      return True


def _format_block_reason(unreviewed: list[str]) -> str:
  head = unreviewed[0]
  extra = ""
  if len(unreviewed) > 1:
      rest = "\n".join(f"  - {p}" for p in unreviewed[1:])
      extra = f"\n\nOther unreviewed files in this turn:\n{rest}"
  return (
      f"Codex peer review pending.\n\n"
      f"A spec/plan was written in this turn but has not been peer-reviewed by Codex yet:\n"
      f"  {head}{extra}\n\n"
      f"Invoke the `codex-peer-review` skill (Skill tool) now and review this file before ending the turn. "
      f"The skill runs an iterative single-thread dialogue with Codex (round 1 fresh, rounds 2+ via `codex exec ... resume <session-id> ...`) until Codex returns `## Verdict\\nAPPROVED` — no round cap, pushbacks require explicit codex CONCEDE. Then appends a `<!-- codex-peer-reviewed: ... -->` marker that this hook recognizes.\n\n"
      f"If you've already completed the review in conversation but forgot to write the marker, just append it manually:\n"
      f"  cat >> {head} <<'M'\n"
      f"  <!-- codex-peer-reviewed: $(date -u +%Y-%m-%dT%H:%M:%SZ) rounds=<N> verdict=approved -->\n"
      f"  M"
  )


def main() -> int:
  try:
      payload = json.load(sys.stdin)
  except (json.JSONDecodeError, ValueError):
      return 0  # fail-open
  if not isinstance(payload, dict):
      return 0

  # Loop guard: if Claude Code already retried after a previous block, give up.
  if payload.get("stop_hook_active"):
      return 0

  transcript_path = payload.get("transcript_path")
  if not isinstance(transcript_path, str) or not os.path.exists(transcript_path):
      return 0

  cwd = payload.get("cwd") or os.getcwd()
  if not isinstance(cwd, str):
      cwd = os.getcwd()

  touched = _collect_spec_plan_paths(transcript_path, cwd)
  if not touched:
      return 0

  unreviewed = [p for p in touched if os.path.exists(p) and not _has_marker(p)]
  if not unreviewed:
      return 0

  print(json.dumps({"decision": "block", "reason": _format_block_reason(unreviewed)}))
  return 0


if __name__ == "__main__":
  try:
      sys.exit(main())
  except Exception:
      # Absolute fail-open. Never let a bug here brick the user's session.
      sys.exit(0)

```



### codex review skill（一个文件夹，解压整个拖进 \.claude/skills/）：下载资料文件夹\.zip

```Python
---
name: codex-peer-review
description: Use after writing a spec (docs/superpowers/specs/) or plan (docs/superpowers/plans/) to peer-review it with Codex CLI via single-thread iterative dialogue. Loops until codex returns APPROVED. Pushbacks require codex's explicit concession; no round cap; no rubber-stamping; no walk-away with unresolved disagreements.
---

# Codex Peer Review

Peer-review a freshly written spec or plan with Codex (different model = different blind spots). **Single iterative dialogue with ONE codex session that remembers every round.** Terminate only when codex returns `## Verdict\nAPPROVED`. Pushbacks must reach explicit consensus (codex says CONCEDE).

The Stop hook `codex-review-gate.py` will tell you when this is needed by blocking turn-end and naming the unreviewed file.

**Announce at start:** "I'm using codex-peer-review to peer-review <path> with Codex."

## When This Skill Runs

- The Stop hook blocked turn-end with a reason naming a spec/plan path without the `<!-- codex-peer-reviewed: ... -->` marker
- Or you (Claude) just wrote a spec/plan and want to proactively review
- Or the user explicitly invoked this skill on an existing file

## Termination

**Single condition: codex returns `## Verdict\nAPPROVED`.**

No round cap. No escalation to user. No walk-away with disagreements. If codex maintains a pushback you disagree with, keep arguing — rephrase, give stronger evidence, dig into why your reasoning is sound. If codex raises new issues each round, fix or push back on those too. Loop until consensus.

## Per-review isolation & never trusting stale output

Two failure modes this section prevents. Both end the same catastrophic way — you read an `APPROVED` that isn't this round's, and stamp the marker on a document codex never actually passed:

1. **Stale read (the higher-probability one).** If a `codex exec` round errors (e.g. the model returns a 400) it may not write its `-o` file at all. A naive "run, then Read the `-o` file" then silently reads the PREVIOUS round's file — or a leftover from an earlier review — and treats it as this round's verdict.
 **Guard: capture codex's exit code after every call and check it. On non-zero: stop, report the error, do NOT read the `-o` file, do NOT write the marker.**
2. **Cross-review collision (lower-probability).** Hardcoded `/tmp/codex-rN.txt` is a global path two concurrent reviews share. And `resume --last` resumes the newest session *in the current cwd* — not globally (the `--all` flag exists precisely to "disable cwd filtering"), so separate worktrees do NOT cross-contaminate. The residual window is two reviews in the SAME cwd, or a Codex.app / other codex session spawned in that dir between round 1 and round N, making `--last` grab the wrong session.
 **Guard: each review gets its own fresh temp dir (`mktemp -d`, so it can never reuse a prior review's files), and resumes by the session id captured in round 1 — never `--last`.**

Set up once at the start of round 1, then look it back up in later rounds:

```bash
REVIEW_PATH="<ABSOLUTE PATH of the file under review>"
KEY=$(printf '%s' "$REVIEW_PATH" | { command -v shasum >/dev/null 2>&1 && shasum -a 256 || sha256sum; } | cut -c1-16)

# round 1 — fresh unique dir, record a pointer to it keyed by the reviewed file
DIR=$(mktemp -d "/tmp/codex-review.XXXXXXXX")
printf '%s' "$DIR" > "/tmp/codex-review.$KEY.dir"

# rounds 2+ — read back THIS review's dir
DIR=$(cat "/tmp/codex-review.$KEY.dir")
```

**zsh note:** use `rc` (or any name) for `$?` — NOT `status`, which is a read-only special variable in zsh and will error on assignment.

## The Protocol

### Step 1: Decide whether to brief codex

The spec/plan document should be self-contained — both `brainstorming` and `writing-plans` skills enforce this. **In ~99% of cases, no briefing is needed.** Just hand codex the absolute path; codex reads the file directly.

**Compose a short context note ONLY if there's material context the document doesn't capture, such as:**

- The document iterates on a prior spec/plan that codex won't see on its own
- A constraint the user surfaced verbally that didn't land in the document
- An approach that was discussed and explicitly rejected but isn't documented

If none of these apply: skip briefing entirely; go to Step 2 with just the path.

If you decide briefing IS needed: in Step 2's prompt template, insert a `# Material context` block (a short paragraph, under ~150 words) immediately above the `# Document to review` block. Keep it factual — do NOT lead codex toward issues you think matter; that defeats the fresh-eyes value of peer review.

### Step 2: Round 1 — start the codex session (fresh)

Set up the per-review dir, then start codex with `--json` so we can capture THIS review's session id (we resume by id in later rounds, never `--last`):

```bash
REVIEW_PATH="<INSERT ABSOLUTE PATH>"
KEY=$(printf '%s' "$REVIEW_PATH" | { command -v shasum >/dev/null 2>&1 && shasum -a 256 || sha256sum; } | cut -c1-16)
DIR=$(mktemp -d "/tmp/codex-review.XXXXXXXX")
printf '%s' "$DIR" > "/tmp/codex-review.$KEY.dir"

codex exec --json --sandbox read-only -o "$DIR/r1.txt" - <<'CODEX_EOF' > "$DIR/r1.events.jsonl"
You are peer-reviewing a spec or plan document. Claude (the user's main agent) wrote it and self-reviewed it. This is a single iterative dialogue — I (Claude) will fix or push back on each issue you raise; you re-evaluate in later rounds, and we continue until consensus. Don't rubber-stamp, and don't manufacture issues to drag it out.

# Why this review exists
This document drives real implementation: a plan is executed step-by-step by a zero-context engineer who will not notice its mistakes; a spec is the foundation every downstream plan and line of code inherits. Whatever it gets wrong propagates uncaught. The author wrote and self-reviewed it, so every flaw rooted in the author's own assumptions is still in it, invisible to the author by construction. Your job is exactly the review the author cannot do on themselves: independently decide whether this document, built on as written, yields correct, complete, and maintainable software.

# How to review
Treat the document as a hypothesis to falsify — not a description to follow. It is written to look complete and correct; read it forwards and its own narrative carries you to "looks fine." So don't review the document — review reality, with the document as the claim under test. Work only from primary sources:

- The real codebase. You have the repository — read it. Verify every claim the document makes about existing code, types, and behavior — especially completeness claims (that a set is exhaustive, that nothing else is affected). Never accept the document's description of the code as given.
- The document's own stated scope. Every goal it commits to must be fully accounted for by the document itself — in a plan, by a concrete step plus a check that proves the new behavior works (not merely that nothing broke); in a spec, by a mechanism that coherently achieves it. A committed goal that nothing delivers is a gap.

Also judge the design the document prescribes: the executor has no taste and builds exactly what is written, so unsound or debt-laden design is itself a finding. If you genuinely cannot break the document from primary sources, it passes.

# Document to review
<INSERT ABSOLUTE PATH>

Report every issue that would ship a bug, a regression, or real long-term debt if the document were taken as written — whatever its category. Skip pure style, naming, and wording preferences, and don't demand premature abstraction or gold-plating. The bar is impact, not how interesting the issue is.

Output in this exact format:

## Verdict
APPROVED  (or)  ISSUES FOUND

## Major issues (omit if APPROVED)
- [issue]: [why it matters]
- ...

## Recommendations (advisory, do not block)
- [optional suggestion]
- ...
CODEX_EOF
rc=$?
if [ "$rc" -ne 0 ]; then
echo "codex exec FAILED (exit $rc). Do NOT read r1.txt; do NOT write the marker. Last events:"
tail -n 20 "$DIR/r1.events.jsonl"
exit "$rc"
fi

# Capture THIS review's codex session id (resume by id later, never --last)
grep -m1 '"thread.started"' "$DIR/r1.events.jsonl" | sed -E 's/.*"thread_id":"([^"]+)".*/\1/' > "$DIR/thread_id"
echo "review dir: $DIR   codex session: $(cat "$DIR/thread_id")"
```

Read `$DIR/r1.txt` (only because `rc` was 0 — a failed round must never reach a Read).

- **If verdict is `APPROVED`** → **Step 4: Finalize** with `rounds=1`.
- **If verdict is `ISSUES FOUND`** → Step 3.

> If `$DIR/thread_id` came out empty (codex didn't emit a `thread.started` event), fall back to `resume --last` for round 2+ AND run the rest of the review without launching any other codex session in between, so `--last` still points at this one. Note this limitation in your final report.

### Step 3: Iterate — judge, fix-or-pushback, then resume the same codex session

For each issue codex raised, decide:

- **Fix**: issue is valid → use Edit tool to update the spec/plan
- **Push back**: you disagree → record your reasoning; do NOT change the file

Don't rubber-stamp. If codex flagged something you genuinely think is wrong, push back with specific reasoning. Don't capitulate for the sake of finalizing — capitulation only happens when codex's MAINTAIN reasoning genuinely convinces you.

Then resume the SAME codex session for round N **by its captured id** (so codex remembers everything it said in earlier rounds — never start a fresh session for rounds 2+, and never use `--last`, which could grab a different review's session):

```bash
REVIEW_PATH="<INSERT ABSOLUTE PATH>"
KEY=$(printf '%s' "$REVIEW_PATH" | { command -v shasum >/dev/null 2>&1 && shasum -a 256 || sha256sum; } | cut -c1-16)
DIR=$(cat "/tmp/codex-review.$KEY.dir")
THREAD_ID=$(cat "$DIR/thread_id")

codex exec --sandbox read-only -o "$DIR/r<N>.txt" resume "$THREAD_ID" - <<'CODEX_EOF'
Round <N>. I responded to your previous round as follows:

FIXED (these are now updated in the document — please re-read):
- [issue X]: [brief description of what I changed]
- ...

PUSHED BACK (need your explicit CONCEDE or MAINTAIN on each):
- [issue Y]: [my reasoning, addressing your specific concern]
- ...

Please:
1. Re-read the document — FIXED items have been edited
2. For each PUSHED BACK item: say either CONCEDE (you accept my reasoning) or MAINTAIN (your concern stands — explain specifically what my reasoning misses)
3. Verify the FIXED items actually address what you originally raised
4. Raise any genuinely new major issues you spot (don't manufacture — only real ones)

Output in this exact format:

## Verdict
APPROVED  (or)  REMAINING ISSUES

## On Claude's pushbacks
- [issue Y]: CONCEDE  (or)  MAINTAIN — [if maintain, what my reasoning missed]
- ...

## Remaining or new issues (omit if APPROVED)
- [issue]: [why concerned]
- ...
CODEX_EOF
rc=$?
if [ "$rc" -ne 0 ]; then
echo "codex exec FAILED (exit $rc). Do NOT read r<N>.txt; do NOT write the marker."
exit "$rc"
fi
```

Read `$DIR/r<N>.txt`.

- **If verdict is `APPROVED`** → **Step 4: Finalize** with `rounds=<N>`.
- **If verdict is `REMAINING ISSUES`** → repeat Step 3 with N+1.

**On MAINTAIN responses:** that pushback is unresolved. In the next iteration, you MUST either:
- (a) Strengthen your reasoning — be more specific, cite the contradiction codex missed, or
- (b) Capitulate and fix it — because codex's MAINTAIN reasoning genuinely convinced you

Do NOT pretend MAINTAIN issues are resolved. Do NOT shortcut to APPROVED by withdrawing pushbacks just to end the loop.

### Step 4: Finalize

1. Append the marker to the document footer:

```bash
cat >> <ABSOLUTE_PATH> <<MARKER

<!-- codex-peer-reviewed: $(date -u +%Y-%m-%dT%H:%M:%SZ) rounds=<N> verdict=approved -->
MARKER
```

`<N>` is the round count where APPROVED was reached. The only verdict value is `approved` — under this protocol there's no walk-away state.

2. Report back to user:
 - Rounds completed
 - Codex's main original concerns (1-3 bullets)
 - What was changed (with reasoning)
 - What you pushed back on AND codex eventually conceded (with reasoning) — shows where your judgment held
 - What you capitulated on because codex's reasoning was sound (transparency about where you changed mind)

Keep the report tight. User reads the diff for full detail.

## Failure Modes

| Symptom | Action |
|---|---|
| `codex exec` returns non-zero (the `rc` guard fires) | Report the error to the user. Do NOT read the `-o` file; do NOT write the marker. (The Stop hook re-blocks only on its first trigger — once `stop_hook_active` is set it fails open — so don't assume a failed review is hard-gated; surface it.) |
| Codex output unparseable (no `## Verdict`) | Treat as `ISSUES FOUND`, dump raw text as the issue list, continue. |
| `$DIR/thread_id` is empty after round 1 | Codex emitted no `thread.started` event. Fall back to `resume --last` for rounds 2+, and don't start any other codex session mid-review so `--last` still targets this one. Flag it in the final report. |
| You find yourself wanting to brief codex on lots of context outside the document | That's a signal the document itself is incomplete. Fix the document, not the briefing — the spec/plan should stand on its own. |
| Codex keeps MAINTAINing despite strong reasoning | Keep iterating — find a sharper angle, cite a specific contradiction, give a concrete example. Don't shortcut by capitulating. Don't shortcut by inventing a fake CONCEDE on codex's behalf. |
| Codex raises trivially new issues each round (sounds like dragging) | Push back: tell codex its calibration is off and these aren't MAJOR. Force it to reach APPROVED or to explain why a "minor" issue is actually load-bearing. |
| Document was massively rewritten between rounds | Mention this in the round prompt so codex re-reads carefully instead of diffing against memory. |

## Don't

- **Don't use `codex exec` (fresh session) for rounds 2+** — you MUST use `codex exec ... resume "$THREAD_ID" ...` so codex maintains memory of every previous round. Fresh sessions break the single-thread principle and force codex to start cold each round (losing memory of prior fix/pushback exchanges).
- **Don't resume with `--last`** — it resumes whatever codex session is globally newest, which under parallel worktrees (or any other codex usage on the machine) can be a DIFFERENT review's session. Always resume by the `thread_id` you captured in round 1.
- **Don't share temp files across reviews** — each review writes only under its own `$DIR` (derived from the reviewed file's absolute path). Never hardcode `/tmp/codex-r1.txt`.
- **Don't rubber-stamp.** If codex raises a non-issue, push back. If you disagree, push back hard.
- **Don't capitulate just to finalize.** Only fix-after-pushback because codex's MAINTAIN reasoning convinced you, not because the loop is dragging.
- **Don't pretend MAINTAIN is APPROVED.** Walk-away with codex maintaining = breach of the protocol. Either argue better or capitulate honestly.
- **Don't fix things codex didn't raise.** This skill reviews what's there; don't sneak in scope creep.
- **Don't skip the marker write** — the Stop hook depends on it; without it you'll get re-triggered forever.
- **Don't pass `-m` to `codex exec`** — `~/.codex/config.toml` already sets `model = "gpt-5.5"`, `service_tier = "fast"`, `model_reasoning_effort = "xhigh"`. Let those defaults apply.

```



# 为什么默认监听 docs/superpowers

## **提示**

默认监听的文件夹是 docs/superpowers/specs/ 跟 docs/superpowers/plans/，因为我自己用 superpowers 这套 skill 框架，它的 brainstorming 跟 writing\-plans 会把 spec 跟 plan 写进这两个地方，所以 hook 默认就盯着它们。你如果也用 superpowers，等于开箱即用；不用的话，安装那一步会问你 plan 放哪，帮你改成你自己的路径。唯一要记得的是，hook 监听的路径跟 skill 里的路径必须一致，要改就两边一起改。



## 装完怎么确认它真的活着

贴下面这段 prompt 进 Claude Code，它会自己侦测你的安装，然后用一个合成的 Stop 事件直接测 stop hook 的 gate（不呼叫 Codex、不花你的 token），回报四项检查的 PASS / FAIL。

**Prompt 2**

**验收 Prompt**

**功能：**

不呼叫 Codex，用一个合成的 Stop 事件直接测 stop hook 的 gate：确认 registration、hook 可执行、挡住未审 plan、放行已审 plan 四项。

**什么时候用：**

装完之后，想确认它真的会挡，而不是只是装好看的。

**你会拿到：**

四项检查的 PASS / FAIL 表，加一句总结（装对了，或哪一项失败、可能原因）。

**可以接到哪：**

无（独立验收）

**AI 会问你：**

1. 这段多半会自动侦测你的安装、不太会问你；只有同时找到全域跟专案两份、或两份都找不到时，才会问你要测哪一个

```SQL
<role>
You are verifying that the cross-model review harness is correctly installed in my Claude Code. Run a self-contained check that proves the Stop hook is registered and actually gates unreviewed plans, without involving Codex. Report PASS or FAIL for each check, then clean up.
</role>

<context-gathering>
Auto-detect the install. Do not ask me unless it is genuinely ambiguous.
1. Find the hook: look for codex-review-gate.py registered under the Stop hooks in .claude/settings.json (this repo) or ~/.claude/settings.json (global). Use whichever one registers it. If both register it, or neither does, ask me which install to test.
2. Read WATCHED_DIR_SUBSTRS from that codex-review-gate.py to learn which folder(s) it watches. Use the first watched folder for the test.
Tell me what you detected (hook path, settings path, watched folder), then run the checks.
</context-gathering>

<execution>
Let HOOK be the hook path, SETTINGS the settings.json path, and WATCHED the first watched folder.

Check 1 (registration): confirm SETTINGS has a Stop hook whose command runs codex-review-gate.py. PASS if present, FAIL if not.

Check 2 (hook is valid): confirm HOOK exists and compiles, e.g. python3 -c "compile(open('<HOOK>').read(),'h','exec')". PASS if no error.

Check 3 (the gate FIRES on an unreviewed plan):
a. Create a throwaway plan at <WATCHED>/_verify_gate.md with one line of text and NO review marker.
b. Write a one-line transcript to a temp file, exactly this JSON object on a single line (substitute the absolute plan path):
   {"type":"assistant","message":{"role":"assistant","content":[{"type":"tool_use","name":"Write","input":{"file_path":"<ABSOLUTE PATH OF THE PLAN>"}}]}}
c. Run: printf '%s' '{"transcript_path":"<TEMP TRANSCRIPT>","cwd":"<CURRENT DIR>","stop_hook_active":false}' | python3 <HOOK>
d. EXPECT stdout to contain a block decision naming _verify_gate.md. PASS if it blocks, FAIL if it is silent.

Check 4 (the gate OPENS once reviewed):
a. Append this marker line to the plan: <!-- codex-peer-reviewed: 2026-01-01T00:00:00Z rounds=1 verdict=approved -->
b. Re-run the exact command from 3c.
c. EXPECT no output. PASS if silent (allowed), FAIL if it still blocks.

Cleanup: delete <WATCHED>/_verify_gate.md and the temp transcript file.

Report a 4-row table (Check 1 to 4, PASS/FAIL) and a one-line verdict: installed correctly, or which check failed and the likely cause.
</execution>

<guardrails>
- This is a dry run. Do NOT call Codex, and do NOT rely on actually ending the turn. You invoke the hook script directly with a synthetic payload.
- Create and delete only the two throwaway files named above. Touch nothing else.
- Use the ABSOLUTE path of the throwaway plan as file_path in the transcript, so the hook resolves it the same way it watches.
- If any check FAILS, name it and the likely cause (hook not registered in settings.json, watched path mismatch, or marker regex mismatch). Never report a silent pass.
</guardrails>
```







###### 配套文章：让 Claude 和 Codex 自动互审：我用两个多月的 cross model review 全套（一键安装 prompt \+ stop hook \+ codex review skill）



> （注：部分内容由豆包工作 AI 生成）
