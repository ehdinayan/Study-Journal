# WEEK 4 

## Entry 1 Tuesday June 15 2021

## What are Git and GitHub?

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

# Entry 2 Tuesday June 22 2021

## SUMMARY

- Git follows changes to plain text files ( code, text ).
- A directory in wich changes are staged by Git is called a Git repo.
- To stablish a new Git repo we should type `git init` in desired directory.
- Changes to filles are followed by `git add [filename]` command.
- We create milestones of our files state with command `git commit -m "comment about changes"`
- To see the state of files in directory we use `git status` command.
- We can see a list of commits of repo by typing `git log`.

# WEEK 4 Important Git features

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




