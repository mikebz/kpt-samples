# Overview

This is a proposed solution to http://go/Graybox-Blueprints-PoC given the current state of kpt featureset and the desire for Graybox to do several things:
1) have an update strategy for corporate or Google provided blueprints
2) use a directory tree structure for environments such as dev/test/stage
3) have a wet vs dry repo

## Context and constraints
At the time of writing `kpt` is in the middle of a rewrite and some of the v1 functionality will help making this problem easier. Also while it's possible to do some of the workflows in `kpt` they are closer to the `kustomize` philosophy.  Primarily the wet vs dry repos.

After Q1 2021 we might want to revisit this solution, but at the time we can take advantage of `kpt` update and merge while using `kustomize` hydration to populate the Graybox wet repo.

The key is being disciplined about utilizing the products for various parts use cases even though there are some overlapping features.

## Use cases

### Publishing blueprints
Publishing blueprints can be done in the Kpt format or just by having a folder of yaml that pertains to a particular object type.  One needs to be mindful of the setter and other kpt features that are designed for the hydration step.  Those features are under heavy re-design right now.  The recommendation here is to publish raw yaml in a central repo, possibly with a README.md file that outlines the intended use (make sure to update the password etc).  The CaD model assumes that either the consumer or the consuming tool is not being shielded from the actual configuration.


### Consuming blueprints
The recommended pattern here is to use kpt packaging features because of the merging and updating that kpt does really well.  The update of the "base" package is likely to be an intentional step.  While it's techncially possible to automaticaly update configuration msot of the teams prefer this to be a supervised process.

Adding a new "base" is as simple as issuing this command:
```
kpt package get sso://user/mikebz/blueprints.git/mysql bases/mysql
```
For a kustomize unaware blueprints some automation might be added to create a kustomize.yml with all the config files added to it.

The update command allows app team team to update the mysql base and even if some modifications were done locally kpt will handle simple use cases for merging the upstream changes.
```
kpt pkg update --strategy resource-merge bases/mysql
```

### Hydration pipeline
Since the requirement here is to go from dry to wet repo kustomize works really well by allowing one to set some of the common attributes and also override some elements of configuration as a patch.  The desire here for the Graybox CLI to create a dictionary of parameters that will then be used to create a kustomization file.  The danger of this parameterization is that eventually the parameters will need to contain everything that could be customizable.  A possible approach could be to create a "blueprint" for a kustomization pipeline and create new environments or database instances with those kustomizations in place, letting the user configure the exact things that will need to be customized for that particular environment.

Hydrating the config could look like this:
```
kustomize build ./overlays/test
```
which will output the kustomized yaml.  While kubectl -k can be used it seems like the final config has been deemed as necessary to preserve in the "wet" repo.  There can also be an automation created that generates a pull request to the "wet" repo. 