---
layout: post
title: How to delete files correctly?
date: 2023-10-28
comments: true
---

This is an old post that I wrote a few years ago, and I think I stole some of it from someone else on the Internet, if you happen to find this post, please reach out to me so I can delete it or credit you properly.


## Overview

This is a tutorial on using the command line to delete files in your computer, in the right way. 

## what will happen when you use **rm** to delete large amount of files

I had this problem back in 2019, when I was running a web crawler from PubMeb, what I was doing was crawing the abstracts of all the medical literatures from PubMED, this ended up with 27 million small files, each less than 100KB in one single directory by mistake. 
and when I want to delete them all, the **rm** command does not work properly, it takes way too much time to finish, so what's wrong about it? the problem is that rm command is invoked for each and every file in the list. For example, if there are 50 files in the folder which are bigger than 7M, then 50 rm commands are invoked for deleting each of them. This will take a much longer time.

So are there any other method to solve this?

## Find Command with -exec

example:
```shell
find /test -type f -exec rm {}
```

The above shown command, will delete all the files inside /test directory. First the find command will look for all files inside the directory, and then for each result, it will execute and rm

essentially this command is not different from rm command, however,in practice, this would be a little faster than the raw rm command. it tooks around 14 Minute for half a million files, depending on your individual file size.

## Find Command with -delete

example:
```shell
find ./ -type f -delete
```

this command is actually much faster than the above command. it tooks around 5 Minute for half a million files, depending on your individual file size.

## Perl

example:
```shell
perl -e 'for(<*>){((stat)[9]<(unlink))}'
```

this is actually the fatstest option. it tooks around 1 Minute for half a million files, depending on your individual file size.

But yeah if you are interested in deleting files using Perl, you need to have some good hands on with Perl regular expressions.

There is one more lesser used and less known method that can be used to delete large number of files inside a folder. This method is none other than our famous tool RSYNC used for transferring and synchronizing files between two local as well as remote locations in Linux




## RSYNC with -delete

This can be achieved by simply synchronizing a target directory which has the large number of files, with an empty directory. In our case test directory has half a million files, lets create a directory called as blanktest, which will be kept empty for the purpose of simply synchronization. Now along with this we will be using -delete option in rsync, which will delete all those files in the target directory, which are are not present in the source

example:

Empty Directory: /home/blanktest

Directory to be emptied: /test 
```shell
rsync -a --delete blanktest/ test/
```

this command tooks around 2 minutes to delete all files. Cool!

## One last note

Linux and other operating systems have some limits in their file systems, it is not a good idea to put too many files in one single directory, if you want to store large amount of files, a good idea would be store these files subdirectories and the ideal amount of files in one single subdirecotries is less than 10000. 



