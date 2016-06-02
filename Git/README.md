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
####1.1 Git Init
+ command: git init

Transform the current directory into a Git repository and add a file .git to the current directory and makes it possible to start recording revisions of the project.

+ command: git init directory

Create an empty Git repository in the specified directory. Running this command will create a new folder called <directory containing nothing but the .git subdirectory.

+ command: git init --bare directory

Initialize an empty Git repository, but omit the working directory. Shared repositories should always be created with the --bare flag (see discussion below). Conventionally, repositories initialized with the --bare flag end in .git. For example, the bare version of a repository called my-project should be stored in a directory called my-project.git.

##### Note
directory is the folder or the path that you want to create project

####1.2 Git clone
+ command: git clone repo

Clone the repository located at repo onto the local machine. The original repository can be located on the local filesystem or on a remote machine accessible via HTTP or SSH.
 
+ command: git clone repo directory

Clone the repository located at repo into the folder called directory on the local machine. 

##### Note

repo is link repository of project on github, it can be link ssh or link of https

###### Ex
Link https: https://github.com/mpullerits/cooler.git
Link ssh: git@github.com:mpullerits/cooler.git

If you use git clone without init, it will create a folder, name of folder is name project, now you work with branch master.
You want to switch other branch, you have to use: "git checkout branch_name" to switch and work with branch that you want work.


##2 Basic Git command:
https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html
