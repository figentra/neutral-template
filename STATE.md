# State of figentra/neutral-template

Dated 2026-11-07. This file reports what has been shown to work, separately from what is declared.
Where it disagrees with another document, check the evidence named here, then correct that document.

## 1. What this repository is

The layout that non-product Figentra repositories start from: Figentra Flow's neutral preset with no
product code and no workspace. It holds the rendered agent setup (`.agents/`, `.claude/`,
`AGENTS.md`, `CLAUDE.md`), the GitHub setup (code owners, ruleset, forms, Quality Gate), the pinned
toolchain, git hooks, formatting, spelling, secret scanning, Renovate and the security policy. It is
a GitHub template repository (`is_template: true`). Code owner is `@figentra-usr`.

## 2. Current

| Fact                    | Value                                                                                                          |
| ----------------------- | -------------------------------------------------------------------------------------------------------------- |
| Default branch head     | `main` at `66b92ac30c11ef5a85af8b8a0d8d84a4223a96e9` (2026-11-06, #2)                                          |
| History                 | 2 commits: `Initial commit` and #2 (the layout, rendered by Flow 0.6.4)                                        |
| Versions                | no `package.json`, no workspace; `.flow/lock.json` pins Flow 0.6.4, neutral preset                             |
| Toolchain (`mise.toml`) | node 24.22.0, pnpm 12.16.1, oxfmt 0.71.0, cspell 10.4.0, gitleaks 8.30.1, actionlint 1.7.12, osv-scanner 2.7.0 |
| Tags and releases       | none                                                                                                           |
| Licence                 | MIT, Figentra Technologies L.L.C                                                                               |

## 3. Proven by a real run

- CI Quality Gate passed on `66b92ac`: run 42260142893. Steps that ran: gitleaks, oxfmt, cspell,
  actionlint, Flow gate. Commit messages (commitlint) was skipped.
- That is the only workflow run on `main`.

## 4. Not proven

- No repository has been created from this template and checked here; the Quick start
  (`gh repo create --template`, `mise install`, `fflow sync`) has no recorded run.
- `.github/rulesets/main.json` is declared but not applied: the GitHub API lists 0 rulesets on this
  repository and `main` has no branch protection (checked 2026-11-07).
- `fflow-approve.yml` has never run on `main`.
- The README's Docs badge links Stackra ADR 0528
  (`docs.stackra.figentra.com/adr/0528-neutral-and-stackra-templates`), which returns 404 (checked
  2026-11-07).
- The README's Development section says to install dependencies with the repository's package
  manager; this repository has no package manifest, so there is nothing to install.

## 5. Map

| Path                        | One line                                                                                             |
| --------------------------- | ---------------------------------------------------------------------------------------------------- |
| `.agents/`                  | 3 agents (ci, git, tracker steward), 1 rule (worktrees), 10 `flow-*` skills, `hooks/fflow-guard.mjs` |
| `.claude/`                  | the Claude Code settings Flow renders                                                                |
| `.github/`                  | CODEOWNERS, ruleset, issue and PR forms, `ci.yml`, `fflow-approve.yml`                               |
| `.flow/`                    | `lock.json` and `readme.yml`, the data `README.md` is rendered from                                  |
| `docs/`                     | the repository's own docs; only `docs/README.md` today                                               |
| `flow.config.json`          | the Flow preset (`neutral`) and the apps owner                                                       |
| `mise.toml`, `lefthook.yml` | pinned tools and git hooks                                                                           |

Authoritative documents: `flow.config.json` and `.flow/readme.yml` are the sources; `AGENTS.md`,
`CLAUDE.md`, `README.md` and `lefthook.yml` are rendered from them by `fflow sync`. Framework
decisions are Stackra ADRs, cited and not copied. This repository has no ADRs of its own.

## 6. Open risks

- Main CI: green (run 42260142893).
- Open pull requests: 0 besides this one.
- Branches other than `main`: 1 (`layout/initial`, 3 ahead and 1 behind; #2 landed its content).
- Infisical references: 7 lines in 2 files: 6 in `.agents/hooks/fflow-guard.mjs` (rendered by Flow)
  and 1 in `.github/CODEOWNERS` (`**/.infisical.*`).
- Retired name `figentra-flow`: `.github/CODEOWNERS` line 21 still owns
  `/figentra-flow.config.json`. `CONTRIBUTING.md` and `cspell.config.yaml` mention it only to forbid
  it.
- `main` is unprotected (no ruleset, no branch protection); nothing else blocking.
