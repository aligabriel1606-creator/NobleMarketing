---
name: token-efficiency
description: Minimize token usage in every session. Apply by default when reading files, running commands, exploring codebases, or producing output — filter before reading, prefer targeted search over full-file reads, keep command output quiet, and summarize instead of dumping. Use especially when the user mentions tokens, cost, limits, slow sessions, or context bloat.
---

# Token Efficiency

Goal: spend tokens only on content that changes the outcome. Apply these rules by default; override them only when the user explicitly asks for full output.

## Reading files

- Never read a file blind. Check size first (`wc -l`), then read with `offset`/`limit` or grep for the relevant section.
- Prefer Grep/Glob over Read for locating code. Read only the section you need, not the whole file.
- For structured data (JSON, YAML, CSV, logs): inspect with `jq`, `python3 -c`, `head`, `tail`, or `grep` instead of loading the file into context.
- Never read entire log files. Filter first: `tail -100`, `grep -i error`, a specific time range.
- Check lightweight sources before heavyweight ones: `git status --short`, `git diff --stat`, `package.json` before opening source files.

## Editing and writing files

- Code files: Read + Edit (a reviewable diff is worth the read cost).
- New files: Write directly, no prior read needed.
- Pure transformations of data files (copy, append, bulk replace, merge): use bash (`cp`, `sed`, `awk`, `cat`) instead of Read + Write — the file content never has to enter context.

## Running commands

- Use quiet flags by default: `-q`, `--quiet`, `--silent`, `git -c advice.*=false`.
- Cap output at the source: `head -50`, `--max-count`, `-maxdepth 2`, `tree -L 2`.
- Batch independent commands into one call; run independent tool calls in parallel.

## Exploring codebases

- Get the structure first (file tree, exports, function names), then read only the files that matter.
- For broad multi-file searches, delegate to an Explore subagent and keep only its conclusion in context.
- Read 2–3 representative files fully to learn a pattern; grep for the rest.

## Output discipline

- Summarize results; don't echo raw command output or file contents back to the user unless asked.
- Don't re-state file contents you just wrote or edited.
- Keep progress notes to one line; put the substance in the final message only.

## Session hygiene

- Don't load MCP servers, plugins, or skills irrelevant to the current task.
- Avoid changing tool/MCP configuration mid-session; it invalidates the prompt cache.
- When context grows stale, prefer compacting over dragging dead history forward.

## When to override

Read fully and show verbose output when: the user asks for it, the file is small (< ~200 lines) and central to the task, or filtered output would strip context needed for correctness (e.g., an error whose meaning depends on surrounding lines). Correctness always beats savings — never skip a read that a safe edit depends on.
