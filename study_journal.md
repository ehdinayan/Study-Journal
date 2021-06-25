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

## Entry 3 Wednesday June 23 2021

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

## Entry 4 Thursday June 24 2021

## Markdown

Markdown is a markup language wich allows us add decorative features to text files through a set of rules, just as other languages like HTML, XML
or LaTex. Markup is intuitive and powerfull and can be used as plain text. GitHub transforms markdown text files (.md extension) into simple HTML 
files. If we have a README.md file in our repo, GitHub will renderize it to HTML.
We can create and edit this file with nano.

This are the Markdown rules to write .md text files:
```
double star quotation (**) = bold

simple star quotation (*)  = cursive

comment with simple #      = big text (tittles)

comment with double ##     = average text (second tittles)

three ``` before and after 
 an entire pharagraph      = code format

simple ` quotation         = code format

middle hypen comment (-)   = dot (.)

number and dot comment 1.  = 1.

brackets quotation []+(url)= link

link preceeded by !        = image
```

In course there are links to guides and tools to mastering Markdown.

## Pull request

Forking and pull requests are what make GitHub great. Pull request allow us to compare 2 different branches before doing merge between them.
This way is easy to decide next course of action.

This feature aloow peopple collaborating in develop their projects, but we can use it individually to be organized.
Let's see how to open apull request in our repo. First we should change to our develop or update branch:

`git checkout [branch name]`  
`ls`

let's modify a README file for example, in order to have two different versions in the two branches and have a little Markdown practice.
When this is done, we should add and commit this changes in our develop branch, and push it to our GitHub remote repo:

`git push [remote repo name] [branch name]`

Git will tell us that a new branch has been created. This is normal since we haven't made any push from our develop branch to our remote repo.
So then we better check our GitHub site to to confirm we have now two branches with different README files.

Now that we have pushed and update our develop branch in GitHub, letś open a pull request.
It is similar to a Git Merge guided by GitHub. To do so, we should click on "new pull request button", wich is next to branch selection in GitHub. This
will take us to a page with important features, so we'll explain them.

Under the last commit there are names of base (master) and compare (develop) branches, this one is where changes had been done.
We can also give a name to our pull request action or leave for it the last commit name.
We can also write comments in text boxes about our pull request, if we are in a collaboration project it is important to explain well those changes.
If we continue scrolling down the page we'll see a usefull comparison between the two files wich has same name but different content, as well as a list of the rest of files contained in each branch.
So we click on green button "create pull request", and other important page will open.

Under our pull request name there are three tabs: Comments, where we can comment pull request in Markdown format if we wish.
Commits, where we can see commits to comparison branch for this pull request. Files changed show us a list of changes made to the 
file in a line by line basis. We now come back to the tab where the green button "merge pull request" is and click on it, 
then "confirm merge". This will do a merge of the compare branch into master (base) branch. Now if we click on the top left corner in the 
Code tab, we'll see the changes made to develop branch have been merged into master branch. We have made our first pull request!

Now the important point is update locally in our repo the changes that have been made remotelly through pull request in GitHub.
To do so, on our local repo we type `git pull`. With this command, Git finds master branch in remote repo and updates our local repo
with the new pull request commits. We have completed an entire pull request cycle!

## Entry 5 Friday June 25 2021 

## GitHub Pages

We can create and have a web host a website through GitHub using Git and Markdown.
In our GitHub session, we can click on **Settings** button on top right area and that take us to another page where we have considerable number of options to manage for our repository.
If scrolling down we'll see **Pages** option on the left. Click on it and then other page appears. We can select the branch and file we want to show as web page in this repository.
There are also other options like theme to choose and so, but we are only interested for now in simple Markdown .md files to show as website.

After do the selections, we press **save** button and that will show an url link where our site will be hosted. Next time we enter this option we can click that link in order to see how it looks. Quite a cool thing!
To modify the aspect, we should modify the .md file and commit and push the changes to our remote repo.

This is great for project descriptions, documentation, blogs, etc.

There's a link in the course to go deeper on GitHub Pages.

## Forking

When we do a **fork** of a repository we are copying that Git filesystem to our repo. This way we can modify this copy and save changes for personal use, to share them,
or to open a pull request to merge our changes with original file, wich is in what is known as **upstream repository**.

Once we have forked a repo, we should use `git clone` command in order to have a local copy while Git follows **upstream repo**.
In repository we have just forked there should be a button on top right area wich says **clone or download**. If we click on clone we'll see the url that has been forked, so we should copy it in order to use in our terminal. We go to our local Git repo and type:

`git clone [forked repo url]`

Now that we have clone our first repo, it is cool be sure that Git is following its **upstream repo**, so we can do that by typing:

`git remote -v`

We can now easily modify the file we were interested in, add, commit, push and to complete the **forking cycle**, a pull request to do merge with original file will be great.
We have gone through this by forking course repo, cloning it, add our name in the guestbook.md, add and commit this changes and do a pull request.

## SUMMARY

- GitHub creates and mantains remote repos.
- A Git remote repo is allways connected to the internet.
- We can see remote repos with `git remote` command. 
- We add a remote repo with `git remote add [repo name] [url]`.
- We add commits to our remote repo with `push` command if we have set a default remote repo with `-u` flag in `push` command.
- Pull Request allow us compare two branches before doing a **merge** between them.
- We can have a free website with GitHub and Markdown.
- Forking allow us to make changes in a public repository. Then we can try to do a pull request if consider will be great merge with original file in **upstream repo**.

