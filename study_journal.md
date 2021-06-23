# WEEK 4 

## Entry 1 Tuesday June 15 2021

# What are Git and GitHub?

Git is a command line program wich allow us tracking versions of code and 
text files of our own.

Files being tracked are organized in a repository (directory) 
as well as all changes made to these files.

Git also allow us to do collaborations in writing software

GitHub is a web site that provides git remote repositories, and we can access
to them trhough the internet. Public repositories are free, private not.

There is also a social aspect in the fact that we can see how others 
develop their code, and interact with their development.

## Preparing Git and GitHub

We have first to create an account in the GitHub website with user name
and password.

After checking git version installed `( git --version )` we have to define
2 git variables wich are our user and email:
```
git config --global user.name [user name]
git config --global user.email [email]
```
In or working directory we'll create a folder named My_first_repo, enter
that directory and then type:

`git init`

Now we are going to add a file to this git local repository.

`echo "Wellcome to my new repository" > readme.txt`

We can see now through the command `git status` that a file has been
created on our git repository, but it is not being tracked yet.

In order to allow our file being staged by git, we should type:

`git add readme.txt`

It is important to know if we don't want git to stage a file we should type:

`git rm --cached <filename>`

Now if we type `git status` again we'll see that git is tracking a file.
At this point we have to create a milestone that will log all changes
made to this file and any other we add to be staged by git. This is 
known as a commit:

`git commit -m "added readme.txt"`

Now if we type git status again there will be nothing to do commit and the
prompt show us that our working tree is clean.

That is the way to add files to our git repository and commit their changes.
If we add several files to this repo and also add a line to our readme.txt, 
for example:

```
touch file_{1..2}.txt
echo "learning Git is going well" >> readme.txt
```
After typing `git status` again we'll see Git says there are 2 files not being
tracked and other wich has been modified. The flag -A to add command will
add all files at once to be staged:

```
git add -A
git commit -m "added two files"
```
In order to avoid and erase last changes and commits we can type
`git reset --soft HEAD~`

## Entry 2 Tuesday June 22 2021

## SUMMARY

- Git follows changes to plain text files ( code, text ).
- A directory in wich changes are staged by Git is called a Git repo.
- To stablish a new Git repo we should type `git init` in desired directory.
- Changes to filles are followed by `git add [filename]` command.
- We create milestones of our files state with command `git commit -m "comment about changes"`
- To see the state of files in directory we use `git status` command.
- We can see a list of commits of repo by typing `git log`.

# Important Git features

## Help, Logs and Diffs

