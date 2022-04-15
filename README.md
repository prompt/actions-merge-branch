# Merge Into Current Branch

A GitHub Action for keeping two branches in sync by merging in any `source`
branch changes using `git` locally -- not the GitHub API.

```
pr-mpt/actions-merge-branch@v2
```

## Inputs

| ID | Description | Default | Examples |
| ---- | ----------- | ------- | -------- |
| **`from`** | **Branch to merge into the current branch** | **<kbd>required</kbd>** | **`main`** |
| `author` | Merge commit author | GitHub Actions<sup>[1]</sup> | `Alice <alice@example.com>` |
| `strategy` | Merge strategy with options | `recursive -Xtheirs` | `recursive`<br/>`recursive -Xours` |
| `commit` | Commit changes? | `true` | `true` `false` |
| `push` | Push merge commit to origin? | `true` | `true` `false` |

[1] [`github-actions[bot] <41898282+github-actions[bot]@users.noreply.github.com>`][users/github-actions]

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
      - uses: pr-mpt/actions-merge-branch@v2
        with:
          from: "origin/main"
```

[users/github-actions]: https://api.github.com/users/github-actions%5Bbot%5D
