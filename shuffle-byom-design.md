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

---

# Component Access Discovery — VSC Extension (2026-08-23)

The shuffle-vsc-extension repo reveals a **client-accessible component API** the
CLI doesn't use. Verified live 2026-08-23:

- `GET https://shuffle.dev/api/state?api_key=&email=` → editors (tailwind,
  bootstrap, bulma, material-ui, shadcn/ui), each with `libraries[]` = {name, url}.
  Demo mode (no key): 87 libraries.
- `GET <library url>` e.g. `https://shuffle.dev/api/library/<uuid>` →
  `{library, name, components: {category: [{id, preview, code}]}}` with FULL
  HTML/JSX source inline. Flex Tailwind: 884 comps / 113 cats / 616 KB JSON.
- Assets in code (`flex-ui-assets/...`) are publicly served from
  `https://shuffle.dev/<path>` (verified HTTP 200). Previews on static.shuffle.dev.
- Extension flow: fetch state → fetch library JSON → render preview grid →
  copy `code` to clipboard. That's the whole trick.

## Integration plan for shuffle-byom

1. `fetch-libraries.ts`: pull `/api/state`, cache all library JSONs locally
   (~50–80 MB total est.), build category index.
2. Brief enrichment: given user prompt, pick N relevant components by keyword/
   category match and inject their code into the agent brief as "use these
   Shuffle components as building blocks; adapt, don't invent".
3. Or deterministic assembly: LLM picks + sequences components; local script
   stitches HTML, rewrites asset URLs to absolute shuffle.dev paths (or
   downloads assets locally).
4. CAVEAT: catalog is proprietary — commercial reuse needs ToS/license check;
   paid api_key switches state to 'full' mode with more libraries.

This closes the gap that killed v0.1 ("components never touch your machine") —
they do now, via the same endpoints the VS Code extension uses.

## Implementation status (2026-08-23) — v0.2 SHIPPED

Built and verified end-to-end in `~/workspaces/shuffle-byom/` (commit 53d7b24):

- `shuffle-byom sync --editor tailwind` → 45 libraries, 13,599 components cached
  locally (demo mode, zero failures). Full catalog sync = 5 editors (~87+ libs).
- `shuffle-byom "<prompt>" --editor tailwind` → selects top-N components by
  keyword/category score, injects them as MANDATORY design sources, runner
  (codex/claude) derives sections from them with `<!-- derived: ... -->` comments.
- Verified run: Ember & Oak coffee roastery, codex + 6 components → 204 KB site,
  6 sections, 5 provenance comments, 12 assets downloaded locally
  (`--local-assets`). Screenshot: /tmp/byom-v2-full.png.
- Paid VSC api key → full mode: `shuffle-byom sync --api-key K --email E` or
  ~/.shuffle-byom/credentials.json or SHUFFLE_BYOM_API_KEY/SHUFFLE_BYOM_EMAIL.
  (CLI OAuth token ~/.shuffle-cli/token does NOT work — separate credential
  system, verified 403/stays demo.)

Pitfalls fixed during build:
1. Some components ship EMPTY code — filter before scoring/sorting.
2. Category names carry variant suffixes "(contact-dark-border)" — strip them
   for the 2-per-category diversity guard.
3. Asset URL regex must handle `src="..."` (= sign) AND `url('...')` — the
   original pattern matched only the latter; Shuffle code uses both heavily.
4. `--local-assets` must download PER RUNNER dir and resolve from pristine code
   each time, or runner #2 gets runner #1's rewritten paths.

## PAID TIER LIVE — full-mode validation (2026-08-23)

- Credentials: `~/.shuffle-byom/credentials.json` (apiKey `e104…f7c6` + `salem@viadelweb.com`). First key (`020a…290a`) was bound to a different account email — server returned `error: "'E-mail' and 'API Key' do not match."` while still reporting `mode: demo` with no error surfaced by our old probe (the `error` field must be read from the JSON body).
- **What paid mode actually unlocks:** identical library/component LISTINGS (87 libs, same counts), but demo serves `code: ''` placeholders for 92.6% of tailwind components (12,591 of 13,599). Full mode serves real source for 100%. Plus 42 extra libraries in bootstrap/bulma/mui/shadcn (total cache now 21,680 components).
- Full sync: 87/87 libraries, 0 failures → `~/.cache/shuffle-byom` (demo backup at `~/.cache/shuffle-byom.demo.bak`).
- Code changes: `--editor` accepts comma-separated list (`--editor tailwind,shadcn/ui` → `editorIds`); selection dedupes by component id (Shuffle reuses ids across framework ports) and round-robins categories so every requested section type gets a pick before doubling; `--local-assets` now appends a "Available local image assets" manifest to the brief so the model references real downloaded files; brief template allows `assets/shuffle/**` references.
- E2E v3 (`e2e-full-v3`, codex): 468KB site, 6 unique tailwind components (Trizzle headers ×1, Consulty/Nightsable testimonials, Cronos+Consulty contact, Gradia pricing, NEUB contacts, Flex headings), 5 provenance comments, 2 local Shuffle assets referenced and rendering (Cronos map + decorative SVGs). Screenshot-verified top and bottom halves — coherent, polished, no breakage.
