- [Git](#git)
  * [About Git](#about-git)
  * [Internal Operation](#internal-operation)
  * [A first repository](#a-first-repository)
    + [Working in Terminal](#working-in-terminal)
    + [Create a new git-repository](#create-a-new-git-repository)
    + [Track & commit files](#track---commit-files)
    + [Modify files](#modify-files)
    + [git add -A .](#git-add--a-)
  * [Undo changes](#undo-changes)
    + [Undo changes before staging](#undo-changes-before-staging)
    + [Undo changes after staging](#undo-changes-after-staging)
    + [Undo commits](#undo-commits)
  * [Ignore files](#ignore-files)
    + [Delete files](#delete-files)
    + [Delete files & folders from the commit history](#delete-files---folders-from-the-commit-history)
    + [.gitignore](#gitignore)
  * [Collaboration with git](#collaboration-with-git)
    + [Create & link GitHub account](#create---link-github-account)
    + [Create repository & first push](#create-repository---first-push)
    + [Create gitignore](#create-gitignore)
    + [Git add - commit - push](#git-add---commit---push)
    + [Pull existing repository](#pull-existing-repository)
    + [push - pull](#push---pull)
    + [rebase](#rebase)
  * [Merge conflicts](#merge-conflicts)
  * [Git branches](#git-branches)
  * [Git Resources](#git-resources)

# Git #
## About Git ##
Git is a version control system. It allows you to collaborate on projects with several people and to keep a history of the project.

It was launched in April 2005 by Linus Torvalds - the father of Linux. Code management systems were nothing new, some important systems in the past were:

* SCSS early 1970s
* RCS early 80s
* CVS was launched in 1986
* SVN in 2001

Linux development was done in the early years with Bitkeeper VCS. However, in 2005 Bitkeeper imposed some additional restrictions on the free open source version, so that Linux could no longer be developed via this system. Linus looked for alternatives, but found none that met his requirements:

* Easy to do distributed development
* Being scalable: being able to collaborate with 1000+ developers
* Being Fast & Efficient and Reliable
* Know who did what
* Transaction support: bundle multiple actions
* Branching support: branches of the project that can be merged back into the main project.
* Distributed repositories: project with history is not kept centrally.
* For free

When he couldn't find an alternative that met these requirements, he decided to develop his own system: GIT was born.

The name GIT is not an abbreviation, but a reference to Linus himself: it is slang for "an unpleasant person". Like Linux, he wanted a name that refers to himself. Afterwards, the community put the abbreviation "Global Information Tracker" on it.

## Internal Operation ##

Your files are stored in a repository. This repository contains information about the contents of the files, their name, location and history.

* the contents of files are stored in blob objects
* history is kept in commit objects
* the structure is maintained in tree objects

If you have multiple files with the same content, the tree will reference the same blob object multiple times, saving storage.

## A first repository

We will use git from the command line. There are some applications that allow you to execute git commands via a GUI, but if you want to perform more advanced actions you will have to go back to the command line anyway.

Git is installed when you install the xcode command line tools. So if you have already done this (for example to make Node.js work), you can get started right away. Another option (without the command line tools) is to download and install git from [http://git-scm.com/downloads](http://git-scm.com/downloads).

### Working in Terminal

Before we start using git specific commands, let's do a quick refresher on some important Terminal commands. The following commands should be easy for any developer to use:

* `ls`: Display a list of files and folders in the current folder. If you also want to see the hidden files & the file attributes, you can run `ls -al`.
* `cd foldername`: Navigates to the folder named after the command. This folder will then become the active folder in your Terminal. In this example, navigate to the folder named "foldername". Instead of a relative name (ie a name of a folder that is in the current active folder), you can also enter a full path (starting with a forward slash). Tip: you can drag a folder or file from your finder to the terminal window to place the full path to that folder or file in the window.
* `cd ..`: Navigate to the parent directory so that it becomes the active directory.
* `mkdir foldername`: create a folder with the name specified after the command. In this case, create a folder called "foldername" in the active folder.
* `rm -d foldername`: delete a particular folder. This only works if the folder is empty. If you want to delete a non-empty folder, you can use additional options: `rm -rdf foldername` will delete the folder including subfolders and files.
* `rm filename`: delete a specific file.
* `mv originalname newname`: move or rename a file. You can also use absolute / relative paths to move files to another folder.
* `cp originalname newname`: copy a file to a new location.
* `cat filename`: display the contents of a particular file in your terminal window.
* `echo "hello world"`: display the text between the quotes in the terminal window.

By using the `tab` key, you can trigger autocomplete on commands or file and folder names. Type part of the command or part of the path and press tab to autocomplete. This way you can save a lot of time, and you also avoid typing errors.

You can also write output from a command to a file, using the `>` character:

* `ls > test.txt` will write the output of the ls command to a file called test.txt.
* `echo "hello world" > hello.txt` will write the output of the echo command (the text "hello world") to a file called hello.txt.

These are some basic commands you should know by head. This is nothing git specific! You will also use these commands when getting started with Node.js and module bundlers like Gulp, Webpack or ViteJS.

### Create a new git-repository

You can turn any existing directory into a git repository with the `git init` command. It doesn't matter if there are already files or subfolders in it. We will start with a new empty directory, but know that this is not necessary to manage a project via git.

Create a new directory and make it a git repository (note: the dollar signs indicate that this is command line input by the user, you don't type them):

	$ mkdir project
	$ cd project
	$ git init
	Initialized empty Git repository in /Users/frederikduchi/Documents/development3/project/.git/

The `git init` command will create a hidden folder called .git. This contains all information about the repository & its history.

Via the `git status` command you can get some more information about the current status of the repository. You often use this command to see which files have been changed, whether there are new files, or whether files have been deleted.

	$ git status
	# On branch master
	#
	# No commits yet
	#
	nothing to commit (create/copy files and use "git add" to track)

### Track & commit files

Create a new file hello.txt with the text "hello world":

	$ echo "hello world" > hello.txt

Execute the `git status` command again:

	$ git status
	# On branch master
	#
	# No commits yet
	#
	# Untracked files:
	#   (use "git add <file>..." to include in what will be committed)
	#
	#	hello.txt
	nothing added to commit but untracked files present (use "git add" to track)

Git informs us that there are files in your directory that are not yet tracked by Git (untracked files present). If you want to keep track of the files, you have to add them with the `git add` command:

	$ git add hello.txt
	$ git status
	# On branch master
	#
	# No commits yet
	#
	# Changes to be committed:
	#   (use "git restore --staged <file>..." to unstage)
	#
	#	new file:   hello.txt
	#

Now git is aware of that file. This does not mean that git will automatically take a snapshot of every change to that file. You have to decide when to take a snapshot of the changes in your file(s) and add it to your git history. You do this by executing a commit:
	
	$ git commit -m "first commit"
	[master (root-commit) 5588c39] first commit
	 1 file changed, 1 insertion(+)
	 create mode 100644 hello.txt

`git add` and `git commit` are two commands that you will use a lot when working with git.

### Modify files

Edit the contents of the file to "hello devine", and execute the git status command:

	$ echo "hello devine" > hello.txt
	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git restore <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

Git has detected changes to an already tracked file. You will need to "add" this file again to queue the changes for a commit (called stage for commit):

	$ git add hello.txt

Commit the changes:

	$ git commit -m "changed world to devine"
	[master 7f65053] changed world to devine
	 1 file changed, 1 insertion(+), 1 deletion(-)

Of course you can also add and commit multiple changes in a single command. Edit the text, and create a second file:

	$ echo "hello development 3" > hello.txt
	$ echo "hello" > world.txt

Git status will now report 2 things: modifying an already tracked file, and detecting a new file that is not yet tracked:

	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git restore <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	# Untracked files:
	#   (use "git add <file>..." to include in what will be committed)
	#
	#	world.txt
	no changes added to commit (use "git add" and/or "git commit -a")

You can now stage these two files separately by executing a git add twice, but you can also do this at once, by using `git add .`

	$ git add .
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git restore --staged <file>..." to unstage)
	#
	#	modified:   hello.txt
	#	new file:   world.txt
	#

Now both are staged for commit, and with a single commit you can log them into the git repository:

	$ git commit -m "welcome dev3 + new world file"
	 [master 9720321] welcome dev3 + new world file
	 2 files changed, 2 insertions(+), 1 deletion(-)
	 create mode 100644 world.txt

### git add -A . ###

We've seen before that with `git add .` you can stage all changes before commit. Keep in mind that deletes (deleting files) are not staged. To do that, you need to add the -A flag to the command.

## Undo changes

There are 3 scenarios where you might want to undo changes:

1. When you've made changes, but haven't added yet.
2. When changes have been added, but not yet committed
3. When you want to revert to an earlier version after a commit.

In any of these scenarios, you can undo changes by using the appropriate git commands.

### Undo changes before staging

Change the text in hello.txt back to "hello devine", but don't add it yet:

	$ echo "hello devine" > hello.txt

Execute a git status, git detected changes that are not yet staged for commit:

	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git restore <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

Here's a hint on how to undo the changes to your working directory: via the git restore command. Run this command, and check the status of the repository:

	$ git restore hello.txt
	$ git status
	# On branch master
	nothing to commit (working directory clean)

The changes to hello.txt have been undone. If you view the contents of the file via the cat command, you will see that it contains the contents of your last commit:

	$ cat hello.txt
	hello development 3

### Undo changes after staging

Change the text again to "hello devine", stage these changes via the add command, but don't commit it yet:

	$ echo "hello devine" > hello.txt
	$ git add hello.txt
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git restore --staged <file>..." to unstage)
	#
	#	modified:   hello.txt
	#

You get a hint on how to unstage these changes: via git restore --staged:

	$ git restore --staged hello.txt

De file is nog steeds gewijzigd, maar de wijzigingen zijn niet meer gestaged:

	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git restore <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

You can now definitively undo this, by using - just like in the previous topic - git restore:

	$ git restore hello.txt

### Undo commits

Let's say you've committed some changes, but for some reason you want to undo them.

	$ echo "hello devine" > hello.txt
	$ git add hello.txt
	$ git commit -m "changed, but not sure about it"

You can do 2 things: either create a new commit that undoes the changes from the previous commit (`git revert HEAD`), or completely clear the commit from history (`git reset --hard reference-to-commit` ).

	$ git revert HEAD

Your terminal will now display a vim or nano editor, into which you can type a commit message. Edit the default message if you want, and type in vim `:quit` when you're done. For nano, use Ctrl + X, followed by Yes.

	[master 2bc740f] Revert "changed, but not sure about it"
	 1 file changed, 1 insertion(+), 1 deletion(-)

The file will now contain the contents from before the last commit.

You can also set a different editor for the merge message edits. Instead of vim, nano is a more user-friendly alternative:

```bash
git config --global core.editor "nano"
```

By the way, you can view a repository's commit history with the `git log` command:

	$ git log
	commit 2bc740f2af93348267c6b3558e1037c5db540600 (HEAD -> master)
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:57:33 2021 +0200

	    Revert "changed, but not sure about it"

	    This reverts commit 8d977cb2d4855a782e261015645e017c1e128000.

	commit 8d977cb2d4855a782e261015645e017c1e128000
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:56:55 2021 +0200

	    changed, but not sure about it

	commit 5aa411822d8546ef1cd73addc20a022a74deae91
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:54:26 2021 +0200

	    changed, but not sure about it

	commit 9720321677e0798b540b287398edeaadcb630b17
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:35:21 2021 +0200

	    welcome dev3 + new world file

	commit 7f65053ee86593fb29a3102e03f7ae3f44b112d7
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:32:22 2021 +0200

	    changed world to devine

	commit 5588c399cd15bc841c89158d72cc4d3938581196
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:30:22 2021 +0200

	    first commit


You can see that the "wrong" commit is still in the git history, and the changes were undone via a new commit. Also note that each commit has a unique SHA1 hash id. You can use these ids to specify commits on certain commands.

A more drastic way to undo commits is with the `git reset` command. With git reset you are going to reset your working tree to a particular commit and delete all commits after that commit from the repository.

We want to go back to the state of our commit "welcome dev3 + new world file". Through git log, we find out that the SHA1 id is `9720321677e0798b540b287398edeaadcb630b17`. Specify the SHA1 id of the commit to where you want to reset after the command. You don't have to specify the entire id: the first 4 characters are often sufficient (at least if they are unique):

	$ git reset --hard 9720
	HEAD is now at 9720321 welcome dev3 + new world file

Now when you run git log again, you will see that the commits after 9720 are gone:

	$ git log
	commit 9720321677e0798b540b287398edeaadcb630b17 (HEAD -> master)
	Author: Frederik Duchi <frederik.duchi@telenet.be>
	Date:   Wed Sep 1 09:35:21 2021 +0200

	    welcome dev3 + new world file

	commit 7f65053ee86593fb29a3102e03f7ae3f44b112d7
	Author: Frederik Duchi <frederik.duchi@telenet.be>
	Date:   Wed Sep 1 09:32:22 2021 +0200

	    changed world to devine

	commit 5588c399cd15bc841c89158d72cc4d3938581196
	Author: Frederik Duchi <frederik.duchi@telenet.be>
	Date:   Wed Sep 1 09:30:22 2021 +0200

	    first commit

You will only use such a `git reset` command to undo local commits. Once you're collaborating with others, and commits have already been distributed to other users, you use the `git revert` command to create a new commit that undoes a previous commit.

## Ignore files
It won't be necessary to keep track of all the files in a project folder via Git. For example, it is not a good idea to track a `node_modules` folder in your repository. Also hidden system files, such as `.DS_Store` are of no use in a repository.

Initialize your map as a node project, and link for example webpack to this project:

```bash
$ npm init -y
$ npm install webpack --dev
```

We will commit `node_modules` "by accident" to set it straight afterwards

```bash
$ git add .
$ git commit -m "initial project"
[master 0ead6d0] initial project
 2435 files changed, 385719 insertions(+)
 create mode 120000 node_modules/.bin/acorn
 create mode 120000 node_modules/.bin/browserslist
 create mode 120000 node_modules/.bin/terser
 ...
 create mode 100644 node_modules/yocto-queue/license
 create mode 100644 node_modules/yocto-queue/package.json
 create mode 100644 node_modules/yocto-queue/readme.md
 create mode 100644 package-lock.json
 create mode 100644 package.json

 ```

### Delete files

You have now added the entire project, including the `node_modules`, to your git repository.

This is overkill, there is no need to store the entire dependency tree in your git repository. We will now correct this error:

	$ git rm -r --cached node_modules/
	rm 'node_modules/.bin/acorn'
	rm 'node_modules/.bin/browserslist'
	rm 'node_modules/.bin/terser'
	rm 'node_modules/.bin/webpack'
	rm 'node_modules/@types/eslint-scope/LICENSE'
	rm 'node_modules/@types/eslint-scope/README.md'

	...

The --cached option causes the file to be deleted from the repository index, but remains in your filesystem.

A git status now gives the following result:

	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git restore --staged <file>..." to unstage)
	#
	#	deleted:    node_modules/.bin/acorn
	#	deleted:    node_modules/.bin/browserslist
	#	deleted:    node_modules/.bin/terser
	#	deleted:    node_modules/.bin/webpack
	#	deleted:    node_modules/@types/eslint-scope/LICENSE
	#	deleted:    node_modules/@types/eslint-scope/README.md
	...

Add & commit these deletes by using the flag -A  in the add command:

	$ git add -A .
	$ git commit -m "removed node_modules folder"
	On branch master
	nothing to commit, working tree clean

### Delete files & folders from the commit history

We just created a commit removing the `node_modules` folder. However, there is still a commit where these `node_modules` are present, making our repository unnecessarily large. If you want to remove folders or files from the entire history of your project, you have to go one step further.

You can edit the git history using the git `filter-branch` command. To clear our `node_modules` folder, let's do the following:

	$ git filter-branch --tree-filter 'rm -rf node_modules' HEAD
	WARNING: git-filter-branch has a glut of gotchas generating mangled history
	 rewrites.  Hit Ctrl-C before proceeding to abort, then use an
	 alternative filtering tool such as 'git filter-repo'
	 (https://github.com/newren/git-filter-repo/) instead.  See the
	 filter-branch manual page for more details; to squelch this warning,
	 set FILTER_BRANCH_SQUELCH_WARNING=1.
	Proceeding with filter-branch...


The folder will be deleted on your file system and in the history. Note, when you re-link the `node_modules` via npm, you may accidentally re-add them to the history, which is not the intention. We will avoid this by using a `.gitignore` file.

### .gitignore
We will now specify which files we don't want to track in the future. This can be done with a `.gitignore` file. This is a text file in your repository that specifies which files and directories are allowed to be ignored by git.

Create a new file called `.gitignore` in the root of your repository. Give this the following content:

	.DS_Store
	node_modules/

This will cause the `.DS_Store` file and the `node_modules` folder (& all subfolders of `node_modules` and subfolders with this name) to be ignored in the future.

Add and commit this file to include it in your repository.

	$ git add -A .
	$ git commit -m "added .gitignore"

In practice you will create such a `.gitignore` file as one of your first files. This way you avoid "contaminating" your repository with unnecessary files, and you avoid drastic actions such as deleting folders & files from the history.
A list of useful .gitignore files can be found here: https://github.com/github/gitignore

## Collaboration with git

So far we have worked locally with git. You can also collaborate with several people on 1 repository by working with a remote server. Everyone has a local copy of the repository, and can synchronize their changes via a remote server with other people who have the repository.

In theory, you can use any computer on which you have installed the git command tools as a server. It's just not that practical to work together from home, you have to make sure that your computer can be reached externally and everyone who works together must know your ip address or hostname.

That is why we use a hosted git environment. There are several options for this, we will use GitHub.

### Create & link GitHub account

We will create a GitHub account and link our GitHub credentials to our computer, so that we don't have to re-enter our password every time.

Visit [https://github.com](https://github.com) and create an account. Then go to [https://education.github.com/pack](https://education.github.com/pack) and request an educational pack by clicking _Get your pack_, this will be useful to create private repositories.

Then open a terminal window. We'll link our name & email address to git so git knows who is doing a commit. Make sure your email address is the one you used to create your GitHub account:
	$ git config --global user.name "Your Name Here"
	$ git config --global user.email "your_email@example.com"

Next, we configure git to sue our OSX keychain to store passwords:

	$ git config --global credential.helper osxkeychain

### Create repository & first push

Login to your GitHub account, and click the "New repository" button. Choose a name for your repository and click the "Create Repository" button.

Open a terminal window and navigate via `cd` commands to the directory of the git repository containing the "hello world" files. We will make sure that we can synchronize our local repository via GitHub, by adding a "remote". A remote is a location where you can synchronize a git repository:

	$ git remote add origin https://github.com/frederikduchi/dev3-demo.git
	$ git branch -M main
	$ git push -u origin main
	Enumerating objects: 17, done.
	Counting objects: 100% (17/17), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (10/10), done.
	Writing objects: 100% (17/17), 8.98 KiB | 4.49 MiB/s, done.
	Total 17 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), done.
	To https://github.com/frederikduchi/dev3-demo.git
	 * [new branch]      main -> main
	Branch 'main' set up to track remote branch 'main' from 'origin'.

The `git push` command will upload local, unsynchronized changes to the remote location. You use the `-u` attribute the very first time, to ensure that you don't have to specify the remote name in future synchronizations. You can then just run `git push` in the future.

### Create gitignore

Don't forget to create a `.gitignore` file right away, including ignores for `node_modules`, `.DS_Store` and possibly `dist`. This way you avoid that these folders and files are synchronized!

### Git add - commit - push

From now on you can start pushing commits to the online repository. Usually you bundle several local commits when you push. In fact, we already did this with our first push: all the commits we ran earlier are now also in the online repository.

Delete the `world.txt` file, add & commit. We use `git add -u .` to ensure that the delete action of that file is staged:

	$ rm world.txt
	$ git add -u .
	$ git commit -m "removed world file"
	[master 0b0d3b8] removed world file
	 1 file changed, 1 deletion(-)
	 delete mode 100644 world.txt

Create a README.md file, with a little info about the repository:

	$ echo "Demo repository" > README.md
	$ git add .
	$ git commit -m "added readme file"
	[master a8515e0] added readme file
	 1 file changed, 1 insertion(+)
	 create mode 100644 README.md

Execute `git status`. You can see in the status report that the repository is 2 commits ahead of the online version:

	# On branch master
	# Your branch is ahead of 'origin/main' by 2 commits.
	# (use "git push" to publish your local commits)
	nothing to commit (working directory clean)

Execute `git push` to put your commits on GitHub:

	Enumerating objects: 6, done.
	Counting objects: 100% (6/6), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (4/4), done.
	Writing objects: 100% (5/5), 488 bytes | 488.00 KiB/s, done.
	Total 5 (delta 2), reused 0 (delta 0)
	remote: Resolving deltas: 100% (2/2), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo.git
	   f1e8b69..a8515e0  main -> main

When you view the repository through your browser, you will see that the contents of the `README.md` file are shown below the list of files. This is a file in the Markdown format. Markdown is a simple markup language for formatting documents. More information about this can be found on wikipedia: [http://en.wikipedia.org/wiki/Markdown](http://en.wikipedia.org/wiki/Markdown).

### Pull existing repository

Once a repository has been created, and is on a server like GitHub, you can also download it from other computers/locations. Downloading the repository for the first time is done via the `git clone` command. From then on you can get updates via the `git pull` command. `git pull` is the inverse of `git push`, and you will use it to pull in updates you don't already have locally.

Open a second terminal window, navigate to the parent directory of your original git repository and create a directory where you will clone a duplicate of the repository:

	$ mkdir project2
	$ cd project2

Execute the git clone command to get the online repository (just change the url to your own repository:

	$ git clone https://github.com/frederikduchi/dev3-demo
	Cloning into 'dev3-demo'...
	remote: Enumerating objects: 22, done.
	remote: Counting objects: 100% (22/22), done.
	remote: Compressing objects: 100% (11/11), done.
	remote: Total 22 (delta 3), reused 22 (delta 3), pack-reused 0
	Unpacking objects: 100% (22/22), done.

You now have 2 clones from the same repository on your computer. One in the project folder and one in the project2 folder. We'll use these two to test syncs and merges.

### push - pull

We simulate collaboration with 2 users by synchronizing in two different folders with the same remote (online repository). For the following actions, pay attention to the folder in which you execute the commands (from now on the project folder will always be in front of the dollar sign in the command to be executed).

In folder 1 we create a new file `project.txt`, we add, commit and push to the remote:

	project$ echo "created in project" > project.txt
	project$ git add .
	project$ git commit -m "added project.txt file"
	[main 3dc1c52] add project.txt file
	 1 file changed, 1 insertion(+)
	 create mode 100644 project.txt
	 
	project$ git push
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 300 bytes | 300.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo.git
	   a8515e0..3dc1c52  main -> main

In folder 2 (dev3-demo) we create a new file `project2.txt`, add & commit and try to push to the remote:

	project2$ echo "created in project2" > project2.txt
	project2$ git add .
	project2$ git commit -m "added project2.txt file"
	[master 3bdfe55] added project2.txt file
	 1 file changed, 1 insertion(+)
	 create mode 100644 project2.txt
	project2$ git push
	To https://github.com/frederikduchi/dev3-demo
	 ! [rejected]        main -> main (fetch first)
	error: failed to push some refs to 'https://github.com/frederikduchi/dev3-demo'
	hint: Updates were rejected because the remote contains work that you do
	hint: not have locally. This is usually caused by another repository pushing
	hint: to the same ref. You may want to first integrate the remote changes
	hint: (e.g., 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.


We get an error: there are new commits on the remote that we haven't pulled into our project2 clone yet. We have to pull these first before we can do a push:

	project2$ git pull

We are presented with a vim or nano editor to perform a merge. You can enter a custom message here. Enter `:quit` to close the vim editor and continue the merge.

	remote: Enumerating objects: 4, done.
	remote: Counting objects: 100% (4/4), done.
	remote: Compressing objects: 100% (1/1), done.
	remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
	Unpacking objects: 100% (3/3), done.
	From https://github.com/frederikduchi/dev3-demo
	   a8515e0..3dc1c52  main       -> origin/main
	Merge made by the 'recursive' strategy.
	 project.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 project.txt

When you execute `git status`, you will see that you are 2 commits ahead of the remote: 1 commit is the merge commit, and a second commit is the `project2.txt` commit:

	project2$ git status
	# On branch main
	# Your branch is ahead of 'origin/main' by 2 commits.
	#
	nothing to commit (working directory clean)

Push the commits again to the remote. It succeeds this time.

	project2$ git push
	Enumerating objects: 7, done.
	Counting objects: 100% (7/7), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (4/4), done.
	Writing objects: 100% (5/5), 551 bytes | 551.00 KiB/s, done.
	Total 5 (delta 2), reused 0 (delta 0)
	remote: Resolving deltas: 100% (2/2), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo
	   3dc1c52..c18628a  main -> main


Now also get these commits in your first folder (don't forget to switch folders) via a `git pull` command:

	project$ git pull
	remote: Enumerating objects: 7, done.
	remote: Counting objects: 100% (7/7), done.
	remote: Compressing objects: 100% (2/2), done.
	remote: Total 5 (delta 2), reused 5 (delta 2), pack-reused 0
	Unpacking objects: 100% (5/5), done.
	From https://github.com/frederikduchi/dev3-demo
	   3dc1c52..c18628a  main       -> origin/main
	Updating 3dc1c52..c18628a
	Fast-forward
	 project2.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 project2.txt

### rebase

We will work with a centralized workflow for the time being: we work with several people on 1 master branch via 1 remote. There are other more advanced workflows that work through branches and forks. However, these are a bit more complex.

In the previous scenario, we added a merge commit to fast-forward an out-of-date repository. This is not optimal in a centralized workflow: it is better to use a rebase with the `git pull`. A rebase will execute all commits from the remote first, and execute your commits after it, instead of executing a merge commit by default.

Delete `project.txt` in the project folder:

	project$ rm project.txt
	project$ git add -u .
	project$ git commit -m "removed project.txt"
	[main de80b79] removed project.txt
	 1 file changed, 1 deletion(-)
	 delete mode 100644 project.txt
	project$ git push
	Enumerating objects: 3, done.
	Counting objects: 100% (3/3), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (2/2), 233 bytes | 233.00 KiB/s, done.
	Total 2 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo.git
	   c18628a..de80b79  main -> main

Then delete `project2.txt` in the `project2` folder. We will also have to do a pull here before we can push. The difference with the pull is that we pass a rebase flag, to ensure that all commits from the remote repository are executed first, and then our own commits:

	project2$ rm project2.txt
	project2$ git add -u .
	project2$ git commit -m "removed project2.txt"
	[main 6be65fb] removed project2.txt
	 1 file changed, 1 deletion(-)
	 delete mode 100644 project2.txt
	 
	project2$ git pull --rebase
	remote: Enumerating objects: 3, done.
	remote: Counting objects: 100% (3/3), done.
	remote: Compressing objects: 100% (1/1), done.
	remote: Total 2 (delta 1), reused 2 (delta 1), pack-reused 0
	Unpacking objects: 100% (2/2), done.
	From https://github.com/frederikduchi/dev3-demo
	   c18628a..de80b79  main       -> origin/main
	First, rewinding head to replay your work on top of it...
	Applying: removed project2.txt


This way, no merge commit is created. When you execute `git status` you see that you are now only 1 commit ahead of the remote repository, instead of 2:

	project2$ git status
	# On branch main
	# Your branch is ahead of 'origin/main' by 1 commit.
	  (use "git push" to publish your local commits)
	#
	nothing to commit (working directory clean)

Push to the remote repository. Also pull in the projects folder so that both repositories are up to date.

## Merge conflicts

So far we have only made changes in separate files. However, it can happen that you have made changes to the same file with 2 people, and that a conflict occurs.

In the `project` folder, edit the text in `hello.txt` and push it to the remote repository:

	project$ echo "edit in project" > hello.txt
	project$ git add .
	project$ git commit -m "changed hello.txt"
	[main f1c4e08] changed hello.txt
	 1 file changed, 1 insertion(+), 1 deletion(-)
	 
	project$ git push
	Enumerating objects: 5, done.
	Counting objects: 100% (5/5), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 284 bytes | 284.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo.git
	   8f2400d..f1c4e08  main -> main

Als edit the text of hello.txt in the project2 folder

	project2$ echo "edit in project2" > hello.txt
	project2$ git add .
	project2$ git commit -m "changed hello.txt in project2"
	[main 45b7ea9] chenged hello.txt in project2
	 1 file changed, 1 insertion(+), 1 deletion(-)
	 
	project2$ git push
	To https://github.com/frederikduchi/dev3-demo
	 ! [rejected]        main -> main (fetch first)
	error: failed to push some refs to 'https://github.com/frederikduchi/dev3-demo'
	hint: Updates were rejected because the remote contains work that you do
	hint: not have locally. This is usually caused by another repository pushing
	hint: to the same ref. You may want to first integrate the remote changes
	hint: (e.g., 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.

We first pull before we can push

	project2$ git pull --rebase
	remote: Enumerating objects: 5, done.
	remote: Counting objects: 100% (5/5), done.
	remote: Compressing objects: 100% (1/1), done.
	remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
	Unpacking objects: 100% (3/3), done.
	From https://github.com/frederikduchi/dev3-demo
	   8f2400d..f1c4e08  main       -> origin/main
	First, rewinding head to replay your work on top of it...
	Applying: chenged hello.txt in project2
	Using index info to reconstruct a base tree...
	M	hello.txt
	Falling back to patching base and 3-way merge...
	Auto-merging hello.txt
	CONFLICT (content): Merge conflict in hello.txt
	error: Failed to merge in the changes.
	Patch failed at 0001 chenged hello.txt in project2
	hint: Use 'git am --show-current-patch' to see the failed patch
	Resolve all conflicts manually, mark them as resolved with
	"git add/rm <conflicted_files>", then run "git rebase --continue".
	You can instead skip this commit: run "git rebase --skip".
	To abort and get back to the state before "git rebase", run "git rebase --abort".


We get a merge conflict, because we changed the same file in both repositories. We need to resolve this conflict before the rebase can continue.

Via `git status` you can request a list of the merge conflicts:

	project2$ git status
	#rebase in progress; onto f1c4e08
	#You are currently rebasing branch 'main' on 'f1c4e08'.
	#  (fix conflicts and then run "git rebase --continue")
	#  (use "git rebase --skip" to skip this patch)
	#  (use "git rebase --abort" to check out the original branch)
	#
	#Unmerged paths:
	#  (use "git restore --staged <file>..." to unstage)
	#  (use "git add <file>..." to mark resolution)
	#	both modified:   hello.txt
	no changes added to commit (use "git add" and/or "git commit -a")

You will be notified that you are rebasing. At "Unmerged paths" you see the files that are in conflict. You must first resolve the conflict by editing the file before continuing with the rebase.

Open the txt file in a text editor. You notice that the content from `project` and `project2` is present:

	<<<<<<< HEAD
	edit in project
	=======
	edit in project2
	>>>>>>> changed hello.txt in project2

Adjust the text to:

	edit in project
	and edit in project2

Add this to the rebase action and use the continue flag

	project2$ git add hello.txt
	project2$ git rebase --continue
	Applying: changed hello.txt in project2

Now when you execute git status, you will see that you are on the master / main branch again, and you are 1 commit ahead of the remote:

	project2$ git status
	# On branch main
	# Your branch is ahead of 'origin/main' by 1 commit.
	#
	nothing to commit (working directory clean)

Now you can push again to the remote

	project2$ git push
	Counting objects: 5, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 326 bytes, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To https://github.com/devinekask/git-demo
	   7f3b200..920c81f  master -> master

Execute `git pull` in the other folder so that both are synced again.


## Git branches
You can also use branches via Git.

You can use branches to:
- Develop new features
- Bug fixes
- Experiment with new ideas without influencing your production code (code that is online)

This is a walkthrough to work with 2 branches, namely `develop` and `master` branches. You can find the production ready code on the `master` branch. On the `develop` branch, on the other hand, you can push code that is not yet completely ready to show to your end user.

Once you're happy with the (bug-free) code in the `develop` branch, you can merge it into the `master` branch. This process is explained further.

You continue working on the current project.

Create a branch `develop` by executing the following command:

	$ git branch develop

Get an overview of all the branches

	$ git branch

Now that we have created a new `develop` branch, we can switch to it by running `git checkout develop`:

	$ git checkout develop

Push this `develop` branch to remote and check the result on GitHub

	$ git push origin develop

Make some commits on the `develop` branch. Feel free to push these to Github in between (via `git push origin develop`).

We would now like to merge our code from `develop` with our `master` code, so that both branches contain the same code (now `develop` has more commits than `master`, i.e. `develop` stands before `master` - check the differences in Github). For this we first have to switch back to our `master` branch and merge `develop` into it in a next step:

	$ git checkout main

The merge of `develop` in `master` is done by the `git merge` command:

	$ git merge develop main

Switch back to `develop` immediately so you don't accidentally develop in the `master` branch (we want our `develop` branch to always have the most recent code):

	$ git checkout develop

Push the branches:

	$ git push origin main
	$ git push origin develop

Alternatively, you can also push them all at once:

	$ git push --all origin

At a different location (computer) you can then pull in the branches:

	$ git pull --rebase origin develop
	$ git pull --rebase origin main

## Git Resources

This is a basic introduction to get you started with git. There's a lot more you can do with git & github. More information & tutorials can be found at the following locations:

* [https://www.atlassian.com/git/](https://www.atlassian.com/git/)
* [https://help.github.com/](https://help.github.com/)
* [http://git-scm.com/book](http://git-scm.com/book)
