---
layout: post
title: Commonly used Unix commands
date: 2023-10-28
comments: true
---

Here are some commands that I commonly use for unix system terminals. 


### Files and directories

1. **cd dirname** --- go to a specific directory.
    1. **.** is current directory
    2. **..** is the parent directory, for example, **cd ..** means go to the parent directory of where I am currently at.

2. **pwd** --- tells you where you currently are, this returns the absolute path.
3. **ls** --- Listing files in current directory
    1. **ls -a** --- listing all files including hidden files, many files are by default hidden such as .gitignore file in a git repo.

4. **mv filename1 filename2** -- moves a file, rename it or move it to a different directory.
5. **cp filename1 filename2** --- copies a file.
6. **mkdir dirname** --- creates a new directory in current directory
7. **rm filename** --- delete a file.
    1. **rm -r dirname** --- recursively delete everything in a directory


### Connect to remote computer and files uploading
1. **ssh username@remote-computer-ip-address** --- connect to a remote computer
2. **scp filename username@remote-computer-ip-address:/target/directory** --- upload a file from local computer to remote computer
3. **rsync** --- recommended way of sync two directories, the two directories can be local or remote. see [here](https://linux.die.net/man/1/rsync) for more details. This can used to delete files in a local directory (create an empty dir and then sync the target dir to it) or upload files from local dir to remote dir. Empirically this command is very fast.


### Other commands

1. **top** --- display all active process
2. **kill pid** --- kill a specific process say you want to terminate a program because it took forever to run.
3. **whoami** --- show current username
4. **du filename** --- shows the disk usage of the files
5. **quota -v** --- show what your disk quota is (i.e. how much space you have to store files)
6. **grep string filename(s)** --- looks for the string in the files.
7. **df** --- check drive space
    1. **df -h** return size in human readable format, i.e. in GB or MB etc.

### Git related

1. **git add** --- stage changes in your code
2. **git commit -m "some commit message"** --- commit changes to your code
3. **git push origin branch-name** --- push changes to remote repo
4. **git clone repo-link** --- clone remote repo to local 
5. **git checkout -b branch-name** --- checkout to a specific branch, if no such branch exists, this will create a new branch.
6. **git fetch** --- fetch updates from remote repo
7. **git rebase origin/main** --- rebase against main branch. see [here](https://docs.gitlab.com/ee/topics/git/git_rebase.html) for more details




