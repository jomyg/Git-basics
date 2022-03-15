# Git-basics



### Git Basics

#### Hash function and checksum value:
----
We can check the file content is same or different on source and destination if we copy the file. This can be test using the checksum
Hash function: It will return a fixed length string.

eg: Using the sha1sum
~]# echo "i am jomy" > linux.txt
~]# sha1sum linux.txt
fe5279dd65cab86e06a23fa29ed26db2109c2798  linux.txt            >>>>>>>>> The content is same so the checksum value is same. It giving a string value. 
 ~]# echo "i am jomy" > bsd.txt
~]# sha1sum bsd.txt
fe5279dd65cab86e06a23fa29ed26db2109c2798  bsd.txt
~]# echo "i am jomy george" > bsdsum.txt        >>>>>> Content is differnet so the checksum value is different. 
# sha1sum bsdsum.txt
1184da4cc1b28945b9aca8f5d839a60f05b98e1b  bsdsum.txt

]# md5sum bsdsum.txt
fe04bd912292a3b43c8dd55595e7dbef  bsdsum.txt
# md5sum linux.txt
5103dca041d81f5967e9a62e8b85ee18  linux.txt

We can check all the file checksum value using appropriate algoirthms eg: md5sum and sha1sum. This way we can download a ISO file and can be verify using 
their provided checksum value. We can use sha256 algorithm to check. If the value is different on checksum then the downloaded file is different.

### What is GIT ?

Git is like "cp" command. There are three important main points,

- working Directory
- local repository
- objects

Git is a DevOps tool used for source code management. It is a free and open-source version control system used to handle small to very large projects efficiently. 
Git is used to tracking changes in the source code, enabling multiple developers to work together on non-linear development. Linus Torvalds created Git in 2005 for 
the development of the Linux kernel.

What is the difference between the working directory (aka workspace) and the repository?
-The repository is essentially the .git hidden folder inside the working directory (workspace).The working directory (workspace) is essentially your project folder.
Also note the term directory is basically synonymous to the term folder.

- working Directory:
The project files which resided through git on a directory called working Directory. We can create multiple working dir for diff projects.

- The local repository  >>>>>>> .git
The local repository is a Git repository that is stored on your local computer ".git" . The remote repository is a Git repository that is stored on some remote computer.

- Objects
Objects folder is a very important folder in the . git directory. In Git, everything is saved in the objects folder as a hash value. 
By everything I mean every commit, every tree or every file that you create is saved in this directory.

================================================================================================================================================

Git init:
The git init command creates a new Git repository. It can be used to convert an existing, unversioned project to a Git repository or initialize a new, 
empty repository. Most other Git commands are not available outside of an initialized repository, so this is usually the first command you'll run in a new project.

Git ADD:
The git add command adds a change in the working directory to the staging area. 
It tells Git that you want to include updates to a particular file in the next commit.

We can test this now on our system.

[root@ip-172-31-9-154 mydir]# git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in /root/mydir/.git/

[root@ip-172-31-9-154 mydir]# ls -al
total 0
drwxr-xr-x 3 root root  18 Mar 15 10:20 .
dr-xr-x--- 4 root root 166 Mar 15 10:16 ..
drwxr-xr-x 7 root root 119 Mar 15 10:20 .git
[root@ip-172-31-9-154 mydir]#
[root@ip-172-31-9-154 mydir]# tree .git
.git
├── branches
├── config
├── description
├── HEAD
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-merge-commit.sample
│   ├── prepare-commit-msg.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── push-to-checkout.sample
│   └── update.sample
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

9 directories, 17 files
[root@ip-172-31-9-154 mydir]# rm -rf .git/hooks/*
[root@ip-172-31-9-154 mydir]# tree .git
.git
├── branches
├── config
├── description
├── HEAD
├── hooks
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

9 directories, 4 files
================================================================================================================================================
### Now we can configure the git using config command:

[root@ip-172-31-9-154 mydir]# git config user.name "jomy"
[root@ip-172-31-9-154 mydir]# git config user.email "jomy1@gmail.com"
[root@ip-172-31-9-154 mydir]# cat .git/config
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[user]
        name = jomy
        email = jomy1@gmail.com     >>>>>>>>>>>>>>>>>>>>>>>>>>>>> There you go
        
