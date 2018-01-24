GIT INFO



Feature Branch Info:

[https://www.atlassian.com/git/tutorials/comparing-workflows\#feature-branch-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow)

[http://nvie.com/posts/a-successful-git-branching-model/](http://nvie.com/posts/a-successful-git-branching-model/)



Here is a breakdown from a command line perspective:

\#create a new branch: git checkout -b new\_branchexisting\_branch

\#example

$ git checkout -b myfeaturedevelop  \# source branch is optional if source is current branch



\# push branch first time, then normal after that

$ git push -u origin &lt;new-branch-name&gt;



\# determine active branch

$ git branch



\# merge feature branch, --no-ffflag causes the merge to always create a new commit object

$ git checkout &lt;branchmerginginto&gt;

$ git merge --no-ffmyfeature



\# delete feature branch

$ git branch -dmyfeature



\# change branches

$ git checkout &lt;branchname&gt;



\# push changes back

$ git push



