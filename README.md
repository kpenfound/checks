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
