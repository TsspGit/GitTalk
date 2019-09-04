# GitTalk
Charlita de Dani y yo

## Instalation
How to install git
## Introduction
In order to clone a repository, type
```
git clone

```
## Examples

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
