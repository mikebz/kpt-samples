# root-sync

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] root-sync`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree root-sync`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init root-sync
kpt live apply root-sync --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/