# Repository Agent Instructions

AutonomyML (Autonomy Model Language) repository: open specification and architecture research (`AutonomyML Overview.md`, `docs/`, `openspec/`), standalone Part 1 `CapabilitySpecification` and Part 2 `CapabilityBinding` JSON examples (`examples/`), and static website (`src/`, `scripts/`, `package.json`). Coordinated across coding agents with `ateam`.

Guidance for coding agents. Codex, Gemini, and Antigravity load this file as `AGENTS.md`; `CLAUDE.md` imports it (`@AGENTS.md`), keeping a single copy strictly under 24,000 bytes.

## Ponytail decision ladder

You are a lazy senior developer. The best code is the code never written. Solve the whole problem with the least new code, and end each task conclusion and each handoff with 1–2 lines stating **what you skipped or did not check** and **any residual risk**. Acknowledgements and progress updates need no footer, but they still name a blocker, a failed or unavailable check, or a changed risk when one arises.

1. **Does it need to exist?** Skip unrequested features, options, and abstractions.
2. **Already in this codebase?** Reuse existing helpers, components, and conventions.
3. **Standard library or platform feature?** Prefer the project language’s standard library and native platform features.
4. **Installed dependency?** Use what is already in `go.mod` / `package.json`; never add a dependency for a few lines.
5. **Readable at a glance?** Prefer flat, obvious code over clever one-liners.
6. **Minimum complete change:** Finish every caller, test, and fixture your change touches. Mark any intentional deferral with `// shortcut: <the limit>, <when to upgrade>`.

## Rules and what enforces them

### 1. Ponytail decision ladder and code discipline

| Gate | Rule | Where |
| --- | --- | --- |
| `verify+review` | Follow the 6-step Ponytail decision ladder; no unrequested abstractions, wrappers, or dependencies | `.agents/skills/ponytail/SKILL.md` |
| `verify+review` | Every intentional deferral uses `// shortcut: <the limit>, <when to upgrade>`, scanned by `ateam state debt` | `.agents/skills/ponytail/SKILL.md` |
| `verify+review` | Non-trivial logic ships with a test using an independent oracle and proven able to fail via non-destructive mutation check (`ateam mutate` for Go or `cp` + SHA-256; never `git checkout`/`restore`/`stash`/`reset`), reporting `detection`, `survivor`, `invalid`, or `inconclusive` | `.agents/protocol.md` |
| `verify+review` | Changes with interacting inputs, stated laws (round-trip, idempotence), or order-dependent histories record whether generated checks (`testing.F` / PBT) are used or why examples suffice, prove boundary reach and assertion activation, and check histories against a reference model | `.agents/protocol.md` |
| `verify+review` | Every Go Test/Fuzz/executable Example and Vitest test carries attached spec references (`// spec:` or `//aip:verifies`) resolved by `ateam test-spec`; syntactic attribution does not prove semantic coverage | `ateam test-spec`; `.agents/protocol.md` |
| `verify` | Go packages (when present) pass `gofmt`, `go vet`, and `revive` with zero warnings | `Taskfile.yml` |
| `review` | Task conclusions and handoffs end with 1–2 lines stating what was skipped/not checked and any residual risk; acknowledgements and progress updates need no footer but still name blockers, failed or unavailable checks, and changed risks | `.agents/skills/ponytail/SKILL.md` |

### 2. Hooks, MCP budget, and multi-agent parity

