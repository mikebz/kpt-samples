# basens

## Description
kpt package for provisioning namespace

## Usage

### Fetch the package
`kpt pkg get https://github.com/mikebz/kpt-samples/basens basens`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree basens`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init basens
kpt live apply basens --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