[root@ip-172-31-9-154 mydir]# echo "i am jomy" > linux.txt
[root@ip-172-31-9-154 mydir]# ls -al
total 4
drwxr-xr-x 3 root root  35 Mar 15 10:23 .
dr-xr-x--- 4 root root 166 Mar 15 10:16 ..
drwxr-xr-x 7 root root 119 Mar 15 10:20 .git
-rw-r--r-- 1 root root  10 Mar 15 10:23 linux.txt

### mydir]# git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        linux.txt

nothing added to commit but untracked files present (use "git add" to track) "The track means build"

>> The git status command displays the state of the working directory and the staging area. It lets you see which changes have been staged, 
which haven't, and which files aren't being tracked by Git.
From above, this is will print the Untracked files and which means there is no contents of linux.txt in .git DIR.

### .git content before add
[root@ip-172-31-9-154 mydir]# tree .git/
.git/
├── branches
├── config
├── description
├── HEAD
├── hooks
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

9 directories, 4 files
#### We can now add the linux.txt to git. So the untracked disappered and an object is created under the local repository ".git"
[root@ip-172-31-9-154 mydir]# git add linux.txt
[root@ip-172-31-9-154 mydir]# git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   linux.txt
================================================================================================================================================

sha1sum linux.txt        >>> Checksum value of the file which we created
dec17802ef81e76f897e0480b9da459342008e41  linux.txt

GIT is identify the contents by its checksum value and no filename as above.
An object is subdir under the .git

Index file or staging file under .git. Under the index file it will write that the linux.txt and its checksum value not the the file content.
This occur when we "git add". Content is under the .git dir.

[root@ip-172-31-9-154 mydir]# tree .git/
.git/
├── branches
├── config
├── description
├── HEAD
├── hooks
├── index                                            >>>>>>>>>>> This is the index file,
├── info
│   └── exclude
├── objects
│   ├── c0
│   │   └── 45531a2973dd9ee03933a502153ee3e944aae6       >>>>>>> This is the object we have added by linux.txt
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

10 directories, 6 files

================================================================================================================================================

Now we can add some files to test.

root@ip-172-31-9-154 mydir]# echo "i am jomy bsd" > bsd.txt
[root@ip-172-31-9-154 mydir]# echo "i am jomy wind" > windows.txt
[root@ip-172-31-9-154 mydir]# echo "i am jomy" > bsdtest.txt >>>>>>>... Same content of linux.txt so that the checksume is same so dont need to create another object
So it will add the bsdtest.txt under index file not under the object. If new content it will create a object and add to index.file.

[root@ip-172-31-9-154 mydir]# sha1sum linux.txt
dec17802ef81e76f897e0480b9da459342008e41  linux.txt
[root@ip-172-31-9-154 mydir]# sha1sum bsdtest.txt
dec17802ef81e76f897e0480b9da459342008e41  bsdtest.txt

[root@ip-172-31-9-154 mydir]# tree .git/
.git/
├── branches
├── config
├── description
├── HEAD
├── hooks
├── index
├── info
│   └── exclude
├── objects
│   ├── 5a
│   │   └── 03b5aea50a8ba3ea7ff04045bf981ad2dc54f7
│   ├── c0
│   │   └── 45531a2973dd9ee03933a502153ee3e944aae6
│   ├── cc
│   │   └── b228de5712364b0bb206c7df9ddab84df67355
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

12 directories, 8 files
================================================================================================================================================

We can display the index file of git using command: "git ls-files -s" under working dir.

[root@ip-172-31-9-154 mydir]# git ls-files -s
100644 c045531a2973dd9ee03933a502153ee3e944aae6 0       bsd.txt             Same object
100644 c045531a2973dd9ee03933a502153ee3e944aae6 0       bsdtest.txt         Same object
100644 c045531a2973dd9ee03933a502153ee3e944aae6 0       linux.txt           Same object
100644 ccb228de5712364b0bb206c7df9ddab84df67355 0       windows.txt         diff object

[root@ip-172-31-9-154 mydir]# tree .git/
.git/
├── branches
├── config
├── description
├── HEAD
├── hooks
├── index
├── info
│   └── exclude
├── objects
│   ├── 5a
│   │   └── 03b5aea50a8ba3ea7ff04045bf981ad2dc54f7
│   ├── c0
│   │   └── 45531a2973dd9ee03933a502153ee3e944aae6
│   ├── cc
│   │   └── b228de5712364b0bb206c7df9ddab84df67355
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

