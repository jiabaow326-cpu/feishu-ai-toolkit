# 本期工具

Prompt Set

# CLAUDE\.md 健检 Prompt：逐条检查你的指令文件是否值得保留

一段贴进 Claude Code 或 Codex 就能运行的健检指示。它会把指令文件拆成一条一条，先核对事实和项目现状；取得同意后，再按照目前模型自己的官方 prompting guide 检查写法。最后生成逐条建议清单，不主动修改文件。



哈喽，这是搭配本期「CLAUDE\.md 完整实操攻略」文章的健检工具。



文章里我们提到，维护指令文件真正难的是修剪。多数人的文件从建立那天起只增不减，因为每一条都是自己踩坑换来的，删除会心痛。问题出在标准：你没法凭感觉判断哪一条已经过期、哪一条只是看起来过期。



这个 prompt 会把你的指令文件拆成一条一条，先核对内容是否仍然符合项目现状，以及同一件事能不能快速查到。取得你的同意后，它才会读取目前模型自己的官方 prompting guide，检查规则写法。跑完你会拿到一份逐条的留、改、搬、删、待验清单，每一条都附上判断依据。



# 重要

这个 prompt 需要能读取你电脑文件的 AI。请交给 Claude Code 或 Codex 来跑。它需要真的去翻你的项目，验证每一条指令是否仍有效。网页版 ChatGPT 或 Claude 碰不到你的资料夹，跑不起来。







# 怎么用这支 prompt

## 路径 A：完整健检（建议）



在你想健检的项目资料夹里打开 Claude Code 或 Codex，把 prompt 整段贴进去。它会自己判断目前使用哪一套工具，再找出对应的 CLAUDE\.md 或 AGENTS\.md。开跑前它只会问你一个问题：要不要顺便按照目前这个模型的官方 prompting guide 来检查。



## 路径 B：只检查事实，不管 prompting 写法



上面那个问题回答“不用”，它就只跑第一关：每条指示是否仍然符合项目现况，以及同一件事能不能快速查到。适合你只想先清理过期内容，或官方指南暂时找不到的时候。



## 路径 C：先跑官方的 /doctor，再跑这个



如果你用的是 Claude Code，可以先跑一次 /doctor，处理能从 codebase 直接推导的内容，再跑这支 prompt。这样比对基准会更干净。



# 注意！！

**换模型之后特别值得跑一次。**文章里讲过，指令档的写法会跟着模型世代变。升级模型之后，部分为旧模型留下的规则可能已经不合适。这支 prompt 的第二关会根据目前模型自己的官方指南，找出值得重新测试的项目。









# 包含内容：

**Prompt 1：The CLAUDE\.md Checkup（CLAUDE\.md 健检）：**把指令档拆成一条一条，先核对事实与项目现况，再视你的选择对照当前模型的 prompting guide，产出逐条建议清单，不主动修改档案。



**工具建议：Claude Code（最推荐）或 Codex。**纯网页版聊天界面不适用。







# The CLAUDE\.md 检查（CLAUDE\.md 健检）

**功能:** 把这个项目适用的指令文件拆成一条一条，逐条回到项目验证事实，判断信息是否能快速查到，再按照目前模型自己的官方 prompting guide 检查写法，最后给出逐条建议。



**什么时候用:** 刚换到新一代模型的时候最值得跑。另外就是觉得文件越来越大、AI 开始不太听话，或者接手别人的项目想搞清楚继承了哪些规则的时候。



**你会拿到:** 一份逐条建议清单。每条包含原文、建议（留／改／搬／删／待验）、实际查到的证据，以及该搬的话要搬去哪。依「能还你多少注意力」排序。



**可以接到哪: **独立使用。清单出来后可在同一个对话里指定要套用哪几条，AI 会先给 diff 再动手。



**AI 会问你：**

要不要按照你目前正在用的这个模型的官方 prompting guide 来检查？（它会先报自己是什么模型；回答不用的话就只跑事实那一关）

