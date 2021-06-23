## Git Exercises

1. Start a Git repo in a new directory and create a file in that directory.

- we should do this by:
```
git init
touch file_1.txt
```

2. Be sure Git is staging the file and create a commit.

- so we do:
```
git add file_1.txt
git commit -m "added file1"
```
3. Make changes to the file, then commit to these changes.

- modify file_1.txt:

`nano file_1.txt`, then we add a line or two. When this is done:

```
git add file_1.txt
git commit -m "added changes to file_1.txt"
```
4. Add 2 files to repository, but only commit to one of them

first we create the files, then only add one before commit:
```
touch file_{2..3}.txt
git add file_2.txt
git commit -m "added file_2.txt"
```
5. What is the status of repository at this point? Undo last commit, add the 2 files and then do commit again.

- we use `git status` to see the state of repo. Then we have to recall the state as it was before the last changes, so we do:
```
git reset --soft HEAD~
git add -A
git commit -m "added files 1 and 2.txt"
```

## Git features exercises

1. Look at the man page for git log and git diff

Well as we read through `git help diff/log` pages, it is shown to us many 
options in wich we can use this commands, much more than I am able to use at the moment.

2. Add a file type to our .gitignore file and add and commit it to be functional.

I did this following the instructions for the topic in course, but for .pdf files:
```
echo "*.pdf" > .gitignore
git add .gitignore
git commit -m "added pdf to .gitignore"
```
3. Create a file that contains the `git log` command output for the repository.
   Use egrep to see in what day of the week more changes happened.

I did this by the command `$( echo "git log" ) > git_log.txt` to create the file.
Then I did `cat git_log.txt` and was clear wich was the important day, because there were not many commits. I should use egrep with day of the week names I soupose, but I didn't.

 
## Branching exercises

1. Make a new branch

This should be made with `git branch [branch name]`

2. Change to new branch and do some commits in it. Change again to master branch and do merge.

Ok I made a new branch named update_log to update git_log.txt. I did it by `git branch Update-log`.
Then I did: 
```
git checkout Update-log 
$( echo "git log" ) > git_log.txt
git checkout master
git merge git_log.txt
```
To check changes I did `cat git_log.txt`

3. Create a conflict between branches and solve it.

To create the conflict simply update the same file in different branches with different content and add and commit them in each branch.
Then in the branch in wich I wanted do merge message of conflict arised.
At this point `git status` and `cat [filename]` are usefull to see what is happening.
Then proceeding as in topic notes is easy, just leaving changes in update version and erasing modifications in master. 
Then we can commit as conflit solved and complete merge manually, so to speak.