12 directories, 8 files

#### If we change the content of bsd.txt

[root@ip-172-31-9-154 mydir]# echo "i am jomy george" > bsd.txt
[root@ip-172-31-9-154 mydir]# git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   bsd.txt
        new file:   bsdtest.txt
        new file:   linux.txt
        new file:   windows.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   bsd.txt                                                  >>>>>>>>>>.. SHowing as modified now
        
[root@ip-172-31-9-154 mydir]# git add .
[root@ip-172-31-9-154 mydir]# tree .git/
.git/
├── branches
├── config
├── description
├── HEAD
├── hooks
├── index
├── info
│   └── exclude
├── objects
│   ├── 0e
│   │   └── d6884c7a336a3afa1b0f73d7cee9a315701e41                 >>>>>>>>>>>>> New object is created as its new
│   ├── 5a
│   │   └── 03b5aea50a8ba3ea7ff04045bf981ad2dc54f7
│   ├── c0
│   │   └── 45531a2973dd9ee03933a502153ee3e944aae6
│   ├── cc
│   │   └── b228de5712364b0bb206c7df9ddab84df67355
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

13 directories, 9 files

[root@ip-172-31-9-154 mydir]#  git ls-files -s
100644 0ed6884c7a336a3afa1b0f73d7cee9a315701e41 0       bsd.txt
100644 c045531a2973dd9ee03933a502153ee3e944aae6 0       bsdtest.txt
100644 c045531a2973dd9ee03933a502153ee3e944aae6 0       linux.txt
100644 ccb228de5712364b0bb206c7df9ddab84df67355 0       windows.txt

[root@ip-172-31-9-154 mydir]# echo "i am jomy george centos " > bsd.txt
[root@ip-172-31-9-154 mydir]# git add .
[root@ip-172-31-9-154 mydir]# tree .git/
.git/
├── branches
├── config
├── description
├── HEAD
├── hooks
├── index
├── info
│   └── exclude
├── objects
│   ├── 0c
│   │   └── e5c6dd82ac91fe7d9041d04af681bb6816c466
│   ├── 0e
│   │   └── d6884c7a336a3afa1b0f73d7cee9a315701e41
│   ├── 5a
│   │   └── 03b5aea50a8ba3ea7ff04045bf981ad2dc54f7
│   ├── c0
│   │   └── 45531a2973dd9ee03933a502153ee3e944aae6
│   ├── cc
│   │   └── b228de5712364b0bb206c7df9ddab84df67355
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

: Old object will delete automatically from git. We can revoke on the above process.


### What is Commit ?
================================================================================================================================================

[root@ip-172-31-9-154 mydir]# git commit -m "commit 1"
[master (root-commit) 5414c7d] commit 1
 4 files changed, 4 insertions(+)
 create mode 100644 bsd.txt
 create mode 100644 bsdtest.txt
 create mode 100644 linux.txt
 create mode 100644 windows.txt
[root@ip-172-31-9-154 mydir]# git log
commit 5414c7d957159777b122e274c4a0ce2086b904ce (HEAD -> master)        >>> Commit object with checksum value
Author: jomy <jomy1@gmail.com>
Date:   Tue Mar 15 11:24:01 2022 +0000

    commit 1
[root@ip-172-31-9-154 mydir]#
When we run commit. it will create a copy of index file with all checksum.
Commit --> commit tree object -> copy of index file (commit tree file) --> commit object with ID.  Commit as a backup (object)
:
    

[root@ip-172-31-9-154 mydir]# tree .git/
.git/
├── branches
├── COMMIT_EDITMSG
├── config
├── description
├── HEAD
├── hooks
├── index
├── info
│   └── exclude
├── logs
│   ├── HEAD
│   └── refs
│       └── heads
│           └── master
├── objects
│   ├── 01
│   │   └── cf61d099c87b74008eb7d9a906681b1b5e3dd6
│   ├── 0c
│   │   └── e5c6dd82ac91fe7d9041d04af681bb6816c466
│   ├── 0e
│   │   └── d6884c7a336a3afa1b0f73d7cee9a315701e41
│   ├── 54
│   │   └── 14c7d957159777b122e274c4a0ce2086b904ce                >>>> This is the commit object "5414c7d957159777b122e274c4a0ce2086b904ce"
│   ├── 5a
│   │   └── 03b5aea50a8ba3ea7ff04045bf981ad2dc54f7
│   ├── c0
│   │   └── 45531a2973dd9ee03933a502153ee3e944aae6
│   ├── cc
│   │   └── b228de5712364b0bb206c7df9ddab84df67355
│   ├── info
│   └── pack
└── refs
    ├── heads
    │   └── master
    └── tags

