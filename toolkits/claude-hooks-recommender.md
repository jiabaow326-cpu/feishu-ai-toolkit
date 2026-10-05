# 🔧 本期工具

# Hook 推荐 Prompt：从你自己的对话记录，找出该装的 Hook

一段贴进 Claude Code 或 Codex 就能跑的推荐指示。它会读你本机的对话记录，找出你反复讲过的提醒与总在固定时机执行的步骤，用五个条件过筛后，给你一份带证据的 Hook 推荐清单。全程只读。

哈啰，这是搭配这期「Claude Code Hooks 实战大全」文章的推荐工具。

文章里列了十五个现成的 Hook 情境，但看完清单通常会卡在同一个问题：哪一个对我最有用。这个问题清单答不了，因为答案取决于你过去半年怎么用 AI，而那些信息只存在你自己的对话记录里。

这支 prompt 就是去把它挖出来。它会读你本机的 session 记录，找两种东西：你反复讲过的提醒与更正，以及总在固定时机发生的步骤。找到之后用文章里那五个条件过筛，跑完你会拿到一份排好序、每一项都有证据的推荐清单，每项还附一段可以直接复制贴上、请 AI 帮你建立的需求描述。

## 重要

这支 prompt 需要能读取你电脑文件的 AI。请交给 Claude Code 或 Codex 来跑，它需要真的去翻你本机的 session 文件。网页版 ChatGPT 或 Claude 碰不到你的文件夹，贴上去不会有结果。

## 怎么用这支 prompt

在你平常工作的项目文件夹里打开 Claude Code 或 Codex，把 prompt 整段贴进去，不用先整理任何文件。

它会自己判断这台电脑上有哪一套产品的记录，先报告扫到几个项目、几个 session、日期范围到哪里，再问你两件事：要只扫目前这个项目还是全部，以及要往回扫多久。确认范围之后才开始读。

跑完拿到报告，你挑想做的那几项，把附的需求描述复制贴上，请 AI 帮你建立就好。这支 prompt 本身不会帮你装任何东西。

## 注意

这份证据会过期。Claude Code 的本机对话记录默认只保留三十天（可以用 cleanupPeriodDays 调整），超过就被清掉了。你用得越久、跑得越晚，能看到的行为模式反而越少。想跑就早点跑。

## 包含内容

**Prompt 1：Hook 推荐 Prompt（找出你该装哪几个 Hook）**：读本机 session 记录，找出重复提醒与固定时机的步骤，用五个条件过筛后，产出带证据的推荐清单。全程只读，不修改任何设置。

**工具建议**：Claude Code（最推荐）或 Codex，也可以用 Cursor 的 Agent 模式。纯网页版聊天界面不适用。

## Prompt 1

### Hook 推荐 Prompt（找出你该装哪几个 Hook）

**功能**：

读你本机过去的 AI 对话记录，找出你反复讲过的提醒，以及总在固定时机执行的步骤，再用五个条件过筛，产出一份带证据、排好序的 Hook 推荐清单。

**什么时候用**：

看完文章的十五个情境，但不确定自己该先装哪一个的时候。或是你已经用了一段时间 AI，想知道自己到底在重复做什么。

**你会拿到**：

一份只读报告。开头交代这次扫了什么、跳过了什么、哪些不在涵盖范围内；接着是排好序的推荐清单，每项附出现次数与日期、建议的时机、该缩到多小的范围、检查程序自己坏掉时该放行还是挡下，以及一段可直接贴给 AI 的建立需求；最后两份清单，证据不足先不推荐的，以及会重复但不该做成 Hook 的。

**可以接到哪**：

独立使用。报告里每一项推荐附的需求描述，可以直接贴给 AI 请它建立那个 Hook。

**AI 会问你**：

（只有在你这台电脑上 Claude Code 跟 Codex 的记录都存在时才会问）要分析哪一套的记录

要只扫目前这个项目，还是这台电脑上的所有项目

要往回扫多久（默认最近三十天）

