# GitHub action to run Dagger Checks

## Usage Examples

### `dagger checks`

```yaml
- name: Check
  uses: dagger/checks@v1.0.0
```

### `dagger checks '**/lint'`

```yaml
- name: Check
  uses: dagger/checks@v1.0.0
  with:
    filter: '**/lint'
```

### `dagger checks` with Dagger vX.Y.Z and a Dagger Cloud Token

```yaml
- name: Check
  uses: dagger/checks@v1.0.0
  with:
    version: 'vX.Y.Z'
    cloud-token: ${{ secrets.DAGGER_CLOUD_TOKEN }}
```

### Dynamic matrix: run each check as its own job

Use `list: true` to discover available checks, then run each one independently with its own runner:

```yaml
jobs:
  list-checks:
    runs-on: ubuntu-latest
    outputs:
      checks: ${{ steps.list.outputs.checks }}
    steps:
      - uses: actions/checkout@v4
      - uses: dagger/checks@v1.0.0
        id: list
        with:
          list: true

  run-check:
    needs: list-checks
    runs-on: ubuntu-latest
    strategy:
      matrix:
        check: ${{ fromJSON(needs.list-checks.outputs.checks) }}
    steps:
      - uses: actions/checkout@v4
      - uses: dagger/checks@v1.0.0
        with:
          filter: ${{ matrix.check }}
```
