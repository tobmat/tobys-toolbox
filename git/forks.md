# Forks

## Configuring a remote for a fork

Specify a new remote \_upstream \_repository that will be synced with the fork:

```text
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```

Verify the new upstream repository you've specified for your fork:

```text
git remote -v
```

Reference: [https://help.github.com/articles/configuring-a-remote-for-a-fork/](https://help.github.com/articles/configuring-a-remote-for-a-fork/)

## Syncing a fork

Fetch the branches and their respective commits from the upstream repository. Commits to master will be stored in a local branch, upstream/master:

```text
git fetch upstream
```

.Check out your forks local master branch:

```text
git checkout master
```

Merge the changes from upstream/master into your local master branch. This brings your fork's master branch into sync with the upstream repository, without losing your local changes:

```text
git merge upstream/master
```

Reference: [https://help.github.com/articles/syncing-a-fork/](https://help.github.com/articles/syncing-a-fork/)

