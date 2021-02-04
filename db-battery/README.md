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
The recommended pattern here is to use kpt packaging because of the merging and updating that kpt does really well.  The update of the "base" package is likely to be an intentional step.  While it's techncially possible to automaticaly update configuration msot of the teams prefer this to be a supervised process.