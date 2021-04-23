---
description: Cheat sheet
---

# Git

#### \# git stash

```bash
# stash files locally
git stash

# retrieve stashed files
git stash pop
```

#### \# push changes to external repo

`$ git push`

#### \# pull changes from external repo

`$ git pull`

#### \# see git remote info

`$ git remote -v`

#### \# git commit info

`$ git log`

#### `# compare files from 2 branches`

```text
git diff dev master -- scripts/basic_win_boot_chef.ps1
```

#### Pull latest changes to feature branch

```text
git checkout <feature branch>
git merge master
```

