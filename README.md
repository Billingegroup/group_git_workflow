# Getting started with the Billinge-Group git workflow

This page summarizes the git workflow we use in the Billinge Group.
It is not supposed to teach you how to use git. It is based on the numpy
workflow.  For more on git, GitHub and git workflows,
please go to [full git documentation](https://guides.github.com/). Also
Google and [stackoverflow](https://stackoverflow.com/) is incredibly helpful.

# Workflow example
Here is a brief example of the workflow we will cover.  you can refer back to
this later whenever you want.  If this is your first time through, jump to
Section Step 0 below where things are discussed in more detail.

1. Let's start our new branch on our existing master.

   ```
   git checkout master
   ```

1. Let's make sure our local master is up to date with the upstream master.

   ```
   git pull upstream master --ff-only
   ```

1. Assuming the pull was successful make a new branch based on master for our
  issue fix with memorable name.

   ```
   git checkout -b add_huskies_to_uw
   ```

1. Work work work, test test test, commit commit commit.
1. Create a new branch on our fork and push these commits there.

   ```
   git push -u origin add_huskies_to_uw
   ```

1. Go to fork on GitHub and create a PR into the main repo using the website.
1. Wait for comments, fix comments and commit.
1. Push comments to the same branch and they will automatically update the same PR
   ```
   git push origin add_huskies_to_uw
   ```

   `git push` will also work if you did the `-u` in the earlier push, which creates a permanent link between the local and fork branch.

1. If you see that your PR has a conflict on the main page, it means that the master branch of the main repo has diverged from your local branch. You need to "rebase your branch onto the upstream/master branch". You might be lucky and, on your branch, this command works:

   ```
   git fetch upstream master
   git rebase upstream/master
   ```

   The first step fetches any upstream changes to your local computer but doesn't
   apply them.  If there is a serious conflict though things get more complicated.
   The rebase process with conflict resolution is much easier with `PyCharm` where the process is explained in the [PyCharm documentation](https://www.jetbrains.com/help/pycharm/apply-changes-from-one-branch-to-another.html) or even better, you can reference our documentation below (Step 7).

1. After your PR is pulled in. You can delete your local branch and stay
   nice and organized.

   ```
   git branch -d add_huskies_to_uw
   ```

   You can delete the branch on your fork at `github` website.
   Congratulations! You completed your fix. You are now ready to fix your next issue.

# Some useful commands
Below is a code block for reference. It includes some of the most useful git commands you will use to complete the workflow introduced below. If it's your first time here, skip this block and finish reading the workflow below.

```
git remote add <name> <remote url>  # add a remote
git remote -v  # list all remotes
git remote update  # update and sync with remote branches
git branch # list all local branches
git branch -a  # list all available branches
git checkout <branch name>  # check out an already existing branch. only check out local branches
git checkout -b <new branch name> # check out to new branch based on current branch
git add <filename>  # add changes into working history
git commit -m "CODE: <my commit message>  # commit changes
git push origin <branch_name>  # push local branch to branch on your Fork
```

# Step 0: get all required tools and reference
1. First you need a [github account](https://github.com/).
1. You would also need to have [git](https://git-scm.com/) installed on your computer.
1. Read chapters 15 and 16 of **Effective Computation in Physics** by
Scopatz and Huff (it is strongly recommended that you get a copy, but we do have).
1. We also recommend [PyCharm](http://www.jetbrains.com/pycharm/) as an IDE/editor because
  * It's powerful.
  * It makes rebasing much easier.
  * It's widely used in the group, so you can get help easily.
  * As students you can request a free copy of the full production version!

# Step 1: Fork the repository you wish to contribute to
Forking will allow you to make a `pull-request` (PR) later. We need it for our workflow, even if it may not be clear now why. `fork` can be done through github website:

![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_fork.png "")

# Step 2: Clone the git repository to local machine
1. Go to your fork on GitHub.
1. Click on the green **clone or download** button at the top-right corner:

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_clone.png "")

1. The link shows here is the identity to this repository. Click on the "clipboard icon" to copy the link to your clipboard. You can then copy it and paste to your terminal and do:

   ```
   git clone <url just copied>
   ```

   Now you have your local copy of your remote repository!

# Step 3: Set remote and fetch
1. Navigate to your the directory you just cloned.
1. As suggested by the name, `remote` means the repository on `github`. With a ``remote`` setup, you are able to compare the difference, push edits to and pull changes with respect to remote(s).
1. Your local repo is already connected to the Fork because you cloned it from
   the fork.  However, you need to connect it to the "upstream" repo that the
   fork was forked from.   To do this we need to "add a remote" using the
   following command:

   ```
   git remote add <remote name> <url to the github repository>
   ```

   `url to the github repository` can be obtained as we did in the `clone` section and `remote name` can be any name that is meaningful (easy to remember) to you.
1. To view which remotes your local repository is synced to:

   ```
   git remote -v
   ```

   And you might see something similar to this

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_remote_v.png "")

1. By default `origin` is always set to the repository you cloned. You can rename any `remote` by doing:

   ```
   git remote rename <old name> <new name>
   ```

1. By convention, we usually name the remote repo of the parent repository of your fork as
   `upstream`.
1. If we want to get any changes from remote repositories onto our local
   computer, we can use the following commands:

   ```
   git remote update #update all remotes
   git fetch <remote name> #update certain remote
   ```

   These won't affect our local branch but will make the remote changes
   available if we want to merge or compare.

# Step4: Branch
Branches are like virtual environments. Each of them has its own working history that is
synced with certain `remote`. Once you ``checkout`` (switch) your branch, you
are literally jumping into another parallel world where files live in *another* history.
1. To list all available branches (including ones from all remotes):

   ```
   git branch -a
   ```

1. To checkout (switch) to any branch available branch:

   ```
   git checkout <branch name>
   ```

1. To create a new branch based on **current** branch:

   ```
   git checkout -b <new branch name>
   ```

1. Next, make sure your local master is synced with the upstream master (VERY
   IMPORTANT...can avoid lots of headaches later).  You can update your local ``master`` by:

   ```
   git merge --ff-only upstream production #update your local master
   ```

# Step 5: Add, commit and push
1. Before your edits, checkout to a new branch. Since creating a branch is free on
   github, it's **suggested** to keep every branch as granular as possible.
1. It's also recommended never to edit your local master. Always make a branch and edit that.  Later you will merge it back into master.
1. Start your edits with your favorite editor (we recommend `PyCharm`).
1. After your edits, commit them to your local git repo. To check current working history:

   ```
   git status
   ```

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_status.png "")

   Here you see we have ``Untracked files`` and ``Changes not staged for commit``. The difference between them is as following.
1. `Git` is all about version control so while you are working you might edit existing files or you might create a new file, which hasn't been included into the working tree yet. The newly created file will be listed as `Untracked files`.
1. If a file as been added into your working history before, then every time you change it, `git status` will be listed as ``Changes not staged for commit``.
1. To add this files into your working history:

   ```
   git add <path to files you want to add>
   git add --all # (or git add -A) add all edited files shows in git status
   ```

1. After adding files into history, we want to `commit` the changes. To commit your edits.

   ```
   git commit # this will open the core editor currently used by git
   git commit -m "<commit message>"
   ```

   Usually `git commit` will bring you to something similar to this screen shot:

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_commit.png "")

   The first line is a brief of your commit. It shouldn't be more than a line.
   Starting from the third line, it is the main body of your commit message. You can be as detailed as you want.
1. It is **important** to make your commit message as clear as possible so that other contributor will be able to trace back.
1. You can also use ``git diff`` to see detailed difference between current commit and the last commit.
1. Then we are ready to push our hard work back to `remote`. To push our
   local version to a specific branch in a given remote:

   ```
   git push <remote name> <branch name>
   ```

# Step 6: Pull request
The final step is to get your changes incorporated into the parent (upstream)
repo.  You can't just push them there because you could cause all kinds of
problems.  Instead, you issue a `pull request` (PR).

`pull request` means you are requesting people to consider your edits and github
makes it very easy to compare edits.

1. PR makes it easy to compare difference and start discussions. To issue a PR through github web page:

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/issue_PR.png "")

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/create_PR.png "")

