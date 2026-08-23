# Shuffle CLI BYOM — Bring Your Own Model

## Status: IMPLEMENTED (v0.1) — verified working 2026-08-22

Decision: **companion tool** (no fork), **fully local sessions** (no Shuffle
registration), runners: **Codex + Claude Code**.

## Source analysis

CLI v1.0.13, MIT, 12 source files. Thin Axios API client. The model call happens
on Shuffle's **server** (`POST /cli/ai-design/sessions/{hash}/runs`) — the CLI
never calls a model directly.

**Key finding:** the CLI package contains **zero components, templates, or design
tokens**. Shuffle's component library is proprietary and server-side. A local
BYOM runner therefore cannot reuse Shuffle's components — it replaces the whole
design-to-code pipeline. The workflow (prompt → complete site on disk) is what's
preserved.

## Implemented architecture

```
prompt → templates/design-brief.md → local CLI (codex|claude) → <out>/<runner>/site
```

- Companion tool `shuffle-byom` (Node, no deps), repo `~/workspaces/shuffle-byom/`
- Shared design brief template: design-system rules, required file layout
  (`index.html`, `assets/styles.css`, `assets/app.js`), accessibility/perf
  constraints, and a machine-parseable `{"files_written": ...}` summary block
- Per-runner output subdirectories so multiple models never clobber each other
- Verification: required files exist; reports size + model summary
- Credential boundary: never reads `~/.codex/` or `~/.claude/` — each CLI
  authenticates itself (Codex OAuth/ChatGPT, Claude OAuth)

## Verified on this machine (2026-08-22)

| Runner | Command | Result |
|---|---|---|
| codex | `codex exec <brief> --sandbox workspace-write --skip-git-repo-check --json` | ✓ 20.7 KB site (default model gpt-5.6-terra) |
| claude | `claude -p <brief> --output-format json --dangerously-skip-permissions` | ✓ 30.5 KB site (claude-sonnet-5, ~$0.55/run) |

Both ran side-by-side on one brief ("Ember & Oak" coffee roastery landing page).

## Pitfalls discovered

1. **`codex exec` requires `--skip-git-repo-check`** when cwd is not a git repo.
2. **`codex exec` reads stdin** — must be closed immediately (`child.stdin.end()`)
   or the run fails with "Reading additional input from stdin...".
3. **`-m <model>` only works for models your auth supports** — `o4-mini` failed
   with exit 1 on a ChatGPT-logged-in CLI; default (`gpt-5.6-terra`) works.
4. **Codex `--json` output is NDJSON** (thread.started, agent_message,
   file_change, turn.completed lines), not a single JSON object. Parse the
   stream for the summary block.
5. **Claude needs `--dangerously-skip-permissions`** for non-interactive file
   writes. Contained because output dir is a dedicated scratch dir.
6. **Claude writes `.omc/` session state into the output dir** — filter it when
   listing/verifying results.
7. Combined runs take ~4–5 min total (2 min per runner) — don't use tight outer
   timeouts.

## Roadmap

- [x] Codex runner
- [x] Claude runner
- [x] Multi-runner side-by-side
- [ ] Shuffle-compatible output manifest (`--save-output` shape)
- [ ] Playwright screenshot preview pass
- [ ] `--model` availability validation per CLI
- [ ] Server-side BYOM hook from Shuffle (would enable component reuse — out of
      our control; would be a Shuffle feature)
