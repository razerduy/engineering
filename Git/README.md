# Engineering

Why git?

Version control has become a central requirement for modern software development. It allows projects to safely track changes and enable reversions, integrity checking, and collaboration among other benefits. The git version control system, in particular, has seen wide adoption in recent years due to its decentralized architecture and the speed at which it can make and transfer changes between parties.

While the git suite of tools offers many well-implemented features, one of the most useful characteristics is its flexibility. Through the use of a "hooks" system, git allows developers and administrators to extend functionality by specifying scripts that git will call based on different events and actions.

In this guide, we will explore the idea of git hooks and demonstrate how to implement code that can assist you in automating tasks in your own unique environment. We will be using an Ubuntu 14.04 server in this guide, but any system that can run git should work in a similar way.


Setup Github:
For Windows: http://git-scm.com/download/win
For Mac: http://git-scm.com/download/mac
For Ubuntu/Debian: $ sudo apt-get install git
For CentOS/Fedora/RHEL: $ yum install git


Usage:
1. Setting up a repository:

+ command: git init
Transform the current directory into a Git repository and add a file .git to the current directory and makes it possible to start recording revisions of the project.

+ command: git init <directory>
Create an empty Git repository in the specified directory. Running this command will create a new folder called <directory containing nothing but the .git subdirectory.

+ command: git init --bare <directory>
Initialize an empty Git repository, but omit the working directory. Shared repositories should always be created with the --bare flag (see discussion below). Conventionally, repositories initialized with the --bare flag end in .git. For example, the bare version of a repository called my-project should be stored in a directory called my-project.git.

Basic Git command:
https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html
