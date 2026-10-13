# commit-test

[中文](README.md) · [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Selective integration verification driven by git commits or working-tree changes: analyze the impact surface, prepare the environment, verify changed behavior through real pages, and record reusable module knowledge and per-run evidence separately. P0 smoke checks and change acceptance are tracked independently, so necessary scenarios are never skipped just because a commit baseline already exists.

## Usage

Trigger it with requests like "test the recent commits/changes", "run integration tests", "verify this batch of commits / this change", or "regression check". It is not for writing unit tests or pure code review. The five-stage workflow (scope → impact analysis → environment → execution → report) and its constraints live in [SKILL.md](SKILL.md); phase details are loaded progressively from [phases/](phases/).

## Structure

```
SKILL.md          Entry point: workflow, capabilities, and authorization boundaries (progressive loading)
phases/           Details: analysis (scope & impact) / env (environment) / execute (browser execution)
TEMPLATE.md       Template for module knowledge files
projects/         Local accumulation area (git-ignored, not synced)
  └── <project>/
      ├── env.md             Linked repos, start commands, addresses, credential sources, and environment limits
      ├── tested-commits.md  Per-repo versions with scope/depth/scenario coverage and relevant dirty state
      ├── modules/*.md       Stable knowledge: trigger scope, call chains, entries, scenarios, and evidence criteria
      └── runs/*.md          Actual operations, results, evidence, and uncovered items for each run
```

## Deployment (local machine chain)

This repository is the skill source directory, exposed to hosts via local junctions:

```
D:\projects\CommonAssets\skills\commit-test          (source, git-synced)
  ├→ C:\Users\admin\.codex\skills\commit-test
  └→ C:\Users\admin\.config\opencode\skills\commit-test
       → C:\Users\admin\.zcode\skills\commit-test
```

## Sync semantics

- **In git**: SKILL.md, phases/, TEMPLATE.md, and both READMEs (methodology, synced across machines)
- **Not in git**: `projects/` (local environment, baselines, module knowledge, and run evidence; excluded by `.gitignore`). An ignored directory is not a credential store — reports never copy passwords or tokens.

After cloning this repository on a new machine, the first run initializes `projects/<project>/` on the spot.

The browser layer uses whatever tooling the current host actually provides; no specific auxiliary skill is required. Detailed execution rules, result evidence, and baseline updates are documented in [SKILL.md](SKILL.md) and its phase files.
