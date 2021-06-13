# Merge Branch

A GitHub Action for keeping two branches in sync by merging in any `source`
branch changes.

```
pr-mpt/actions-merge-branch@v0
```

## Inputs

| ID | Description | Default | Examples |
| ---- | ----------- | ------- | -------- |
| **`from`** | **Branch to merge into the current branch** | **<kbd>required</kbd>** | **`main`** |
| `author` | Merge commit author | GitHub Actions<sup>[1]</sup> | `Alice <alice@example.com>` |
| `strategy` | Merge strategy with options | `recursive -Xtheirs` | `recursive`<br/>`recursive -Xours` |
| `push` | Push merge commit to origin? | `true` | `true` `false` |

[1] `github-actions[bot] <41898282+github-actions[bot]@users.noreply.github.com>`

## Outputs

No outputs.

## Examples

### Synchronise `release` branch with `main`

Every push to `main` is synchronised to the `release` branch by merging in any
changes.

```yaml
on:
  push:
    branches:
      - "main"

jobs:
  synchronise-release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          ref: "release"
          fetch-depth: 0
      - uses: pr-mpt/actions-merge-branch@v0
        with:
          from: "origin/main"
```
