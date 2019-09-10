# GitTalk

![Branches](Branches.png)

### Contents
* [Getting started](#1-getting-started)
* [Advanced stuff](#2-advanced-stuff)
* [Workflows](#3-workflows)
* [Hacktoberfest](#hacktoberfest)
* [References](#references)


## 1. Getting started
Git is a free and open source software that allows us to improve continously on a project. It is a distributed version control system (DVCS) in which several collaborators can work on the same project.  GitHub is an online remote repository based on Git and thus, has the same features as Git. However, GitHub allows us to create  Pull Requests, which are a very useful interactive way of merging  Branches. GitHub also provides an interactive way to do the things that can be done using a Linux Shell in regards to Git commands. 


### Git  commands 
Here we will review the most common commands through examples. We will also introduce the use of Git through common situations where you may end up using it. Furtheremore, Git has a [documentation](https://git-scm.com/doc) and an official [book](https://git-scm.com/book/en/v2). For more information, see [references](#references).

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
You can just try typing `git help` without `[command]` and the general help will be displayed where the basic commands are listed. 
### Example : creating repositories
We will learn how to get a repository ready for battle. First you need to [install Git](https://git-scm.com/downloads) and have a [GitHub account](https://github.com/), just follow the provided instructions .

 
 #### Create our local repository
* First, you need to configure the personal info 
```git help config ## This will show how config works
git config --global user.name "Your Name" ##Set your name 
git config --global user.email "Your@email" ##Set your email
git conf user.name (user.email) ## View your current settings 
```
Global means that the configuration will be set only for the user of the system. You can see that all this information has been added to the file `.gitconfig` . 

```
 cd
 gedit .gitconfig
```
Imagine we have different GitHub accounts (work and home) and we wish to `push` and `pull` our repo. Therefore, we need to configure the information locally, i,e  ` git config --local `.  

To create a new ropository use 
```
mkdir myrepo
cd myrepo
git init
```
in the directory where you want it. We can see that we have now a `.git` directory -- use `ls -a`--. Now we can create files, add them to the staging area  and commit them. 

* Commit in our local repository: 
 1. Make changes in the Working Tree, for instance create a file.txt `touch file1.txt`
 2. Add these changes in the staging area
 ```
 git add file1.txt
```
If we have more than one file we can add everything fast 
```
git add .
```
we can always see the status of the staging area using `git status`. 
 3. Commit the changes to make it official
```
 git commit -m"comments"
```
The -m option allows us to introduce the message for the commit. However, if we just type `git commit`, Git will display a text editor to write the message. By default, the text editor is "vim". We can always change the text editor using `git config --global core.editor "text_editor"`. **Exercise: Edit file1.txt and create file2.txt. Then, commit the new files**. 
4. In order to see the commits history use  `git log` . However, there are several options that can be helpful:
```
git log --oneline ##short description 
git log --graph ## see the commit --graph 
git log --all --decorate --oneline --graph ## the usual thing to visualize a nice diagram
```
These options will show us the history of our commits and their names. The names of a commit are a SHA-1 (Secure Hash Algorithm) reference. Apart from SHA-1 values , there are user friendly names called references. HEAD and master are user friendly names. HEAD usually points to the last commit of the branch. However, if we checkout to another commit `git checkout [other commit]` , it will show you that HEAD is not in the last commit, so  **DONT LOSE YOUR HEAD!**.
####  Create a remote repository
We can create a remote repository using the interface that GitHub provide, and clone it to our computer

```
git clone https://github.com/TsspGit/GitTalk.git 
```
Nevertheless, we can also push a local repository to GitHub, and thus creating a remote repository 
```
git remote add origin https://github.com/our-repo
```
origin is the usual name for the source-of-truth remote repository. You can have more than one remote repository using the command `git remote add [name] [path]`. Then we push or pull to the preferred remote repository 
```
git push -u origin master
```
Master is the name of the main branch (when use push, enter the branch that we wish to push) and `-u` is the flag of "set-upstream ". `-u` link the local branch to the remote branch and allows us use `git pull` without any arguments. To see the state of the remote repositories, type
```
git remote -v
```
If you are working as a team and a member of your team updates the remote repo, you can download the new features using pull, 
```
git pull 
```


### Problem: Want to retrieve some older version files?
```
git rm -r .
git checkout [SHA-1] . ##  introducing the SHA-1 value
git commit -m"retrieve"
```
What this code does is A <- B <- C <-B,which means that it simply recover an older version. We may want to restore only one file, this can be done manually, i.e.
```
git checkout [SHA-1 of the commit] 
git checkout [name of the branch] ## to go back the last commit of the branch
```
and then manually chose the files. 

HEAD may be important because we can refer to previous commits using `HEAD~n`. Where n represent n-older-version previous commit. For instance, if we want to see the diference between a 3 commits-older version and the current working directory we may use
```
git diff HEAD~3 file.txt
```
We can also retrieve older version using the reference HEAD, i.e. 
```
git rm -r .
git checkout HEAD~n . 
git commit -m"retrieve"
```

Another useful command is `git show [commit] file `, which displays what changes we made at an older commit as well as the commit message.  

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
### Pull Requests & Issues

### Gitflows

### Privacity

## Hacktoberfest
Most important event ever
## References
* [Git](https://git-scm.com/)
* [GitHub](https://github.com/)
* [bitbucket](https://bitbucket.org/)
* [xuanxu](https://github.com/xuanxu/)
* [Chacon, S., & Straub, B. (2014). Pro git. Apress.](https://git-scm.com/book/en/v2)
* [Version control with Git, Coursera](https://www.coursera.org/learn/version-control-with-git)
* [Software Carpentry, version control with Git](https://swcarpentry.github.io/git-novice/)
* [hacktoberfest 2019](https://hacktoberfest.digitalocean.com/)
