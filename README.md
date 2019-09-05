# GitTalk
Charlita de Dani y Tomás

### Contents
* [Getting started](#1-getting-started)
* [Advanced stuff](#2-advanced-stuff)
* [Workflows](#3-workflows)
* [Hacktoberfest](#hacktoberfest)
* [References](#references)


## 1. Getting started
Git is a free and open source software that allows us to improve continously on a project. It is a distributed version control system (DVCS) in which several collaborators can work on the same project.  GitHub is an online remote repository based on Git and thus, has the same features as Git. However, GitHub allows us to create  Pull Requests, which are a very useful interactive way of merging  Branches. It also provides an interactive interface to do the things that can be done using a terminal. 


### Git  commands 
Here we review the most common commands through examples. We will introduce the use of Git through common situations where you may end up using it. Furtheremore, Git has a [documentation](https://git-scm.com/doc) and an official [book](https://git-scm.com/book/en/v2). For more information, see [references](#references)

Git commands are typed in the terminal (shell) and have the following general structure
```
git [command] [--flags] [arguments]
```
You can also see, Git Help! 
```
git help [command]
```
When you type `git help [commnand]`, things like this will appear in your terminal:
```
-f or --flag ## Change the command behaviour, options of the commnand.
[<placeholders>] ## replace the placeholder by the actual value, arguments.

```
### Example : creating repositories
We will learn how to get a repository ready for battle. First you need to install Git, just visit the [Git web page](https://git-scm.com/downloads) and follow the instructions.

1. To create a remote repository, click at "create a remote repository" in GitHub and follow the instructions. 
2. Create your local repository
* First, you need to configure the personal info 
```$git help config ## This will show how config works
$git config --global user.name "Your Name" ##Set your name 
$git config --global user.email "Your@email" ##Set your email
$git conf user.name (user.email) ## View your current settings 
```
You can see that all this information has been added to the file .gitconfig . 

```
$ cd
$ gedit .gitconfig
```
Imagine we have different GitHub accounts (work and home) and we wish to push and pull our repo. Therefore, we need to configure the information locally, i,e  ` git config --local `. 

* Clone our remote repository
```
git clone https://github.com/TsspGit/GitTalk.git 
```
* Commit in our local repository 
 1. Make changes in the Working Tree, for instance create a file.txt
 2. Add this changes in the staging area
 ```
 git add file.txt
```
If we have more than one file we add everything fast 
```
git add .
```
 3. Commit the changes to make it official
```
 git commit
```
4. See the commits history use  `git log` . However, there are several options that can be helpful
```
git log --oneline ##short description 
git log --graph ## see the commit --graph 
git log --all --decorate --oneline --graph ## the usual thing to visualize

```
It will show you the history of your commits and the names. The names of the commit are a SHA-1 (Secure Hash Algorithm) reference.  Note that we can always go to and old commit using checkout and the SHA-1 value of that commit.

### Problem: Want to retrieve some older version files?
```

git rm -r .
git checkout [SHA-1] . ##  introducing the SHA-1 value
git checkout [HEAD~n] . ## introducing the n latest branch
git commit -m"retrieve"
```
```
I should explain more about the HEAD and ~^ or these things
```

Note that the dot `.` is important at the end of the commands. What this code does is A <- B <- C <-B, simple goes to an older version. We may want to restore only one file, this can be done manually, i.e.
```
git checkout [SHA-1 of the commit]
git checkout [name of the branch] ## to go back the last commit of the branch
```
and then manually chose the files. 


## 2. Advanced stuff

### Example fetch:
It is possible to connect our local repository to as many remote repositories as we want.
In order to doing that let's add the following repository:
```
$ git remote xuanxu https://github.com/xuanxu/
```
- Display the remotes repositories with:
```
$ git remote -v
```
- Finally, fetch the information about the commits and the branches created:
```
$ git fetch xuanxu
```

### Example stash:
Maybe, you are adding some funcionalities to your project and you realize that you have to
solve a very urgent bug. Also maybe you forgot to commit the last changes and have some
half-done work. How do you choose what to commit and what not? **git stash**

On *stash_ex* branch one could fine a python file named *sumar.py*. The file consist of a
simply function and its respective test. Imagine that we are working on a file named
*restar.py* at the time that we need to solve immediately the error in *sumar.py*.
```
$ vim restar.py
```
```
$ git add restar.py
```
- git status would say that we have uncomitted files. Now, stash them:
```
$ git stash
```
- Now, git status says that there isn't files to commit. *git stash list* returns the
  files stashed away. 
Following the example, once we have solved the bug we can commit the changes. 

- Finally, go back to a clean directory recovering stashed files:
```
$ git stash apply
```
- And clear the dirty stash directory:
```
$ git stash clear
```

### Example rebase:
One way to change the commit's history is using **git rebase**. In this example we will
integrate changes from one branch into another.

The branch *rebase_master* contains predoc.py, which is a class that send the information
of new employees to the database of the company. The commit is already done, but we would
like to add a new method to firing people. The first step that we are going to take is to
create a new branch named *fire*.
```
$ git checkout -b fire
```
- Add the next part of code inside the class on predoc.py:
```
def __del__(self):
	print("You just fired ", self.name)
```
- Commit the modification with the message 'add firing predoc.py'. 
- At the moment you are working your collaborator creates a new file on *rebase_master*:
```
$ touch newfile.txt
```
- Commit it and run **git --all --decorate --oneline --graph - 4**. Notice that the
  working flow are no longer linear. 
- Finally, checkout to fire branch and run:
```
$ git rebase rebase_master
```
- See how the working flow have change. The history of *fire* has been erased!
- Let's finalize this example checking that the information contained in each branch is
  the same than before the rebase. This implies that we need to merge those two branches
in order to collect the modifications.


## 3. Workflows
## Hacktoberfest

## References
* [Git](https://git-scm.com/)
* [GitHub](https://github.com/)
* [bitbucket](https://bitbucket.org/)
* [xuanxu](https://github.com/xuanxu/)
* [Chacon, S., & Straub, B. (2014). Pro git. Apress.](https://git-scm.com/book/en/v2)
* [Version control with Git, Coursera](https://www.coursera.org/learn/version-control-with-git)


