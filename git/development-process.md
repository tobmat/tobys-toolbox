### When multiple developers are working on a repository



1. Start with the master and develop branch. 

2. Those who will develop will branch out his own feature branch from develop branch.

3. Completed feature branch will be merged to the develop branch by doing a pull request.

4. The release branch will be created once the develop branch is ready to be tested in our test environment.

5. All bug fix from the release branch will be merged back to the develop branch.

6. Once all bug fixes are done in the release branch it will be merged to the develop and the master branch where the PROD environment will be taking it’s scripts.

7. Once release is complete, delete the release branch both locally and via github ui.  \(Note: Can keep branch open if continuing to do smaller changes within repo.  Larger changes should have own feature branch\)

8. Hot fix branch should only be created if we found issues in PROD.

9. Once hot fix is done, it will be merged back to PROD and Develop



Rules to be followed:



1. No feature should branch out from master.

2. No feature or develop can be merged to the master.

3. No feature can be merged to develop while a release is ongoing.



