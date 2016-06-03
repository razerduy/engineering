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
Link https: https://github.com/mpullerits/cooler.git
Link ssh: git@github.com:mpullerits/cooler.git

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

Remove untracked files from the current directory. The -f _force_ flag is required unless the clean.requireForce configuration option is set to false (it's true by default). This will not remove untracked folders or files specified by _.gitignore_.

+ command: git clean -f __path__

Remove untracked files, but limit the operation to the specified path.

+ command: git clean -df

Remove untracked files and untracked directories from the current directory.

+ command: git clean -xf

Remove untracked files from the current directory as well as any files that Git usually ignores.

+ References: https://www.atlassian.com/git/tutorials/undoing-changes

### 6. Rewriting history
+ References: https://www.atlassian.com/git/tutorials/rewriting-history

## Basic Git command:
https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html