[root@ip-172-31-9-154 mydir]# git cat-file -p 5414c7d957159777b122e274c4a0ce2086b904ce         >>> When we display the commit object
tree 01cf61d099c87b74008eb7d9a906681b1b5e3dd6          >>>>>>>> This is the copy of index file which created on run commit.
author jomy <jomy1@gmail.com> 1647343441 +0000
committer jomy <jomy1@gmail.com> 1647343441 +0000

commit 1

[root@ip-172-31-9-154 mydir]# git cat-file -p 01cf61d099c87b74008eb7d9a906681b1b5e3dd6    >>> COpy of index file and its content as a object
100644 blob 0ce5c6dd82ac91fe7d9041d04af681bb6816c466    bsd.txt
100644 blob c045531a2973dd9ee03933a502153ee3e944aae6    bsdtest.txt
100644 blob c045531a2973dd9ee03933a502153ee3e944aae6    linux.txt
100644 blob ccb228de5712364b0bb206c7df9ddab84df67355    windows.txt
[root@ip-172-31-9-154 mydir]# git cat-file -p c045531a2973dd9ee03933a502153ee3e944aae6   
i am jomy
[root@ip-172-31-9-154 mydir]#


#### Branch pointer : This will keep the object checksum value of commit. 
A branch in Git is simply a lightweight movable pointer to one of these commits. The default branch name in Git is master . 
As you start making commits, you're given a master branch that points to the last commit you made. 
Every time you commit, the master branch pointer moves forward automatically.

[root@ip-172-31-9-154 mydir]# git branch
* master                          >>>>>>>>>>>>>>>>>>>> Branch

[root@ip-172-31-9-154 mydir]#  tree .git
.git
├── branches
├── COMMIT_EDITMSG
├── config
├── description
├── HEAD
├── hooks
├── index
├── info
│   └── exclude
├── logs
│   ├── HEAD
│   └── refs
│       └── heads
│           └── master
├── objects
│   ├── 01
│   │   └── cf61d099c87b74008eb7d9a906681b1b5e3dd6
│   ├── 0c
│   │   └── e5c6dd82ac91fe7d9041d04af681bb6816c466
│   ├── 0e
│   │   └── d6884c7a336a3afa1b0f73d7cee9a315701e41
│   ├── 54
│   │   └── 14c7d957159777b122e274c4a0ce2086b904ce
│   ├── 5a
│   │   └── 03b5aea50a8ba3ea7ff04045bf981ad2dc54f7
│   ├── c0
│   │   └── 45531a2973dd9ee03933a502153ee3e944aae6
│   ├── cc
│   │   └── b228de5712364b0bb206c7df9ddab84df67355
│   ├── info
│   └── pack
└── refs
    ├── heads
    │   └── master              >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>> Branch point
    └── tags

19 directories, 16 files

[root@ip-172-31-9-154 mydir]# cat .git/refs/heads/master
5414c7d957159777b122e274c4a0ce2086b904ce                               >>> This is Commit id which we run last commit.
[root@ip-172-31-9-154 mydir]# git cat-file -p 5414c7d957159777b122e274c4a0ce2086b904ce
tree 01cf61d099c87b74008eb7d9a906681b1b5e3dd6
author jomy <jomy1@gmail.com> 1647343441 +0000
committer jomy <jomy1@gmail.com> 1647343441 +0000

commit 1  

#### WHat is head pointer
Keeping the branch pointer name as file called head pointer.

[root@ip-172-31-9-154 mydir]#  tree .git
.git
├── branches
├── COMMIT_EDITMSG
├── config
├── description
├── HEAD          >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>> Head pointer
├── hooks


[root@ip-172-31-9-154 mydir]# cat .git/HEAD
ref: refs/heads/master