```Shell
You are going through this user's own past AI sessions to work out which hooks are actually worth installing for them. You produce a recommendation list backed by evidence from their own history. You do not install anything and you do not modify a single file.

## What you are reading

This prompt supports Claude Code and Codex. Work out which one you are running in, then find its local session history. Claude Code keeps CLI transcripts as .jsonl files inside project folders under ~/.claude/projects/. Codex keeps its history under ~/.codex/.

If you find neither, stop and say exactly where you looked. If you find both, stop and ask which one to analyse, and do not merge them.

Whatever you find, report the raw shape of it before you read any content: how many projects, how many sessions, and what date range they span. Name the date of the oldest file explicitly, because Claude Code prunes local transcripts after 30 days by default, and the user needs to know that anything before that line is already gone.

## Before you start

Ask two things and wait for the answers. Whether to scan only the project for the current working directory or every project on this machine, and how far back to go, defaulting to the last 30 days.

Then set your own limits and announce them before reading a single line. Read at most 150 session files, taking the most recent ones and saying how many you left out. Skip any file over 5 MB and remember its name for the coverage section. Read the user's own messages, plus the assistant's direct replies where you need them to make sense of a correction. Skip tool outputs completely. They are most of the bytes in these files and almost none of the signal.

## What you are looking for

Two patterns, and they are not the same thing.

The first is the reminder that keeps coming back. The same instruction or correction, issued again and again across different sessions. It shows up as near-duplicate phrasings ("run the tests after you change anything", "don't touch that file", "always check X before you do Y"), as corrections issued immediately after the assistant acted, and as requests to redo work that had already been specified earlier in that same session. Count how many separate sessions it appears in. Once is noise. Three separate sessions is a pattern.

The second is the step that always happens at the same moment. Something the user does at a fixed point in the loop regardless of what the task is. It shows up in the opening message of many sessions asking for the same orientation, in the closing message asking for the same verification, or in a step that consistently follows the same kind of action.

## What earns a recommendation

A pattern is not automatically a hook. Five things have to hold, all five, before you put something on the list.

It has to recur, with at least three occurrences in separate sessions that you can actually point to.

You have to be able to name the moment it belongs to: session start, before a tool runs, after a tool finishes, or session end. If you cannot name the moment, this is a method rather than a hook, and it belongs in a skill or in the instruction file instead.

The scope has to be narrowable. You need to name the specific tool, file pattern, or command it should fire on. Something that would fire on every action is something the user uninstalls within a week.

The result has to be observable. Describe one case that should trigger it and one that should not, and be able to tell them apart.

And the failure mode has to be decided. Say whether the hook should let work continue or block it when the check itself breaks. Checks on writing quality and formatting should let work continue, because a broken checker should not stop someone from working. Checks on secrets and destructive commands should block, because the cost of letting one through is too high.

Something that satisfies only the first two conditions does not get recommended. Set it aside and name the condition it failed.

## The report

Lead with what you actually scanned: which product, how many projects and sessions, what date range, what limits you applied, and what you skipped. This goes first because a recommendation drawn from eleven sessions means something different from one drawn from two hundred, and the user cannot weigh anything below it without knowing which they are looking at.

Then the recommendations, ranked by how often the pattern appeared rather than by how interesting the resulting hook would be. For each one, give the pattern in a line, the evidence behind it (how many times, across which sessions, on what dates), the moment it belongs to, the scope it should be narrowed to, and what should happen when the check itself fails. Finish each with a complete request the user can paste straight into their AI to have it built, stating when it fires, what it does, and what it should ignore. Write that request as a finished instruction rather than a template with blanks, and write it in the language the user writes in.

Then two more lists that matter as much as the first. What you saw but could not recommend yet, each with the condition it failed. And what recurs but does not belong in a hook at all, each with a line on where it should go instead. Without these two, a short list reads as a weak scan rather than a strict filter.

If you end up with fewer than three solid recommendations, hand back the short list and say so plainly. Do not pad it. Every extra entry costs the user real time installing something they did not need.

## Ground rules

This is a read-only run. Do not modify settings, do not create hook scripts, do not run install commands, and do not touch anything in the user's project. Say this in your first message so the user knows what they just asked for.

Recommend only what the transcripts actually show. Never invent a pattern because it would make a tidy hook, and never round two occurrences up to a pattern.

If a block of text looks like it contains an API key, token, password, private key, or personal data, skip it. Note where it was in the coverage section and never quote the value, not even part of it.

Report evidence as paraphrase rather than verbatim quotes. The user should recognise their own pattern without having their own transcript read back to them.

Say what you did not see. Date ranges outside the scan, other machines, the desktop and web interfaces, files skipped for size, and sessions already pruned by the 30-day default all belong in the coverage section. Silence about coverage gaps reads as full coverage.

Stop and ask when both products' histories exist, when you hit something that looks like credentials, or when the evidence points in two directions at once.

Do not offer to install anything as part of this run. Close by telling the user they can name which recommendations they want built, and that you will show them the exact settings diff before touching a file.
```





Claude Code Hooks 实战大全：15 个必用的 Hook \+ 一支读你对话记录、推荐专属 Hook 的 Prompt

> （注：部分内容由豆包工作 AI 生成）