1. After issuing a PR, other developers can view your edits, add comment and eventually decide whether to pull in your PR.
1. You can always update your PR by pushing new edits to the same branch under your fork.


# Step 7: Rebase
Sometimes you may find `Github` shows `This branch has conflicts that
must be resolved` in your PR page. This simply means the remote branch
this PR is based on is in a different working history as `upstream\master`.
`Github` provides a button in the PR page to solve the conflict,
but **DO NOT** use this approach since it creates an extra commit
and could further divert you away from `upstream\master`.
For this situation, the step you need is **rebase**. Rebasing can be
carried out on the command-line using `git` commands (described later) but
it is much easier using a python IDE with built-in rebasing tools, such
as our good friend `PyCharm`. Here we reproduce the steps to do the rebase
using `PyCharm`. It will be slightly different if you are using a
different IDE. Look lower down if you want to do it directly with `Git`.

1. Make sure that you are on the branch that you are actively working
   on and want to rebase. If not,

   ```
   git checkout <branch name>
   ```

1. Make sure you have all the upstream updates on your local computer

   ```
   git fetch upstream master
   ```

1. Make active (by clicking on it) an open file that is on your active branch as in the following figure.

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_rebase0.png "")

   In this case `institutions.yml` is active

1. Left click on `Git: <branch name>` in the lower right of the
   `PyCharm` window.
