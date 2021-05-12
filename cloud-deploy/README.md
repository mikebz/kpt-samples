# cloud-deploy

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] cloud-deploy`
Details: https://kpt.dev/reference/pkg/get/

### View package content
`kpt pkg tree cloud-deploy`
Details: https://kpt.dev/reference/pkg/tree/

### Apply the package
```
kpt live init cloud-deploy
kpt live apply cloud-deploy --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/live/
