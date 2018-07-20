Feature Branch Info:

[https://www.atlassian.com/git/tutorials/comparing-workflows\#feature-branch-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow)

[http://nvie.com/posts/a-successful-git-branching-model/](http://nvie.com/posts/a-successful-git-branching-model/)

Here is a breakdown from a command line perspective:

\#Create a new branch

`$ git checkout -b myfeature develop  # source branch is optional if source is current branch`

`# Push branch first time`

`$ git push -u origin <new-branch-name>`

`# List branches, * branch is active one`

`$ git branch`

`# delete feature branch`

`$ git branch -d myfeature`

`# change branches`

`$ git checkout <branchname>`

\# merge feature branch, --no-ff flag causes the merge to always create a new commit object

$ git checkout &lt;branchmerginginto&gt;

$ git merge --no-ff myfeature

