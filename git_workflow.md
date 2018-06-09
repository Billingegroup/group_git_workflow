# Git workflow

This page is aimed to be a simplified version of github help. For complete workflow,
please go to [full git documentation](https://guides.github.com/). Also Google and [stackoverflow](https://stackoverflow.com/) is incredibly helpful.

Below is a code block for reference. It includes the most basic git commands you will
use to complete the workflow introduced below. If it's your first time
here, skip this block and finish reading the workflow doc first.
```git
git clone <remote url>  # clone a repo
git remove add <name> <remote url>  # add a remote
git remove -v  # list all remotes
git remote update  # update remotes
git branch -a  # list all available branches
git checkout <branch name>  # checkout to available branch
git checkout -b <new branch name> # checkout to new branch based on current branch
git add <path to the file>  # add changes into working history
git commit  # commit changes
git push <remote name>  <branch name>  # push local to remote
```
# Step 0: get all required tools and reference
1. First you need a [github account](https://github.com/).
1. You would also need to have [git](https://git-scm.com/) installed on your computer.
1. Read chapters 15 and 16 of **Effective Computation in Physics** by
Scopatz and Huff (it is strongly recommended that you get a copy, but we do have.
1. We also recommend [PyCharm](http://www.jetbrains.com/pycharm/) because
  * it's powerful.
  * it's wildly used in the group, so you can get help easily.
  * as students you can request a free copy of the full production version!

# Step 1: Fork the repository you wish to contribute
Forking means you keep the entire copy of certain github repository under your account. 
The advantages of forking are:
1. it doesn't affect the original repository, i.e. what was working remains working.
1. now this repository is completely under your account, you can do whatever you want. `fork` can be done through github website:

![alt text](https://github.com/chiahaoliu/group_git_workflow/blob/doc_gitworkflow/img/git_fork.png "")

# Step 2: Clone the git repository to local machine
1. Go to the repository you wish to work on(ideally under your fork). Click on the green **clone or download** button at the top-right corner:

![alt text](https://github.com/chiahaoliu/group_git_workflow/blob/doc_gitworkflow/img/git_clone.png "")

1. The link shows here is the identity to this repository. You can then copy it and paste to your terminal and do:
```
git clone <url just copied>
```
Now you have your local copy of your remote repository!

# Step 3: Set remote and fetch
1. Navigate to your the directory you just cloned.
1. As suggested by the name, `remote` means the repository on `github`. With a ``remote`` setup, you are able to compare the difference, push edits to and pull changes with respect to remote(s).
1. To add a remote:
```
git remote add <name of this remote> <url to the github repository>
```
`url to the github repository` can be obtained as we did in the ``clone`` section.
and ``name of this remote`` can be any name that is meaningful (easy to remember) to you.
1. To view which remotes your local repository is synced to: 
```
git remote -a
```
And you might see something similar to this

![alt text](https://github.com/chiahaoliu/group_git_workflow/blob/doc_gitworkflow/img/git_remote_v.png "")

1. By default `origin` is always set to the repository you cloned. You can rename any `remote` by doing:
```
git remote rename <old name> <new name>
```
1. By convention, we usually set the parent repository of your fork as
   `upstream`. Because that's where our contribution will go into.
1. We then sync our local with all remotes. 
```
git remote update #update all remotes
git fetch <remote name> #update certain remote
```

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

# Step 5: Add, commit and push
1. Before your edits, checkout to a new branch. Since branch is free on
   github, it's **suggested** to keep every branch as granular as possible.
1. It's also recommended to leave your local master untouched. The main reason will be explained later in the `Pull request`` section.
1. Start your edits with your favorite editor (we recommand `PyCharm`).
1. After your edits, put your works into the working tree. To check current working history:
```
git status
```

![alt text](https://github.com/chiahaoliu/group_git_workflow/blob/doc_gitworkflow/img/git_status.png "")

Here you see we have ``Untracked files`` and ``Changes not staged for commit``. The difference between them is as following.
1. `Git` is all about version control so while you are working you might edit existing files or you might create a new file, which hasn't been included into the working tree yet. The newly created file will be listed as `Untracked files`.
1. If a file as been added into your working history before, then every time you change it, `git status` will be listed as ``Changes not staged for commit``.
1. To add this files into your working history:
```
git add <path to files you want to add>
git add -all # add all edited files shows in git status
```
1. After adding files into history, we want to `commit` the changes. To commit your edits.
```
git commit # this will open the core editor currently used by git
git commit -m "<commit message>"
```
Usually `git commit` will bring you to something similar to this
screen shot:
![alt text](https://github.com/chiahaoliu/group_git_workflow/blob/doc_gitworkflow/img/git_commit.png "")
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
Assume you have gone through all the steps and pushed your works onto
your fork but we haven't had any interaction with `upstream` yet. It's always nice to have a second opinion on our works and `pull request(PR)` turns out to be a good way of doing this.

`pull request` means you are requesting people to consider your edits and github
makes it very easy to compare edits.

1. PR makes it easy to compare difference and start discussions. To issue a PR through github web page:

![alt text](https://github.com/chiahaoliu/group_git_workflow/blob/doc_gitworkflow/img/issue_PR.png "")
![alt text](https://github.com/chiahaoliu/group_git_workflow/blob/doc_gitworkflow/img/create_PR.png "")

1. After issuing a PR, other developers can view your edits, add comment and eventually decide whether to pull in your PR.
1. You can alway update your PR by pushing new edits to the same branch under your fork.

# Step 7: Merge after PR is pulled in
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
