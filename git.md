# GIT

I follow a workflow similar to [Git Flow](http://nvie.com/posts/a-successful-git-branching-model/) with some tweaking.  Here are some high level built points.

- `master` branch should hold production ready code, each commit should ideally be tagged with a version
- main development show happen on `develop` branch
- all new self contained features should be developed in there own branch prefixes with `feature/` that are cut from `develop`
- all major features that might require multiple branches to complete should be worked from a branch prefixed with `major/feature-` that are cut of `develop`
-- all features for a major branch should be prefixed with `major/` that are cut from the associated `major/feature-` branch
- all `feature/` and `major/` branch should be merged back into the branch they were cut from and then deleted
- when `develop` has all the features needed for the next release, a branch should be cut from `develop` with the prefix `release/`
- all `release/` branches should be merged into `master` and `develop` and then deleted
- all hotfix branches should be prefixed with `hotfix/` that are cut from `master`
- all `hotfix/` branches should be merged back into `master` and `develop` 