```SQL
You are auditing the instruction file that governs your own behaviour in this project, one instruction at a time. You produce a recommendation list. You do not edit anything.

## What you are auditing

This prompt supports Claude Code and Codex. Identify which one you are running in without asking the user. If you are running in neither, stop and explain that this checkup does not cover that product's instruction-loading rules.

If you are Claude Code, resolve the effective sources using Claude Code's documented loading rules. Include the managed-policy CLAUDE.md when present, ~/.claude/CLAUDE.md, ~/.claude/rules/, the applicable project and local CLAUDE.md files from the filesystem hierarchy, project .claude/rules/, and nested CLAUDE.md or path-scoped rules that can load on demand inside this project. Respect exclusions and distinguish startup sources from on-demand sources.

If you are Codex, build the effective instruction chain before auditing any instruction. Resolve $CODEX_HOME, defaulting to ~/.codex. At the global scope, select only the first non-empty file in this order: AGENTS.override.md, then AGENTS.md. Then walk from the project root to the current working directory. In each directory, select only the first non-empty file in this order: AGENTS.override.md, AGENTS.md, then each filename from project_doc_fallback_filenames in its configured order. Concatenate only the selected files from root to the current directory. A file shadowed by an override or an earlier filename may be listed as inactive, but its instructions must not enter the recommendation list.

For every source, record its actual scope and load behaviour before judging it. Distinguish instructions loaded at session start from nested or path-scoped instructions loaded only when matching files are involved.

Read the whole thing, then break it into individual instructions. One line is usually one instruction, but a paragraph making three separate demands is three. Track the source file and scope of every instruction. Every instruction gets audited on its own, and nothing gets skipped for looking harmless.

## Before you start

State which model you are currently running as.

Then ask the user one question: do they want their instructions audited against that model's current official prompting guidance? If yes, go read that guidance before you judge anything. If they decline, or you cannot find current guidance for this model, say so plainly and run check 1 only.

That is the only question you ask them. Everything else you work out yourself.

## The two checks

Every instruction gets check 1. Check 2 runs only when the user asks for it and you successfully find current official guidance for this model.

### Check 1: Does it earn its place?

An instruction file is not general storage. Instructions loaded at session start cost attention on every request. Nested and path-scoped instructions cost attention only when work enters their scope. Judge each line against its real load frequency rather than pretending every source is always loaded.

Establish two things. Use an isolated subagent where the instructions below make that possible; otherwise rely on explicit read-only repository evidence and disclose the limitation.

**Is it still true?** Verify the claim against the repository as it exists right now, reasoning from what you can actually see rather than from what the file asserts. Does the command still exist in the package scripts or configuration? Does the path still exist? Is that still the framework, package manager, test runner, or workflow? Use read-only evidence. Do not execute builds, tests, or other commands that may create files. If runtime proof is required, mark the instruction for testing instead of claiming a result.

**Is it obvious?** In Claude Code, use the built-in Explore subagent for this check when it is available, because that built-in agent does not load CLAUDE.md files. In another environment, use an isolated worker only if you can confirm it did not receive the instruction being tested. If clean isolation is unavailable, do not pretend you ran a blind test. Instead, cite the exact repository files and the short search path that reveals the same fact, and label the result as a repository-evidence check. If a quick look around the repo reveals the same thing, weigh that against the instruction's actual load frequency and scope.

Then judge whatever survives against what belongs in an instruction file at that scope: things that cannot be worked out quickly from the repo, that apply to most work within the scope where the instruction is stored, and that will still hold in a few months. In practice the keepers are rules you must not get wrong, procedures that have to be done one fixed way, knock-on changes that are easy to forget, what counts as finished, and pointers to where information lives. Treat an always-loaded project overview more strictly than a narrow rule that loads only when its matching files are involved.

### Check 2: Is it written the way this model should be prompted?

Run this only if the user asked for it and you have read the guidance.

Use only the current official guidance you just read for the model that is actually running. Do not transfer Claude guidance to Codex, Codex guidance to Claude, or guidance for one model generation to another. If the guidance does not address a practice, say so and do not invent a verdict from a different model's advice. Cite the specific part of the guidance behind each recommendation so the user can check your reasoning.

Be careful here. "This model can probably handle it on its own" is a hunch, not evidence, and acting on hunches is how people delete the one rule that was actually saving them. When an instruction looks obsolete on these grounds alone, mark it as needing a test and say exactly what that test is: which instruction to pull out temporarily, and what kind of task to run before and after to compare.

## The recommendation list

Go through every instruction and give a verdict: keep as is, rewrite, move somewhere better, delete, or test before deciding.

For each one, quote the original, say what you propose, and give the evidence you actually found. If you cannot cite evidence, do not propose the change. Say what evidence would settle it and move on. Never fill a gap with reasoning that merely sounds right.

When something should move rather than go, give a destination that exists in the current product. In Claude Code, folder-specific rules can move to a nested CLAUDE.md, and file-pattern rules can move to .claude/rules with a paths filter. In Codex, use a nested AGENTS.md or AGENTS.override.md where its documented scope fits. Long procedures needed only for one kind of task belong in a Skill when the current product supports that mechanism. Anything that has to be guaranteed rather than merely encouraged belongs in an enforceable setting, hook, pre-commit check, or CI, chosen from mechanisms the current environment actually supports.

Order the list by how much attention each change gives back. Put always-loaded instructions ahead of rarely activated nested or path-scoped rules when the likely savings differ. Within similar scopes, rank larger and more frequently relevant changes first.

## Ground rules

This is a report-only run. Do not create, modify, or delete files, and do not run builds, tests, or commands that may write caches or artifacts. Use read and search operations only. Say this in your first message so the user knows what the prompt is asking you to do. If the environment offers a plan or read-only mode, recommend enabling it before continuing.

If anything in the files looks like a key, a token, or personal data, flag where it is and never quote it.

Do not offer to apply changes as part of this run. Close by telling the user they can name the items they want applied and you will show them the exact diff before touching a file, and that you will not commit anything on your own.
```





配套文章：CLAUDE\.md 完整实操攻略 \+ CLAUDE\.md 健检 Prompt



