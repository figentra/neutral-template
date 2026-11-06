# Contributing

This repository follows the neutral Figentra layout (Stackra ADR 0526 and 0528): the root holds
configuration and docs only, and any code lives in members or under one `tools/` folder with a
README. The short version:

1. `mise install` pins every tool (`mise.toml`). There is no workspace install unless the repository
   adds one.
2. Work on a branch named after its issue (`figentra/sta-<n>-<slug>`); `fflow start STA-n` makes the
   worktree under `.claude/worktrees/`.
3. Use conventional commits (`.commitlintrc.yaml`).
4. Never hand-edit what `fflow sync` renders (`AGENTS.md`, `CLAUDE.md`, `.agents/`, `.claude/`,
   `lefthook.yml`, `.mcp.yaml`, `README.md` and the `fflow-*` workflows): change `flow.config.json`,
   `.flow/readme.yml` or `.flow/overrides/`, then run `fflow sync`. `fflow gate ci` fails on a hand
   edit.
5. Secret values never go in a file. A workflow that needs one decrypts its figentra/secrets scope
   with core's pinned `secrets-decrypt` action (Stackra ADR 0525).

## Change risk

Each pull request states its change risk, R0 to R3
([Stackra ADR 0120](https://docs.stackra.figentra.com/adr/0120-sdlc-spec-location-lanes-and-change-risk)):
R0 docs and comments, R1 a contained change, R2 a change others depend on, R3 security, secrets,
`.github/` or anything the code owners hold. R3 needs a code owner's review.

## Layout

`stackra validate --repository` compares the root with this template. A repository that needs
another root entry declares it in package.json `stackra.layout.allow`, with the reason. A root
`src/`, a `scripts/` or `bin/` folder and the retired name `figentra-flow` are never allowed.

## Formatting and spelling

- oxfmt formats Markdown, YAML and JSON (`.oxfmtrc.jsonc`); lefthook checks staged files and CI
  checks the rest.
- Spelling is British English with US English accepted (`cspell.config.yaml`); add a project word
  there, never inline.

## Conduct

Report unacceptable behaviour privately to a maintainer (see `SECURITY.md` for the address).
