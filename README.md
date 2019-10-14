# GitTalk

![Branches](Branches.png)

### Contents
* [Getting started](#1-getting-started)
* [Advanced stuff](#2-advanced-stuff)
* [Workflows](#3-workflows)
* [Hacktoberfest](#hacktoberfest)
* [References](#references)


## 1. Getting started
Git is a free and open source software that allows us to improve continously on a project. It is a distributed version control system (DVCS) in which several collaborators can work on the same project.  GitHub is a website  based on Git and thus, it has the same features as Git. However, GitHub allows us to create  Pull Requests, which are a very useful interactive way of merging  Branches. From my personal point of view, it has the spirit of social networks but for code sharing.   


### Git  commands 
During this talk, we will review the most common commands through examples. We will also introduce the use of Git through common situations where you might end up using it. Furtheremore, Git has [documentation](https://git-scm.com/doc) and an official [book](https://git-scm.com/book/en/v2). For more information, see [references](#references).

Git commands are typed in a terminal and have the following general structure
```
$ git [command] [--flags] [arguments]
```
For instance, Git Help! 
```
$ git help [command]
``` 
Here `[command]` is the `[argument]` of `[help]`. Whenever you type `git help [commnand]`, things like this will appear in your terminal:
```
$ -f or --flag ## Change the command behaviour, options of the commnand.
$ [<placeholders>] ## replace the placeholder by the actual value, arguments.
```
 Just try typing `git help` without `[command]` and the general help will be displayed where the basic commands are listed. 
### Example : creating repositories
We will learn how to get a repository ready for battle. First you need to [install Git](https://git-scm.com/downloads) and have a [GitHub account](https://github.com/), just follow the provided instructions .

 
 #### Create a local repository
* First, you need to configure the personal info 
```$ git help config ## This will show how config works
$ git config --global user.name "Your Name" ##Set your name 
$ git config --global user.email "Your@email" ##Set your email
$ git conf user.name (user.email) ## View your current settings 
```
Global means that the configuration will be set for the system user . You can see that all this information has been added to the file `.gitconfig` .  

```
 $ cd
 $ gedit .gitconfig
```
Imagine we have two different GitHub accounts (work and home) and we wish to `push` and `pull` our private repository. Therefore, we need to configure the information locally, i.e,  `$  git config --local `.  Moreover, the following code worked for me well (otherwise Git may not identify private repositories). 
```
$ git clone https://username@github.com/username/repo_name
```
To create a new ropository type 
```
$ mkdir myrepo
$ cd myrepo
$ git init
```
at the desired directory. We can see that we have now a `$ .git` directory ( use `ls -a` ). From this point, we can create files, add them to the staging area and commit them. 

* Commit in our local repository: 
 1. Make changes in the Working Tree, for instance create a file.txt `$ touch file1.txt`.
 2. Add these changes in the staging area
 ```
$ git add file1.txt
```
If we have more than one file we can add everything fast 
```
$ git add .
```
we can always see the status of the staging area using `$ git status`. 
 3. Commit the changes to make it official
```
$ git commit -m"comments"
```
The -m option allows us to introduce the message for the commit. However, if we just type `$ git commit`, Git will display a text editor to write the corresponding message. By default, the text editor is "vim". We can always change the text editor using `$ git config --global core.editor "text_editor"`,  I use sublime  `$ git config --global core.editor "subl -n -w"` . **Exercise: Edit file1.txt and create file2.txt. Then, commit the new files**. 
4. In order to see the commits history use  `git log` . However, there are several options that can be helpful:
```
$ git log --oneline ##short description 
$ git log --graph ## see the commit --graph 
$ git log --all --decorate --oneline --graph ## the usual thing to visualize a nice diagram
```
These options will show us the history of our commits and their names. The names of a commit are a SHA-1 (Secure Hash Algorithm) reference. Apart from SHA-1 values , there are user friendly names called references. HEAD and master are user friendly names. HEAD usually points to the last commit of the branch. However, if we checkout to another commit `$ git checkout [SHA1_othercommit]` , it will show us that HEAD is not in the last commit, so  **DONT LOSE YOUR HEAD!**.
####  Create a remote repository
We can create a remote repository using the interface that GitHub provide, and clone it to our computer

```
$ git clone https://github.com/TsspGit/GitTalk.git 
```
Or set the path, and push. 
```
$ git remote add origin https://github.com/user/repo
```
origin is the usual name for the source-of-truth remote repository. You can have more than one remote repository using the command `$ git remote add [name] [path]`. Then we push or pull to the preferred remote repository 
```
$ git push -u origin master
```
Master is the name of the main branch (we need to specify the branch that we wish to push) and `-u` is the flag of "set-upstream ". `-u` link the local branch to the remote branch and allows us use `$ git pull` without any arguments (this usually works by default). To see the state of the remote repositories, type
```
$ git remote -v
```
If you are working as a team and a member of your team updates the remote repo, you can download the new features using pull, 
```
$ git pull 
```
`$ git pull` merge the remote repository with the local repository. Sometimes, a milder option is better. This is the command `git fetch`.

### Example fetch:
It is possible to connect our local repository to as many remote repositories as we want.
In order to doing that let's add the following repository:
```
$ git remote xuanxu https://github.com/xuanxu/intergalactic
```
- Display the remotes repositories with:
```
$ git remote -v
```
- Finally, fetch the information about the commits and the branches created:
```
$ git fetch xuanxu
```
It appears that the fetched repository has the reference FETCH_HEAD and thus, to see all the content we need to type
```
$ git checkout FETCH_HEAD
```

### Problem: Want to retrieve some older version files?
```
git rm -r .
git checkout [SHA-1] . ##  introducing the SHA-1 value
git commit -m"retrieve"
```
What this code does is `A <- B <- C <-B` , which means that it simply recovers an older version (commit). We may want to restore only one file, this can be done manually, i.e.
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

Another useful command is `git show [commit] file `, which displays what changes we made regarding an older commit as well as the commit messages.  



## 2. Merging example

1. Create the branch merge1 and a file named mergear.txt
```
$ git checkout -b merge1 && touch mergear.txt 
```

2. Commit with message "mergear.txt created"

3. From merge1 create a new branch named merge2 and write:
"hola
que tal"
Inside mergear.txt

4. Commit with message "change mergear.txt in merge2"

5. Come back to merge1 and write:
"adios"
Inside mergear.txt

6. Commit with message "change mergear.txt in merge1"

7. At this point, we have an ancestor commit that the two branches share and two different commits in each of them. If we try to merge the two branches, Git will try a 3-way merge and it would fail. 
```
$ git merge merge2
```

8. The reason is that Git can't choose between changes performed in the same position of the file. In order to solve it we have to open the file and delete the lines with:
<<<<<<< HEAD
=======
>>>>>>>
Reorder the lines as you wish and commit.

9. Delete merge2 branch.
```
$ git branch -D merge2
Or if the branch has been pushed to the remote repository:
$ git push origin --delete merge2
```

## 3. Advanced stuff



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

Create a new named *rebase_master*:
```
$ git checkout -b rebase_master
```
- Add a new file *wimp.py*, which is a class that creates a WIMP dark matter particle:
```
class Wimp: 
	v = 230 # km/s 
	def __init__(self, mass): 
		self.m = mass # GeV
		print("A new WIMP particle has been created!\nmass: {} GeV\nv = {}".format(self.m, self
		.v))
W = Wimp(100)
```
We would like to add a new class to create the target nucleus on the detector. The first step that we are going to take is to create a new branch named *nucleus*.
```
$ git checkout -b nucleus
```
- Add the following part of code inside wimp.py just below the WIMP class:
```
class Nucleus:
	v = 0 # at rest
	def __init__(self, Z, N):
		self.Z = Z 
		self.N = N
		self.A = self.Z + self.N
		self.M = 931.5 * A * 1e-3 # GeV
		print("A new nucleus has been created!\nMass number: {}\nMass: {} #GeV".format(self.A, self.M))
N = Nucleus(18, 22)
```
- Commit the modification with the message 'add nucleus to wimp.py'. 
- At the moment you are working your collaborator creates a new file on *rebase_master*:
```
$ touch newfile.txt
```
- Commit it and run **git --all --decorate --oneline --graph - 4**. Notice that the
  working flow are no longer linear. 
- Finally, checkout to *nucleus* branch and run:
```
$ git rebase rebase_master
```
- See how the working flow have change. The history of *nucleus* has been erased!
- Let's finalize this example checking that the information contained in each branch is
  the same than before the rebase. This implies that we need to merge those two branches
in order to collect the modifications.


## 3. Workflows
Here, we will review good practices in regards to working as  a team. 
### Pull Requests & Issues
Doing a pull request is a way of merging two branches using the GitHub online interface. Issues can be used to keep tracks of enhancements. 

### Gitflows
1. There is a version of the project which is considered the source of thruth and it is a remote repository.
2. Issues are created as statements of problems and bugs... , and possible enhacements to our software. 
3. For every issue it is recommended to create *a new branch* and work on that issue, never modifying master. 
4. After satisfactorily modifying our software in the *the new branch*, request for a team review and pull request. 

Note that  pull requests can be created at the beginning . Future improvements of our project will be reflected as commits in the correspoding pull request. Finally, when everything is ready branches can be merged. 

### Privacy

There exist two types of repositories, public and private repos. 
* Public repositories can be seen by anyone and `git clone` (fork).
* Private repositories can only be seen by owners and collaborators. 
* Permisions [link](https://help.github.com/en/articles/permission-levels-for-a-user-account-repository):  There are mainly two permission levels: Owner and collaborators. The Owner can invite collaborators **(3 for free accounts)** , change the visibility of the repository (private or public), and limit interactions with a repository (for 24h). Collaborators can only edit the repository in regards to adding and deleting content. 

Furthermore, GitHub will never acces to a private repository without the consent of the owner. However, there are [exeptions](https://help.github.com/en/articles/github-terms-of-service#e-private-repositories). 

### Licence 
Even though the repositories are set as public repositories,  one might find contrains regarding the use of a software. These contrains are usually stated in a file named as "lisense". Mostly, software can be used but has to be cited.   

## Hacktoberfest
Most important event ever taking place in October. 
## References
* [Git](https://git-scm.com/)
* [GitHub](https://github.com/)
* [bitbucket](https://bitbucket.org/)
* [xuanxu](https://github.com/xuanxu/)
* [Chacon, S., & Straub, B. (2014). Pro git. Apress.](https://git-scm.com/book/en/v2)
* [Version control with Git, Coursera](https://www.coursera.org/learn/version-control-with-git)
* [Software Carpentry, version control with Git](https://swcarpentry.github.io/git-novice/)
* [hacktoberfest 2019](https://hacktoberfest.digitalocean.com/)
