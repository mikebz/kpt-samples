# cluster-config

## Description
RootSync and cluster configuration for kgr

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] cluster-config`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree cluster-config`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init cluster-config
kpt live apply cluster-config --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
