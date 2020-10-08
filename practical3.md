---
layout: page
title: Practical 3
permalink: /practical3/
---

# Objectives

The learning objectives for this practical are:

 * Setting up Git
 * Setting up a Git repo in our local disk.
 * Update your local repository.
 * Upload your local repository to GitHub.
 * Cloning a GitHub repo into a local repository.
 * Push changes to GitHub.
 * Pull changes from GitHub.

# Setup and background

We will download again some COVID19 data. Please follow the next two steps:

1. Go to the Catalan Health Departament COVID data portal at [https://dadescovid.cat](https://dadescovid.cat)
   and switch the language to "ENGLISH" using the pull-down menu on the top-right corner of the page.
2. Follow the downloads link and on the next page click and download the two
   files corresponding to the "7 DAY AGGREGATION" for "CATALUNYA" and "COUNTIES"
   ("COMARQUES" in Catalan). It is important that you download both files in the
   same day to make them comparable, because all data is updated daily. Make sure you know
   exactly where in your filesystem these two files have been downloaded.
   **Tip:** some browsers automatically download files into a folder called "Downloads"
   or under a name corresponding to the translation of "Downloads" to the default
   language of your operating system.
3. Make a directory in your filesystem, for instance at your _home_ directory,
   called `practical3` and copy in it the CSV files contained in the previous two
   ZIP files that you have downloaded, as you analogously did in practical 1 and 2.

# Setting up Git

We start setting up some global options for Git. You only need to do this once in your
computer. Make sure you have git installed in your system by opening the Unix shell and typing:
```
$ which git
```
If you get no answer from this command, it means that you need to install the Git software.
Check out the [setup](/setup/) page for instructions about how to install it. Once git is
installed, please verify the version of git you have by typing:

```
$ git --version
```
Now you should set up your identity with Git by giving your name and email address. This
information is important because Git will store it in every commit and will allow you and
others to track which changes you have made. To set up your identity type:

```
$ git config --global user.name "XXXXX YYYY"
$ git config --global user.email "ZZZZ@WWWW.UUUU"
```
where `XXXXX` is your first name and `YYYYY` is your family name, while
`ZZZZ@WWWW.UUUU` if you student UPF email address.

It may be handy to set up your favorite text editor associated with Git, so that when
Git requires you to write some text, your favorite text editor is launched. Please check
the following [link](https://docs.github.com/en/free-pro-team@latest/github/using-git/associating-text-editors-with-git) to find out how to set your favorite text editor associated with Git. If you don't
set up any text editor, it's likely that, when Git needs it, it will start a classical
text editor, such as Vi or Emacs. In the case of Vi, to write you need first to press the
key of letter 'i' and then you can type your text. Once you're finished, press Esc, colon (:) and
type 'x' for save and quit.

To verify that you have set up your global configuration data correctly, please type:

```
$ git config -l
```

Git has built-in documentation that you can access in different ways:

```
$ git help
$ git help command
$ git command --help
```
where `command` is one of Git's commands such as `add` or `checkout`.

# Setting up a Git repo in our local disk

Here we are going to set up our first Git repo in our local disk. First make sure you have
a directory called `practical3` with the two CSV files `cataluna_setmanal.csv' and
'comarques_setmanal.csv'. Now, enter the `practical3` directory and type the following:

```
$ git init
```
Verify that the `.git` database directory has been created by typing (you should see a
directory called `.git/` next to your CSV files):

```
$ ls -lhaF
drwxr-xr-x  5 robert  staff   160B Oct  7 17:49 ./
drwxr-xr-x  7 robert  staff   224B Oct  7 17:49 ../
drwxr-xr-x  9 robert  staff   288B Oct  7 17:49 .git/
-rw-r--r--@ 1 robert  staff   1.4M Oct  7 17:49 catalunya_setmanal.csv
-rw-r--r--  1 robert  staff   800K Oct  7 17:49 comarques_setmanal.csv
```

Checkout the status of your Git repo using `git status`:

```
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	catalunya_setmanal.csv
	comarques_setmanal.csv

nothing added to commit but untracked files present (use "git add" to track)
```

You should note that we have two modified files that are "untracked" (unstaged).
Stage those files by using the `git add` command and check the status again:

```
$ git add .
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   catalunya_setmanal.csv
	new file:   comarques_setmanal.csv
```

Finally, commit the staged files by doing:

```
$ git commit -m 'First commit.'
[master (root-commit) d35b756] First commit.
 2 files changed, 26965 insertions(+)
 create mode 100644 catalunya_setmanal.csv
 create mode 100644 comarques_setmanal.csv
```

Check out that the status doesn't have pending commits anymore:

```
$ git status
On branch master
nothing to commit, working tree clean
```

Examine this first change with `git log`:

```
$ git log
commit d35b7567e8ddef0534303737e0b8b3a51b4c0ec6 (HEAD -> master)
Author: Robert Castelo <robert.castelo@upf.edu>
Date:   Thu Oct 7 17:55:50 2020 +0200

    First commit.
```

# Update your local repository

Here we want to practise how to update the local repository, keeping track of the
changes with Git. First, create a file called `catalunya_setmanal_geriatric.csv`
with the subset of the data in `catalunay_setmanal.csv` corresponding to the
population that lives in geriatric residences (see practical 2). Once you have
generated that file, check out the status of the repo. You should notice that
Git has detected a new file that is untracked. Stage this untracked file and
commit the change to the repo.

# Upload your local repository to GitHub

Here we want to create in GitHub a remote repository connected to our local one.
Log into your GitHub account. Click on the plus sign on the top-right and select
"New repository" from the pull-down menu.

![](./GHnewrepo.png)

In the next page, type `practical3` in the textbox under `Repository name`, select
`Private` for the type of repository and press the button `Create repository`.

![](./GHnewrepo2.png)

At this point you have created in your GitHub account an empty repository called
`practical3`. We are going to connect it now with our local repository of
`practical3`. Make sure your CWD is the Git repository `practical3` in your local disk
and follow the instructions in the GitHub page under the title **"... or push an existing
repository from the command line"**. They consist of the following three steps:

  1. Create a new connection to your remote GitHub repo with `git remote add`,
     **replacing** the `fcbstudent` word below by your own username):
    ```
    $ git remote add origin https://github.com/fcbstudent/practical3.git
    ```
    You can check whether this connection has been successfully established by
    using the `-v` option with the `remote` command:
    ```
    $ git remote -v
    origin	https://github.com/fcbstudent/practical3.git (fetch)
    origin	https://github.com/fcbstudent/practical3.git (push)
    ```
    If you see **no** URL connection specified to the right of the word `origin`, then
    you have probably misspecified the repo URL. Before you try to add again the
    remote connection, you should remove this _bogus_ one by typing:
    ```
    $ git remote remove origin
    ```
  2. Create the default branch under the name `main`:
    ``` 
    $ git branch -M main
    ```
  3. Push the contents of the current branch in the local Git repo to the
    upstream main branch in the GitHub repo:
    ```
    $ git push -u origin main
    Enumerating objects: 4, done.
    Counting objects: 100% (4/4), done.
    Delta compression using up to 4 threads
    Compressing objects: 100% (4/4), done.
    Writing objects: 100% (4/4), 368.54 KiB | 4.24 MiB/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: Resolving deltas: 100% (1/1), done.
    To https://github.com/fcbstudent/practical3.git
     * [new branch]      main -> main
    Branch 'main' set up to track remote branch 'main' from 'origin'.
    ```
    If in this step instead of the previous output you get an error, then
    probably the connection to the remote GitHub repo has not been correctly
    established. Got back to step 1, use the given command to remove this
    current connection and try to add it again, making sure that the GitHub
    URL is correct.

Click now on the link to the private repo on the top-left of your GitHub account
to go to the page of the repo and check that the files have been successfully
uploaded to GitHub.

![](./GHnewrepo3.png)

Check out also that the status of your local repo tells that it is up to date
with the new remote connection.

```
$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

The GitHub page for the repo has several tabs, where the one called "Settings"
can be used to configure some of the other tabs and perform actions such as
switching the visibility from private to public or delete entirely this repository
from GitHub.

# Cloning a GitHub repo into a local repository

The reverse operation of uploading a local repo to a GitHub is **cloning**
a GitHub repo into a local repo. When you _clone_ a GitHub repo, you are copying
into your local filesystem all the files, version history and branches from the
GitHub repo.

To _clone_ a **public** GitHub repo into your local filesystem you use the Git
command `clone` as follows:
```
$ git clone https://github.com/USERNAME/REPONAME [DIRECTORY]
```
where `USERNAME` is the username owner of the repo you want to _clone_, while
`REPONAME` is the name of the repository you want to clone. **Optionally**, you can
give a directory name in `DIRECTORY` to clone the repo under a directory called
differently to the `REPONAME`.

To _clone_ a **private** GitHub repo into your local filesystem you use the Git
command `clone` as follows:
```
$ git clone https://USERNAME:PASSWORD@github.com/USERNAME/REPONAME [DIRECTORY]
```

It's important to know whether you are cloning a public or a private repo, because
if you use the syntax for cloning a public repo that in fact is private, then
Git will give you and error saying that it cannot find the repository.

For instance, go to your home directory and clone your recently created GitHub
repo `practical3` into a different name such as `practical3copy` by doing:

```
$ cd
$ git clone https://USERNAME:PASSWORD@github.com/USERNAME/practical3 practical3copy
```
where you should replace `USERNAME` and `PASSWORD` accordingly.

# Push changes to GitHub 

Here, we are going to see how update the new local copy of our remote GitHub repo
and send (_push_ in Git terminology) those changes to the remote GitHub repo.
Enter in the directory of this new local copy of the GitHub repo and introduce a
change by creating a `README.md` file using a Unix shell terminal output redirection
as follows:

```
$ cd practical3copy
$ cat > README.md
This is Practical 3!
```
Remember to press the keys `Ctrl+d` once you've typed the text. Now list the files,
verify that a new file called `README.md` is there, that it has the contents you've
typed and check the status of the repo:

```
$ ls
README.md                        catalunya_setmanal_geriatric.csv
catalunya_setmanal.csv           comarques_setmanal.csv
$ cat README.md 
This is Practical 3!
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md

nothing added to commit but untracked files present (use "git add" to track)
```
Stage the modified files and check the status again:
```
$ git add .
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   README.md
```
Commit the staged files and check the status again:
```
$ git commit -m 'Added README.md'
[main 7d38744] Added README.md
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
Finally, push the changes to the remote GitHub repo:
```
$ git push
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 298 bytes | 298.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/fcbstudent/practical3
   1a28e38..7d38744  main -> main
```
If this last step has been successful, you should be able to see the
new file and actually its contents as shown here below (a `README.md`
file at the root of a GitHub repo has a special
[treatment](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/about-readmes)
in the GitHub page of the repo).

![](./GHnewrepo4.png)

# Pull changes from GitHub 

You have your initial copy of the GitHub repo at `~/practical3` and
a modified copy at `~/practical3copy`, where the latter has been
synchronized with the remote GitHub repo. Now, let's see how could
we update (_pull_ in Git terminology) our initial copy with the
latest changes made in the second copy of our repo. First enter
the directory of the initial copy of the GitHub repo (here we assume
it was created at the _home_ directory) and verify it lacks the
last file `README.md` we have added to the GitHub repo:

```
$ cd
$ cd practical3
$ ls
catalunya_setmanal.csv           comarques_setmanal.csv
catalunya_setmanal_geriatric.csv
```
Second, _pull_ the changes from GitHub and verify the new file
`README.md` has been added to this copy of the GitHub repo:
```
$ git pull
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/fcbstudent/practical3
   1a28e38..7d38744  main       -> origin/main
Updating 1a28e38..7d38744
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
messi:practical3 robert$ ls
README.md                        catalunya_setmanal_geriatric.csv
catalunya_setmanal.csv           comarques_setmanal.csv
```

In general, you will not work with two local copies of the same
GitHub repo in the same computer. We have used these two copies here
only to illustrate how to _clone_ a remote repo, and _push_ and _pull_
changes from that repo. The main utility of these actions is when
either you work in two or more computers and need to synchronize your
local copies of the GitHub repo, or you are working with collaborators
that all update the same GitHub repo.
