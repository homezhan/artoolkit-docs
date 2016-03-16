#Get involved
We have publicly available repositories for everyone to contribute to. There is the main [ARToolKit5 repo](https://github.com/artoolkit/artoolkit5 "ARToolKit5 GitHub"), the [Unity integration] (https://github.com/artoolkit/arunity5 "ARToolKit5 for Unity") and the [JavaScript integration] (https://github.com/artoolkit/jsartoolkit5 "JSARToolKit5") to name the major ones. With more open source ventures coming soon.
To get involved there are a few steps you need to do and a few procedures that take place behind the scenes.

##Check out the source code
1. To contribute to the ARToolKit codebase, no matter if fixing or enhancing a sample app or the ARToolKit codebase itself, you need to have a [GitHub](https://github.com/join?source=header-home "Join GitHub") account.
2. Always work with GitHub forked branches. Fork the public https://github.com/artoolkit/artoolkit5.git repository for the base toolkit, or https://github.com/artoolkit/arunity5.git for the Unity plugin.
  - For documentation on how to fork and on how to keep your fork up-to-date with the master see the this documentation https://help.github.com/articles/fork-a-repo/
3. We recommend setting an `upstream` remote to the main repo from your fork. With this you'll see changes to the main ARToolKit5 repo when you do a `git status`. (It just makes things easier)
  - As an example, to add the main ARToolKit5 repo as a remote, type `git remote add upstream https://github.com/artoolkit/artoolkit5.git` into your git terminal.
  - Remember to re-sync against the remote master branch often. `git fetch upstream` and `git rebase upstream/master`
4. Do your work in whatever branch you want to in your fork.
  - Work on branches that track the `upstream master` branch. `git checkout -b <<branch name>> upstream/master`
  - Try to keep your changes small, push your work remote (`git push`), and generate pull requests often. We want to avoid big bang pull requests. 
  -  Also, sync your branch often with the ARToolKit repo. `git fetch upstream` followed by `git rebase upstream/master`. Using `git rebase` will always keep local changes on the tip of the remote branch being tracked while it is constantly changing. This enables simple fast-forwards when finally merging local changes to remote master through a pull request (without [merge bubbles](https://github.com/wp-e-commerce/wp-e-commerce/wiki/Merging-Pull-Requests)).
5. When all your work is done and pushed up, synchronize your branch with the ARToolKit master repository. To do so follow these steps:
	1. Ensure that you have checked out the branch you would like to commit. You can verify this with: `git branch` and switch to your branch with `git checkout [BRANCH_NAME]` if needed.
	2. Get changes from the original repo: `git fetch upstream`
	3. Rebase your changes on top of the latest ARToolKit master changes:  `git rebase upstream/master`
	4. Be prepared that merge conflicts may result that require resolution.
	5. Commit and push again to your branch in your forked repository.
6. The way to contribute back is via a **Pull Request**. To create a **Pull Request** do the following:
  1. Log-in to you GitHub account 
  2. Select the branch you would like to be merged to the ARToolKit repository. (The branch you made the changes in.)
  3. Select the "New pull request" button and ensure that the base is set to **master** and the head is set to _the branch you would like to be merged_.
7. Done, the **Pull Request** is now in review state. 

##Review
Once you have published a merge request the ARToolKit-Team receives an email about this request. We will have a look at your changes and (if needed) enter comments to your merge request. You will get notified about those comments by email from GitHub. So please ensure that you check your GitHub emails regularly. If all comments are resolved (if any) your code will be merged into the ARToolKit repository.
Congratulations you are now a member of the growing ARToolKit-Community. 

**The ARToolKit staff is very grateful for your participation in improving and increasing the mind share of the SDK. Thanks a lot for your help to grow ARToolKit**