| Gate | Rule | Where |
| --- | --- | --- |
| `verify` | `AGENTS.md` stays under 24,000 bytes, `CLAUDE.md` only imports `@AGENTS.md`, and rule row counts match `.agents/rules-index.md` | `.agents/README.md` |
| `verify` | Canonical skills in `.agents/skills/*/SKILL.md` have matching thin adapters in `.claude/skills/` and `.gemini/commands/` | `.agents/README.md` |
| `verify` | Hook configs in `.claude/settings.json`, `.codex/hooks.json`, `.gemini/settings.json`, and `.agents/hooks.json` map native events to `ateam hook`; with `ATEAM_HOOK_SCOPE=user`, `ateam doctor` also accepts one complete local or user-scope file (`.claude/settings.local.json`, `~/.claude/settings.json`, `~/.codex/hooks.json`, `~/.gemini/settings.json`) and names the file under `hook_sources` | `.agents/README.md` |
| `verify` | `ateam mcp` exposes only the 2 multiplexed tools (`ateam_state`, `ateam_task`) with `<300` total schema tokens | `.agents/README.md` |
| `verify` | `ateam hook` executes normalized lifecycle events in `<10ms` target budget (`doctor` warns `>10ms`, fails `--check` `>100ms`) with zero external runtime dependencies | `.agents/README.md` |

### 3. State, OpenSpec, Forge (GitHub/Gitea), and Definition of Done

| Gate | Rule | Where |
| --- | --- | --- |
| `review` | Clarify Deliverable, Scope/non-goals, Definition of Done, and Stop boundary before mutating state | `.agents/protocol.md` |
| `verify+review` | Shared state syncs with GitHub (`gh`/API) or Gitea (`tea`/API v1) and git worktrees, cached in gitignored `.ateam/state.json` | `.agents/protocol.md` |
| `verify` | OpenSpec changes/specs validate via `spec:check`, and `Hold:` / caveats (`HALT`, `RED`, `BLOCKED`, `WONTDO`, `OPEN-Q`) are parsed by `spec:queue` | `openspec/` |
| `review` | Non-trivial work's OpenSpec `proposal.md` stays one page (≤ 60 lines; `spec:check` warns past it) and carries `Approved-by:`, empty until the owner fills `<name> (<YYYY-MM-DD>)`; the change's first task holds `Hold: OPEN-Q proposal awaits owner approval` until the owner removes it in the same edit, and an agent whose Stop boundary is proposal approval stops there and hands off | `.agents/protocol.md` |
| `review` | A non-trivial change declares the `quick` or `design` track at Clarify; `design` is required when it adds a spec Requirement, touches more than one capability under `openspec/specs/`, adds exported surface reachable from an adopting repository, or touches a boot path, durability/ack behavior, or a gate file, and then carries a `design.md` (≤ 120 lines; `spec:check` warns past it) drafted by the read-only `design` skill and approved with the proposal under the one `OPEN-Q` hold | `.agents/protocol.md` § Clarify; `.agents/skills/design/SKILL.md` |
| `verify` | `task verify` runs `ateam doctor --check`, OpenSpec validation (`spec:check`), standalone example JSON checks (`examples:check`), and website build (`site:build`) | `Taskfile.yml` |
| `verify+review` | Review requires an independent reviewer not weaker than every implementer by model tier, then effort band, optional provider separation and current trusted-base evidence; the dormant configured path adds scoped owner ceiling exceptions | `ateam review`; `.agents/contracts/reviewer.md` |
| `merge:check+review` | Non-draft code PRs (any file outside `.md` and `openspec/**/*.{md,yml,yaml,json}`, plus `.claude/agents/` and `.agents/contracts/`) carry `implemented-by:` and `reviewed-by:` each naming an agent (`claude`, `codex`, `gemini`) with its model and, once `.agents/review-policy.json` exists, native effort in parentheses (`claude (opus, high)`), the reviewer not weaker by tier then band (`ateam review compare`) and a different agent only when the policy sets `cross_provider`, plus a PR comment review record (`reviewed-by: <agent>` or `### Independent Cross-Agent Review`) naming a PR commit with only clean `main` merges or docs-only commits after it, checked alongside active `main` ruleset and open `class:flake` issues by `ateam review gate` | `ateam review gate`; `.agents/protocol.md` |
| `review` | A PR archives its completed OpenSpec change before it is marked ready; once its required check is green on an up-to-date branch and the squash auto-merge (GitHub or Gitea) has landed, the claiming agent removes its worktree and remote branch (the `main` run is informational), and a review checkout is removed when its record is posted | `.agents/protocol.md` § Close; `ateam state pickup` worktree labels |