1. A list of all the linked repositories and branches will pop up. If you click on any of them,
   it will give a list of possible actions regarding that branch.  In the example in the Figure
   the branch checked out is `british_drug_cos` and after clicking on that I selected
   `upstream/master`.  The options are to `check-out`, `compare with`, `merge onto current`,
   `delete`, and of interest here `rebase current onto selected`, which is what we want to do
1. Select `rebase current onto selected` which will rebase
   `british_drug_cos` branch onto the latest fetched version of `upstream/master`
   which is exactly what we want to do.

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_rebase1.png "")

1. `PyCharm` starts the rebase by going and looking for all the commits
   from upstream that are missing on our branch.  While it works, it
   tells us what it is doing in the center-bottom of the page.  Here it is
   first `stashing changes from rg-db-public` because I had made some
   changes that I hadn’t committed.  `PyCharm` will ask git to stash them,
   make all the rebasing updates, then restore them back into the directory
   at the end.  I don’t have to do anything.

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_rebase2.png "")

1. Now `PyCharm` finds a commit in the commit chain that has a conflict
   with the edits on my branch, so a new window pops up with this information in it. I click merge.

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_rebase3.png "")

1. Now a handy window pops up that has my branch version on the left,
   the upstream/master version on the right, and the merged version in
   the middle.  I want to accept all the changes that don’t raise
   conflicts.  These appear in green, and I can accept them all by clicking
   on one of the icons with green arrows in the top tools panel.  I click
   on the one that has green arrows from the left and right, and `PyCharm`
   accepts **ALL** these changes.

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_rebase4.png "")

1. Either I can then navigate to the next (the first in this case)
   conflict by clicking a down-arrow, or in this case `PyCharm` does it
   automatically.  Conflicts appear in red.

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_rebase5.png "")

1. This conflict is easy to resolve because the upstream change is a
   new item, so I want to accept it.  I do that by clicking the `<<` sign on the right.

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_rebase6.png "")

1. Now the conflicting edit in my version is just a carriage return
   on the end of the line.  I could click `>>` and it would also be
   accepted, and placed after the other one, or in this case it is probably
   better to click X to not accept it, since it seems that the
   `upstream/master` edit already has a line-end in it.  Great.  If there
   were more conflicts to resolve I could navigate through them, but this
   was the last so a message pops up “all changes have been processed, save
   changes and finish merging”.  I click on this to accept the changes, or
   I could click on Apply in the lower corner.

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_rebase7.png "")

1. `PyCharm` continues the rebase, looking for the next conflicted commit
   and all the steps above are repeated, until we get through all the
   commits.  Then `PyCharm` says `rebase successful`.

   ![alt text](https://github.com/Billingegroup/group_git_workflow/blob/master/img/git_rebase8.png "")

1. You are all done!  Well done.  But don’t forget to push your
   rebased branch to your fork to update the PR.  This may have to be a
   force-push (--force)

   ```
   git push origin <branch name> --force

   ```

   because you have changed the `git` commit history. Be very careful when force pushing.
   In general you only ever do it to your fork, and you should only need it after a rebase.


# Step 8: Merge after PR is pulled in
1. After your PR is pulled in, your hard works have been merged into `upstream` but your local copy hasn't been updated. So that is the reason why we want to keep local ``master`` branch clean - because we want to make it always aligned with `upstream`.
1. After your PR is merged, you can update your local ``master`` by:

   ```
   git checkout master #checkout to local master
   git merge --ff-only upstream production #update your local master
   ```

1. Now your local ``master`` branch is updated and if you want to work on other features, you can:

   ```
   git checkout -b <new branch name> #switch to a new branch
   ```

   So your new branch would have latest code with ``upstream`` and you can start previous steps :)

Up to now, we have cover the most common git work flow. Of course, you will find
minor difficulties during your work. Please be patient and follow the instruction
``git`` gives at the run time.

# Advanced reference:
[19 Tips For Everyday Git Use](http://www.alexkras.com/19-git-tips-for-everyday-use/)
