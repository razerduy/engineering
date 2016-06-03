# Engineering

## Why git?

Version control has become a central requirement for modern software development. It allows projects to safely track changes and enable reversions, integrity checking, and collaboration among other benefits. The git version control system, in particular, has seen wide adoption in recent years due to its decentralized architecture and the speed at which it can make and transfer changes between parties.

While the git suite of tools offers many well-implemented features, one of the most useful characteristics is its flexibility. Through the use of a "hooks" system, git allows developers and administrators to extend functionality by specifying scripts that git will call based on different events and actions.

In this guide, we will explore the idea of git hooks and demonstrate how to implement code that can assist you in automating tasks in your own unique environment. We will be using an Ubuntu 14.04 server in this guide, but any system that can run git should work in a similar way.

## Setup Github
For Windows: http://git-scm.com/download/win

For Mac: http://git-scm.com/download/mac

For Ubuntu/Debian: $ sudo apt-get install git

For CentOS/Fedora/RHEL: $ yum install git

##### Note

you can use [Github application](https://desktop.github.com/) or [SourceTree application](https://www.atlassian.com/software/sourcetree)

## Usage
### 1. Setting up a repository
####1.1. Git Init
+ command: git init

Transform the current directory into a Git repository and add a file .git to the current directory and makes it possible to start recording revisions of the project.

+ command: git init __directory__

Create an empty Git repository in the specified directory. Running this command will create a new folder called _directory containing nothing but the .git subdirectory.

+ command: git init --bare __directory__

Initialize an empty Git repository, but omit the working directory. Shared repositories should always be created with the --bare flag (see discussion below). Conventionally, repositories initialized with the --bare flag end in .git. For example, the bare version of a repository called my-project should be stored in a directory called my-project.git.

##### Note
directory is the folder or the path that you want to create project

####1.2. Git clone
+ command: git clone __repo__

Clone the repository located at repo onto the local machine. The original repository can be located on the local filesystem or on a remote machine accessible via HTTP or SSH.
 
+ command: git clone __repo__ __directory__

Clone the repository located at repo into the folder called directory on the local machine. 

##### Note

repo is link repository of project on github, it can be ssh or https

###### Ex

Link https: _https://github.com/mpullerits/cooler.git _

Link ssh: _git@github.com:mpullerits/cooler.git_

If you use git clone without init, it will create a folder, name of folder is name project, now you work with branch master.
You want to switch other branch, you have to use: "git checkout branch__name" to switch and work with branch that you want work.

####1.3. Git config

The git config command lets you configure your Git installation (or an individual repository) from the command line. This command can define everything from user info to preferences to the behavior of a repository. Several common configuration options are listed below.

+ command: git config user.name __name__

Define the author name to be used for all commits in the current repository.

Typically, you’ll want to use the --global flag to set configuration options for the current user.

+ command: git config --global user.name __name__
+ command: git config --global user.email __email__

References: https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-config

### 2. Saving changes
####2.1 Git add

The git add command adds a change in the working directory to the staging area

+ command: git add __file__
Stage all changes in __file__ for the next commit.
+ command: git add __directory__
Stage all changes in __directory__ for the next commit.

####2.2 Git commit

The git commit command commits the staged snapshot to the project history. Committed snapshots can be thought of as “safe” versions of a project—Git will never change them unless you explicity ask it to. Along with git add, this is one of the most important Git commands.

+ command: git commit
+ command: git commit -m __message__

##### Note: you should use "git commit -m __message__" to remember what you changes

### 3. Inspecting a repository
####3.1 Git status

The git status command displays the state of the working directory and the staging area.

+ command: git status
List which files are staged, unstaged, and untracked.
+ command: git log
Display the entire commit history using the default formatting. If the output takes up more than one screen, you can use Space to scroll and q to exit.

### 4. Viewing old commits

The git checkout command serves three distinct functions: checking out files, checking out commits, and checking out branches. In this module, we’re only concerned with the first two configurations.
+ command: git checkout __branch__

This return to _branch_ and this also return all of file in this branch with commit lastest

+ command: git checkout __commit__ __file__

Check out a previous version of a file. This turns the _file_ that resides in the working directory into an exact copy of the one from _commit_ and adds it to the staging area.

+ command: git checkout __commit__

Update all files in the working directory to match the specified commit. You can use either a commit hash or a tag as the _commit_ argument. This will put you in a detached HEAD state. 

+ References: https://www.atlassian.com/git/tutorials/viewing-old-commits

### 5. Undoing changes
#### 5.1. Git checkout _see above_
#### 5.2. Git revert

The git revert command undoes a committed snapshot. But, instead of removing the commit from the project history, it figures out how to undo the changes introduced by the commit and appends a new commit with the resulting content. This prevents Git from losing history, which is important for the integrity of your revision history and for reliable collaboration.

+ command: git revert __commit__

Generate a new commit that undoes all of the changes introduced in _commit_, then apply it to the current branch.

#### 5.3. Git reset

When you undo with git reset(and the commits are no longer referenced by any ref or the reflog), there is no way to retrieve the original copy—it is a permanent undo. Care must be taken when using this tool, as it’s one of the only Git commands that has the potential to lose your work.

+ command: git reset __file__

Remove the specified file from the staging area, but leave the working directory unchanged. This unstages a file without overwriting any changes.

+ command: git reset

Reset the staging area to match the most recent commit, but leave the working directory unchanged. This unstages all files without overwriting any changes, giving you the opportunity to re-build the staged snapshot from scratch.

+ command: git reset --hard

Reset the staging area and the working directory to match the most recent commit. In addition to unstaging changes, the --hard flag tells Git to overwrite all changes in the working directory, too. Put another way: this obliterates all uncommitted changes, so make sure you really want to throw away your local developments before using it.

+ command: git reset __commit__

Move the current branch tip backward to _commit_, reset the staging area to match, but leave the working directory alone. All changes made since _commit_ will reside in the working directory, which lets you re-commit the project history using cleaner, more atomic snapshots.

+ command: git reset --hard __commit__

Move the current branch tip backward to _commit_ and reset both the staging area and the working directory to match. This obliterates not only the uncommitted changes, but all commits after _commit_, as well.

#####Note: Difference between revert vs reset in [here] (https://www.atlassian.com/git/tutorials/undoing-changes/git-revert)

#### 5.4. Git clean

The git clean command removes untracked files from your working directory. This is really more of a convenience command, since it’s trivial to see which files are untracked with git status and remove them manually. Like an ordinary rm command, git clean is not undoable, so make sure you really want to delete the untracked files before you run it.

The git clean command is often executed in conjunction with git reset --hard. Remember that resetting only affects tracked files, so a separate command is required for cleaning up untracked ones. Combined, these two commands let you return the working directory to the exact state of a particular commit.

+ command: git clean -n

Perform a “dry run” of git clean. This will show you which files are going to be removed without actually doing it.

+ command: git clean -f

Remove untracked files from the current directory. The -f (force) flag is required unless the clean.requireForce configuration option is set to false (it's true by default). This will not remove untracked folders or files specified by _.gitignore_.

+ command: git clean -f __path__

Remove untracked files, but limit the operation to the specified path.

+ command: git clean -df

Remove untracked files and untracked directories from the current directory.

+ command: git clean -xf

Remove untracked files from the current directory as well as any files that Git usually ignores.

+ References: https://www.atlassian.com/git/tutorials/undoing-changes

### 6. Rewriting history

####6.1. Git commit --amend

+ command: git commit --amend

Combine the staged changes with the previous commit and replace the previous commit with the resulting snapshot. Running this when there is nothing staged lets you edit the previous commit’s message without altering its snapshot.

####6.2. Git rebase

+ command: git rebase __base__

Rebase the current branch onto _base_, which can be any kind of commit reference (an ID, a branch name, a tag, or a relative reference to HEAD).

####6.3. Git rebase -i

Running git rebase with the -i flag begins an interactive rebasing session. Instead of blindly moving all of the commits to the new base, interactive rebasing gives you the opportunity to alter individual commits in the process. This lets you clean up history by removing, splitting, and altering an existing series of commits. It’s like git commit --amend on steroids.

+ command: git rebase -i __base__

Rebase the current branch onto _base_, but use an interactive rebasing session. This opens an editor where you can enter commands (described below) for each commit to be rebased. These commands determine how individual commits will be transferred to the new base. You can also reorder the commit listing to change the order of the commits themselves.

####6.4. Git reflog

Git keeps track of updates to the tip of branches using a mechanism called reflog. This allows you to go back to changesets even though they are not referenced by any branch or tag. After rewriting history, the reflog contains information about the old state of branches and allows you to go back to that state if necessary.

+ command: git reflog

Show the reflog for the local repository.

+ command: git reflog --relative-date

Show the reflog with relative date information (e.g. 2 weeks ago).

+ References: https://www.atlassian.com/git/tutorials/rewriting-history

### 7. Syncing

####7.1. Git remote

The git remote command lets you create, view, and delete connections to other repositories. Remote connections are more like bookmarks rather than direct links into other repositories. Instead of providing real-time access to another repository, they serve as convenient names that can be used to reference a not-so-convenient URL.

+ command: git remote

List the remote connections you have to other repositories.'

+ command: git remote -v

Same as the above command, but include the URL of each connection.

+ command: git remote add __name__ __url__

Create a new connection to a remote repository. After adding a remote, you’ll be able to use _name_ as a convenient shortcut for _url_ in other Git commands.

+ command: git remote rm __name__

Remove the connection to the remote repository called _name_

+ command: git remote rename __old-name__ __new-name__

Rename a remote connection from _old-name_ to _new-name_

####7.2. Git fetch

The git fetch command imports commits from a remote repository into your local repo. The resulting commits are stored as remote branches instead of the normal local branches that we’ve been working with. This gives you a chance to review changes before integrating them into your copy of the project.

+ command: git fetch __remote__

Fetch all of the branches from the repository. This also downloads all of the required commits and files from the other repository.

+ command: git fetch __remote__ __branch__

Same as the above command, but only fetch the specified branch.

####7.3. Git pull

+ command: git pull __remote__

Fetch the specified remote’s copy of the current branch and immediately merge it into the local copy. This is the same as git fetch _remote_ followed by git merge origin/_current-branch_.

+ command: git pull --rebase __remote__

Same as the above command, but instead of using git merge to integrate the remote branch with the local one, use git rebase.

####7.3. Git push

+ command: git push __remote__ __branch__

Push the specified branch to _remote_, along with all of the necessary commits and internal objects. This creates a local branch in the destination repository. To prevent you from overwriting commits, Git won’t let you push when it results in a non-fast-forward merge in the destination repository.

+ command: git push _remote_ --force

Same as the above command, but force the push even if it results in a non-fast-forward merge. Do not use the --force flag unless you’re absolutely sure you know what you’re doing.

+ command: git push _remote_ --all

Push all of your local branches to the specified remote.

+ command: git push _remote_ --tags

Tags are not automatically pushed when you push a branch or use the --all option. The --tags flag sends all of your local tags to the remote repository.

### 8. Using branch

####8.1. Git branch

A branch represents an independent line of development. Branches serve as an abstraction for the edit/stage/commit process discussed in Git Basics, the first module of this series. You can think of them as a way to request a brand new working directory, staging area, and project history. New commits are recorded in the history for the current branch, which results in a fork in the history of the project.

The git branch command lets you create, list, rename, and delete branches. It doesn’t let you switch between branches or put a forked history back together again. For this reason, git branch is tightly integrated with the git checkout and git merge commands.

+ command: git branch

List all of the branches in your repository.

+ command: git branch __branch__

Create a new branch called _branch_. This does not check out the new branch.

+ command: git branch -d __branch__

Delete the specified branch. This is a “safe” operation in that Git prevents you from deleting the branch if it has unmerged changes.

+ command: git branch -D __branch__

Force delete the specified branch, even if it has unmerged changes. This is the command to use if you want to permanently throw away all of the commits associated with a particular line of development.

+ command: git branch -m __branch__

Rename the current branch to _branch_.

####8.2. Git checkout

The git checkout command lets you navigate between the branches created by git branch. Checking out a branch updates the files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on that branch. Think of it as a way to select which line of development you’re working on.

In the previous module, we saw how git checkout can be used to view old commits. Checking out branches is similar in that the working directory is updated to match the selected branch/revision; however, new changes are saved in the project history—that is, it’s not a read-only operation.

+ command: git checkout __existing-branch__

Check out the specified branch, which should have already been created with git branch. This makes _existing-branch_ the current branch, and updates the working directory to match.

+ command: git checkout -b __new-branch__

Create and check out _new-branch_. The -b option is a convenience flag that tells Git to run git branch _new-branch_ before running git checkout _new-branch_. git checkout -b _new-branch_ _existing-branch_

Same as the above invocation, but base the new branch off of _existing-branch_ instead of the current branch.

####8.3. Git merge

Merging is Git's way of putting a forked history back together again. The git merge command lets you take the independent lines of development created by git branch and integrate them into a single branch.

Note that all of the commands presented below merge into the current branch. The current branch will be updated to reflect the merge, but the target branch will be completely unaffected. Again, this means that git merge is often used in conjunction with git checkout for selecting the current branch and git branch -d for deleting the obsolete target branch.

+ command: git merge _branch_

Merge the specified branch into the current branch. Git will determine the merge algorithm automatically (discussed below).

+ command: git merge --no-ff __branch__

Merge the specified branch into the current branch, but always generate a merge commit (even if it was a fast-forward merge). This is useful for documenting all merges that occur in your repository.

## Basic Git command:

https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html