We should be able to get help about any Git command by typing `git help [name of command]
Also, Git can help showing us differences between non followed changes (unstaged) of our files and the last commit.

For example, if we add a line to a file but before do add or commit we type:

`git diff [file]`

We'll get an interesting view from git showing us in red the "before changes state" and in green "new state" in a line by line way wich is very useful.

At this point, if we want to get back the file to its "before changes state", we can do this by:

`git checkout [file]` command.

## Ignoring files

It is possible that we don't want a few files to be ever staged by Git, like binaries produced by code execution (pdf, images...).
A file in our Git repo called .gitignore can be used in order to add filetypes
that we don't want git to follow. We can do this using regular expressions, for example, that can also be understand by `ls` command.

Let's soupose that we have a .jpg file we don't want Git to follow. So we'll be using regular expressions to create .gitignore file 
and be sure Git won't be seeing those kind of files anymore, even if those files are, in fact, in our Git repo but not being staged:

```
echo "*.jpg" > .gitignore
```

After that Git won't show a .jpg file without staging anymore. But first we should add and commit our new .gitignore file in order to git start using it:

```
git add .gitignore
git commit -m "added gitignore file"
```
After that we can be sure any other jpg file won't be detected by Git.

`ls` command will show us if it is working.

## SUMMARY

- `git help` allow us read Git man pages.
- `git log` show us commit history.
- `git diff` show differences between last commit and recent changes not being staged yet.
- We can create a `.gitignore` file to add files we don't want to be detected by Git. 

## Branching, part 1

Branching is one of the most powerfull Git features. We can see branches at the moment by the `git branch` command.
We'll see the branch we are in marked with a (*) sign.
There is always a default branch in a Git repo, wich is named master. This is usually used as the "stable" version of code or whatever we are working in.
We can then develop new implementations in other branches that need kind of testing.

To add a new branch to our repo we should use `git branch [branch name]`
After that if we type again `git branch`, we'll see two branches instead of one.
`git status` also show us the branch we are in at the moment.

To erase a branch we can do it easily by typing `git branch -d [branch name]` command.
To change between branches, we use the `git checkout [branch name]` command.

If we want to create a new branch and at the same time change to it, we can do with `git checkout -b [branch name]` command.

It is important to note that when we create a new branch all files in master are also by default in the new branch, but if we do changes to a file in 
the new one this will not affect the same file in the master branch, even if we have added and commited new changes.

## Branching, part 2

The branching main idea is to be able to do "incremental changes" to plain text files ( usually code ), without affecting the master branch
or any other.

If we have made some changes to a file in new branch we should combine them with the file in master branch in order to take our work one step further.
This process is called "merge". Merge allow us to ellegantly combine changes between 2 different branches.

To do so, first we should change to master branch in order to implement changes. Git will automatically generate a new name "base branch" within the process of merging.
```
git checkout master
git merge [file name]
```

We can check changes with `cat [file name]` for example.

It is possible that we have conflict between 2 branches, because we have different commit for a new line or new "addition" to our file in two different branches.
In such situation if we try to do merge between files from those different branches we will get a "clonfict" message from Git.
To solve this, first we can do is type `git status` in order to figure out what is happening. We'll be prompted to solve the conflicts between additions and do commit again.
If we now use `cat [file name]`, cat will show us very usefull info:
```
<<<<<<<<<<<<<<<HEAD BRANCH

new line in master/base branch file
===================================
new line in update branch file

>>>>>>>>>>>>>>>UPDATE BRANCH
```

So in order to solve the conflict the best thing is erase the addition in the branch we are (master/base), and leave the new in develop branch file.
After that, with:
```
git add -A
git commit -m "solved conflict"
```
We are completing the merge manually, so we don't have to go back to state before `git merge [filename]` command.

There is an opensource book called GitPro to go deeper in the use of git.

## SUMMARY

- Git branching allow us to work with others in the same code base.
- To create a new branch we use `git branch [branch name]`.
- To change between branches we use `git checkout [branch name]`.
- We combine branches and file content using `git mege [branch name]`.

## Entry 3 Wednesday 23 June 2021

# GitHub

Now that we know Git basics we can start see how GitHub works. First we login in the web site with credentials established
at the beginning of week 4 topics. We should see a + sign on top right side. By click on it we are prompted to create a new repo.
After that we should be in a new page with new repo's info. That will be a Git remote repository so I think is usefull
call it the same name than our local repo, or `remote [local repo name]`

With the command `git remote` we can see wich remote GitHub repo is linked to our local repo.

This won't work at the moment because we haven't linked our new GitHub repo yet. To do so, we should copy the url of GitHub repo
we have just created, and then use a command to assign by default such repo to our local repo:

`git remote add [GitHub repo name] [url]`

After that if we type `git remote` again, we'll see our new GitHub repo set as remote. Ok!

When doing changes in our local files with their adds and commits, we should now update also our remote repository in order to 
both remain equal. For the first time doing so, we should use the command `git push -u [GitHub repo name] [branch]`.
The `-u` flag sets that remote repo as default repo, so next time we push changes to GitHub won't be necessary to specify any name or 
branch. Before push we`ll be asked for our GitHub user and password. Now we can see changes are well done in the web.

One interesting GitHub feature is representation of readme files, wich allow us to use markdown (.md) language for example.

## Markdown




