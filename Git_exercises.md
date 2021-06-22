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
