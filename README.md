# GitTalk
Charlita de Dani y yo

## Contents

## Getting started
Git is a free an open source software that allows us to improve continously on a project. It is a distributed version control system in which several collaborators can work on the same project.  GitHub is an online remote repository based on Git and thus, has the same features as Git. However, GitHub allows you yo start a PullRequest, which is a very useful interactive way of merging to Branches. 


### Git  commands 
Here we review the most useful commands. We will introduce the use of Git through common situations where you may end up using Git. Furtheremore, Git has a [documentation](https://git-scm.com/doc) and an official [book](https://git-scm.com/book/en/v2). 

Git commands are typed in the terminal (shell) and have the following general structure
```
git [command] [--flags] [arguments]
```
You can also see, Git Help! 
```
git help [command]
```
Reading help:
```
-f or --flag ## Change the command behaviour
[<placeholders>] ## replace the place holder by the actual value

```
### Example 1: creating repositories
We will learn how to get a repository ready for battle. First you need to install git, visit the [Git web page](https://git-scm.com/downloads) and follow the instructions.

1. Create the remote repository
2. Create your local repository
*  you need to configure the personal info 
```$git help config ## This will show how config works
$git config --global user.name "Your Name" ##Set your name 
$git config --global user.email "Your@email" ##Set your email
$git conf user.name (user.email) ## View your current settings 
```
You can see that all this information has been added to the file .gitconfig
```
$ cd
$ gedit .gitconfig
```
Imagine we have different GitHub accounts (work and home) and we wish to push and pull our repo. Therefore, we need to configure the information locally, i,e  ` git config --local `. 

*  Clone our remote repository
```
git clone https://github.com/TsspGit/GitTalk.git 
```
* Commit in our local repository 
 1. Make changes in the Working Tree, for instance create a file.txt
 2. Add this changes in the staging area
 ```
 git add file.txt
```
 3. Commit the changes to make it official
```
 git commit
```
4. See the commits history
```
git log --oneline
```
It will show you the history of your commits and the names. The names of the commit are a SHA-1 (Secure Hash Algorithm) reference.  Note that we can always go to and old commit using checkout and the SHA-1 value of that commit.

### Problem: Want to retrieve some older version files?
```
git rm -r .
git checkout [SHA-1] . ##  introducing the SHA-1 value
git checkout [HEAD~n] . ## introducing the n latest brancg
git checkout [name of the branch] ## to go the last commit of the branch
```
What this code does is A <- B <- C <-B. We may want to restore only one file, this can be done manually, i.e.
```
git checkout [SHA-1 of the commit]
```
and then manually chose the files. 
t
