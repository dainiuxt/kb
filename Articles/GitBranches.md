# Working with `git` branches

[Link to original post](https://www.nobledesktop.com/learn/git/git-branches)

### See What Branch You're On

    git status

### List All Branches

`NOTE:` The current local branch will be marked with an asterisk (\*).

To see local branches, run this command:

    git branch

To see remote branches, run this command:

    git branch -r

To see all local and remote branches, run this command:

    git branch -a

### Create a New Branch

    git checkout -b my-branch-name

You're now ready to commit to this branch.

### Switch to a Branch In Your Local Repo

    git checkout my-branch-name

### Switch to a Branch That Came From a Remote Repo

1. Get a list of all branches from the remote, run this command:

    `git pull`

2. Then switch to the branch:

    `git checkout --track origin/my-branch-name`

### Push to a Branch

If your local branch does not exist on the remote, run either of these commands:

```
git push -u origin my-branch-name
git push -u origin HEAD
```

`NOTE:` HEAD is a reference to the top of the current branch, so it's an easy way to push to a branch of the same name on the remote. This saves you from having to type out the exact name of the branch!

If your local branch already exists on the remote, run this command:

    git push

### Merge a Branch

1.  You'll want to make sure your working tree is clean and see what branch you're on. Run this command:

    `git status`

2.  First, you must check out the branch that you want to merge another branch into (changes will be merged into this branch). If you're not already on the desired branch, run this command:

    `git checkout master`

    `NOTE:` Replace `master` with another branch name as needed.

3.  Now you can merge another branch into the current branch. Run this command:
    
    `git merge my-branch-name`
    

### Delete Branches

To delete a remote branch, run this command:

    git push origin --delete my-branch-name

To delete a local branch, run either of these commands:

    git branch -d my-branch-name
    git branch -D my-branch-name

`NOTE:` The -d option only deletes the branch if it has already been merged. The -D option is a shortcut for --delete --force, which deletes the branch irrespective of its merged status.