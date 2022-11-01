Turn around your Git mistakes in 17 ways
========================================

[Link to the original post](https://dev.to/smitterhane/turn-around-your-git-mistakes-in-17-ways-2mn1)

### [](#1-stop-tracking-a-tracked-file)1\. Stop tracking a tracked file

You have a `node_modules` folder that you do not want to be tracked by git.  
You committed `node_modules` folder and now you realize that you forgot to ignore it using a `.gitignore` file. You add the `.gitignore` file and list the `node_modules` folder in it then commit.  
  
But still Git is tracking it(`node_modules`). This is because, once a file has been added and committed to Git database, Git will continue tracking changes to it.

So you want to stop Git from tracking the `node_modules` folder.  
  
Just run:  

       git rm -r  --cached node_modules
    

### [](#2-modify-the-last-commit)2\. Modify the Last Commit

You have committed to your local Git Database. Thereafter you realize that you have forgotten to include file changes to that commit(you may have not saved the file). Or you add a new file that you want it tied to the same commit you have committed most recently.

Git can unlock the previous commit and allow you to add your new file.  
  
Just do this:

First, you add the missing file using:  

       git add newfile.ts
    

Then, run:  

       git commit --amend --no-edit
    
The `--no-edit` flag amends the commit without changing the commit message.

### [](#3-modify-the-last-commit-message)3\. Modify the Last Commit Message

This scenario is similar to the one above. But this time, you have commited to git _and you are not very happy with the commit message you specified_. You want the message to have more meaning describing what you have done.

Again Git is forgiving to let you fix your previous crappy commit message.  
  
Simply run:  

       git commit --amend -m "Phew! A better commit message this time"
    
### [](#4-discarding-all-changes-in-your-working-directory)4\. Discarding all Changes in your working directory

You are working on your project. For example, you may be refactoring your code to follow better patterns and clean code principles. While refactoring, you break a functionality in the application and cannot get your head around what really went wrong. You now want to go back to the previous state(commit) where the application was working fine so that you can find your bearing again.

So you want to discard all the uncommitted changes you have made and restore your Git working tree back to the state it was in when the last commit took place.  
  
Use the command:  

       git restore .

_**Note:** This command restores your working copy to the most recent commit in your local git database. Changes that you have not committed will be lost permanently._

### [](#5-discard-all-changes-made-to-a-file)5\. Discard all changes made to a file

You have modified your files in your local git repo. You later realize that changes you made to a particular file(`connect.js`) are not so intelligent and should be discarded. But you want to keep changes made to other files.

So you want the file `connect.js` to go back to the state it was in the previous commit.  
  
This is possible with Git:  

       git restore connect.js

### [](#6-restore-a-file-to-an-old-version-back-in-time)6\. Restore a file to an old version back in time

Unlike the above command, In this case you want a particular file in your project to go back to a state that is deeper back in time than the previous commit.

So for example if version 3 was your previous commit, you want this particular file to appear as it was in version 2 which is earlier than version 3.

With Git:

Find and copy the _commit hash_ back in time you want:  

       git log

Then:  

       git restore --source `commit-hash` <filename>

That simple, right?

### [](#7-recover-a-deleted-filepreviously-committed)7\. Recover a deleted file (previously committed)

You are making new changes to your project and you see an obsolete file. You go ahead and delete the file so you free up space. Sometime later you realize that you need the file you just deleted.

To recover your file:  

       git restore deleted-file.css

This will present the file to you as it was in the previous commit.

### [](#8-discard-all-changes-in-your-local-repo-to-exact-state-in-remote)8\. Discard all changes in your local repo to exact state in remote

You have made a couple of changes and commits in your local repo branch. You have rewired and now you are asking yourself, "Why did I even make these changes in the first place?"

So you want to forget everything on your current local branch and make it exactly the same as what is in the remote's main branch.  
  
Just undo like:  

       git reset --hard origin/main
    



_**WARNING**: Uncommitted changes will be lost permanently._

### [](#9-delete-untracked-files)9\. Delete Untracked Files

You have created several new files in your project and also modified some files. You have changed your approach and you now decide that you no longer need any of these new files you have created but stick with the modified file changes.

Git provides you a command to remove untracked files:  

       git clean -f
    



The `git clean` command requires a `-f` flag implying the force directive(also `--force`). Since this operation entails deleting untracked files, it has to require that you are sure about what you are doing because getting rid of uncommitted work in Git is _undoable_.  

**By default this command will not remove untracked folders or files specified by `.gitignore`**. Specify the `-x` option to cause the removal of ignored files.  
  
Also **`git clean` will not operate recursively on directories**. This is another safety mechanism to prevent accidental permanent deletion.  
  
To also remove directiories, use `-d` flag like:  

       git clean -df
    



This will clean untracked files and directories, but will not remove the ones listed in `.gitignore` file.

### [](#10-switch-a-commit-to-a-different-branch)10\. Switch a commit to a different branch

The project has evolved and you are currently working on two features: adding _newsletter_ and fine-tuning _footer-layout_. You have created two separate branches: `newsletter` and `footer-layout`, dedicating each branch to the associated feature: _newsletter_ and _foooter-layout_ respectively.  
  
You are currently adding _newsletter feature_ and do some commits from the `newsletter` branch. The next time you come back to your project, you want to work on the _footer-layout_ feature and you forget to switch to the associated `footer-layout` branch. You add the _footer-layout_ feature from the wrong `newsletter` branch and commit to it.  
  
Later, it comes to your **attention** that the commit you _added to the `newsletter` branch actually belongs to the `footer-branch`_.

So you want the commit adding _footer-layout feature_ moved from the `newsletter` branch to its rightful `footer-layout` branch.  
  
This is what to do in Git:

Checkout the `newsletter` branch:  

       git checkout newsletter
    



Find and copy the _commit hash_ of the commit that added the _footer-layout feature_. Run the command:  

       git log
    



Checkout the rightful branch you want to apply with this commit. In our case:  

       git checkout footer-layout
    



Then apply the commit:  

       git cherry-pick `commit-hash`
    



Then checkout the `newsletter` branch:  

       git checkout newsletter
    



And strip it off this unwanted commit, which is the commit that adds the _footer-layout_:  

       git reset HEAD~1 --hard
    



`HEAD~1` means that we are resetting our `newsletter` branch _to move one commit behind the most recent commit and rid the commit we have moved away from_. Remember in our case, the latest commit on this `newsletter` branch was the one with _footer-layout feature_.

### [](#11-resurrect-a-deleted-branch)11\. Resurrect a deleted branch

You think you do not need a feature branch anymore and you swing the trash can on it(delete it). Next time, you are alarmed deleting it was a mistake. Now you are in _"panic mode"_. You want to impossibly go back in time and get it back.

So you want to get back your deleted branch.  
  
This is how you can recover your deleted branch:

Find and copy the _commit hash_ of your deleted your branch which will be listed when you run the command:  

       git reflog
    



Then recreate your branch as:  

       git branch <branch-name> <deleted-branch-commit-hash>
    



This will recreate a branch that will contain all the work upto the _<deleted-branch-commit-hash>_. If _<deleted-branch-commit-hash>_ is not the latest work in the deleted branch, you can still find new _commit hash_ until you get the one with your latest work. Type `git branch` and you will see your previously deleted branch listed again. This works even if the branch was deleted in origin(remote).  
  
Also if the _<branch-name>_ is not the name of what you want, simply rename it as `git branch -m <branch-name> <new-branch-name>`.

Needless to say, **the key to successfully bring back your deleted branch is to _find the right commit hash, so name your commits intelligently_**; it helps alot.

### [](#12-rewindundo-an-erroneous-commit)12\. Rewind/undo an erroneous commit

Your team has rolled out a new version of a project. You are all certain all the new features added are an _absolute master-class_. Just moments later, an urgent call from the team lead dictates that the new version rolled out has a critical flaw and needs to be fixed right away. The engineering team needs to act urgently and sitting down to find the flaw is not a timely response to an urgent matter.  
  
One of the quickest response is _to undo the changes to the error prone release_.

So you want to undo the changes done to a commit.  
  
This is how to go about it in Git:

Find and copy the _commit hash_ of the commit you want to undo changes(the broken commit):  

       git log
    



Revert changes specified by that commit:  

       git revert <broken-commit-hash>
    



`git revert` creates a **new commit with the reverted(inverse) changes**. All the changes specified in the _broken commit will be rolled back(undone)_ in the new commit. For instance, anything removed in _broken commit_ will be added in the _new commit_ and anything added in the _broken commit_ will be removed in the _new commit_. A default editor will pop up with default commit message for the _"revert commit"_ about to be created. You can modify is you so wish.

### [](#13-undo-a-git-merge)13\. Undo a Git Merge

You are happy with new changes in `feature` branch. You feel ready to merge `feature` branch to your `main` branch. So from your `main` branch, you merge `feature` branch and push your new changes to remote repository.

Moments later, you realize that merge was really _not_ a pretty move at all.

So you want to undo the merge. Git has you covered.

Start by checking out the `main` branch:  

       git checkout main
    



Then run `git log` to get the _commit hash_ of the _merge commit_.  

       git log
    



Then revert like:  

       git revert -m 1 <merge-commit-hash>
    



Branches in a merge are the parents of that merge.  
  
Usually you cannot revert a merge because _git_ does not know which side(parent) of the merge should be considered the mainline. `git revert -m 1` specifies the parent number of the mainline and _allows revert to reverse the change relative to the specified parent_.

Typically, the parent that gets recorded first during a `git merge` is the branch you were on when you merged. Which in our error case here, we merged `feature` branch while checked out on `main` branch. So `-m 1` specifies the `main` branch.

### [](#14-rollback-to-an-older-version)14\. Rollback to an older version

You can rollback your project to a version back in time. This can also be a response to an erroneous commit: _whereby you want to go back to a version that was working correctly before the recent broken commit_.

_**WARNING**: The git command shown here rewrites history. This is not suitable when collaborating on a software project with others._

So you want to get to a previous version of your project by rewinding your repository's history.  
  
In git:

Find and copy the _commit hash_ you desire your project to rewind to:  

       git log
    



Reset your repository to that state specified by _commit hash_:  

       git reset --hard `commit-hash`
    



`git reset` moves the `HEAD` pointer(and thereby your working tree) to an older version(_`commit-hash`_).  
Commits that come after this version are **removed from the project's history**.

The `--hard` flag will reset the staging area and working tree.

Using the `--mixed` flag like: `git reset --mixed `commit-hash``, will reset your repo back to specified _commit hash_ preserving files in your working tree. Files that were in later commits but not in the commit we've reset to, will become `untracked` files.  
  
The `--mixed` flag has a close cousin `--soft`, with the difference being the way they handle the index(staging area).

The `--mixed` flag will reset the staging area(index) but not the working tree. So _to add untracked files in the next commit, you will have to `git add` then `git commit`_.  
  
The `--soft` flag will neither reset the staging area nor the working tree. So _to add untracked files in the next commit, you only have to `git commit`_.

### [](#15-modify-an-old-commit-message)15\. Modify an old commit message

You are glad with the progress of your project. You are going through your project history. You notice a _commit message_ that is blatantly vague.

So you want to change this message to a better message depicting logical semantics(just a message with better explanation).  
  
In Git, you can edit a _commit message deeper in history_ with _interactive rebase_:

Find and copy the _`commit hash`_ of the commit you want to change its _commit message_:  

       git log
    



Open a rebase interactive session:  

       git rebase -i commit-hash
    



An editor will pop up.

From sample interactive rebase session above, you see that there is a typo on line 1: `pick 21c21b6 udating`. Let's fix this typo and provide a better descriptive message.

In the editor only specify which actions you want to perform. It can be tempting to rewrite the commit message right now, but that won’t work; _`rebase -i` ignores everything after the SHA(commit hash) column_. The text after that is really just to help you remember what the _commit hash_ is all about.

Since you want to preserve the contents of the commit but edit the commit message, specify `reword` action command against the commit you want to change its message; simply just replace the word `pick` in the first column with the word `reword` (or just `r`).

Then save and close the editor.  
  
Finally git opens an editor for you to change the commit message. Change the commit message to a better one.

You can finally save and close your editor. The commit will be updated with the new commit message.

### [](#16-delete-an-old-commit)16\. Delete an old commit

An old commit may be bothering you and you want it plucked out from your project history.

So you want this commit to no longer appear in your project history.  
  
You can delete this commit like:

First, find and copy the _`commit hash`_ of the doomed commit.  

       git log
    



Then:  

       git rebase -i commit-hash
    



Specify a `drop` action verb for deleting the commit.

Save and close the editor. The doomed commit is plucked out from the project history.

### [](#17-edit-an-old-commit-to-add-new-changes)17\. Edit an old commit to add new change(s)

A situation may occur where you want to add a change to your project. _But this change is relevant to a commit back in time_ when you were handling a specific change better described by the commit message for that commit.  
  
**For example**, your project has evolved by several commits and lets presumably brand the most recent commit as **version 5** of your project. You have created a `file.html`. You want this file to be part of a previous commit deeper in history, probably at **version 2** of the project.

In Git, you can meld new change(s) into a commit back in time, hence editing an old commit.  
  
These are the steps:

Find and copy the _`commit hash`_ of the commit you want to mark for editing:  

       git log
    



Start a rebase interactive session:  

       git rebase -i "commit-hash^"
    



_**NOTE** how we are appending a caret(`^`) at the end of the **`commit-hash`**_. This way we are telling Git we would like to go back to the original chronology of commits after we are done editing this marked commit. Because when you run `git rebase -i "commit-hash^"`, `git log` will show the marked _`commit-hash`_ as the _most recent commit_.

Running this command, a default editor will pop up. Modify the action verb `pick` to `edit` in the line mentioning our _`commit-hash`_.

Save and close the editor.

Your working tree and project history is now at the state when you made this commit earlier. Run `git log` and you will see that _`commit-hash`_ is now your most recent commit. You still have the file you created (`file.html`) in your working tree and this is a good chance to ammend it to the most recent commit. Remember at this point, the most recent commit is the commit you want to edit.  
  
So go ahead and ammend like:  

       git add file.html
       git commit --amend --no-edit
    



Now to take the project history back to normal order:  

       git rebase --continue
    



This way, you have edited commit specified by _`commit-hash`_ by adding `file.html` to it.  

**WARNING:** This will rewrite the history from that point forward. It is not a good idea when working a project in a team setting.
