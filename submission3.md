# Task 1: Understanding Version Control Systems

## Find commit hashes
``` sh
git log
```

### Output
``` sh
commit 5a66281a1302842549486e6ad6cfb133b7abee8f (HEAD -> lab3)
Author: Liana <mlr04@bk.ru>
Date:   Tue Sep 10 23:25:07 2024 +0300

    Commit 3 to inspect git

commit 66a754f75d3fcdab1a214ecf75486cc021b7d6ed
Author: Liana <mlr04@bk.ru>
Date:   Tue Sep 10 23:24:53 2024 +0300

    Commit 2 to inspect git

commit cf4880502ca0666fb05a621d1a56d48302213c36
Author: Liana <mlr04@bk.ru>
Date:   Tue Sep 10 23:24:38 2024 +0300

    Commit to inspect git
...
```

## Inspecting Commit
``` sh
git cat-file -p 5a66281a1302842549486e6ad6cfb133b7abee8f
```

### Output
``` sh
tree 06eddbfd10fe5f17d8faf0e6b7446af0832b1e08
parent 66a754f75d3fcdab1a214ecf75486cc021b7d6ed
author Liana <mlr04@bk.ru> 1725999907 +0300
committer Liana <mlr04@bk.ru> 1725999907 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgcrAQRpfBSJdjg4jukhMNtt7d6B
 4ZMm0bwtvUM+dN+AIAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQFi4Oxp2QFard5BYQxl/ccrUqME5/MzjisB9QDZJaOIrtAqpt1UvVyq7+Hjq2nApAn
 cOKHNCT5eLaPEUBhsj6QE=
 -----END SSH SIGNATURE-----

Commit 3 to inspect git
```



## Inspecting Tree
``` sh
git cat-file -p 06eddbfd10fe5f17d8faf0e6b7446af0832b1e08
``` 

### Output 
``` sh
100644 blob ede183da8ef201e5f5737eea502edc77fd8a9bdc    README.md
100644 blob 01f9a2aac3e315c5caa00db4019f1d934171dba0    file.txt
100644 blob cad401cc540a745e6b5133d4ac4b5d303529a3de    file2.txt
100644 blob 8bb2e871e94c486a867f5cfcbc6f30d004f6a9e5    file3.txt
100644 blob 5738bc15a0416ad2624df13badfb235052777e79    index.html
100644 blob 7a94f7af59b8968be392288ea03179a24ffc9d9e    lab1.md
100644 blob 1b99cc0044f93f556a0f6a599c7edf2f33f4944a    lab2.md
``` 

## Inspecting Blob

``` sh
git cat-file -p 8bb2e871e94c486a867f5cfcbc6f30d004f6a9e5
``` 

### Output 

``` sh
commit3
```

# Task 2: Practice with Git Reset Command

## Created and switched to `git-reset-practice` branch

```sh
git checkout -b git-reset-practice
```

## Create a series of commits

```sh
echo "First commit" > file.txt
git add file.txt
git commit -m "First commit"

echo "Second commit" >> file.txt
git add file.txt
git commit -m "Second commit"

echo "Third commit" >> file.txt
git add file.txt
git commit -m "Third commit"
```

## Reset Commands

Moves HEAD pointer by one commit back => keeps the changes staged

```sh
git reset --soft HEAD~1
```

file.txt
```
First commit
Second commit
Third commit
```

Moves HEAD pointer by one commit back => removes all changes 

```sh
git reset --hard HEAD~1
```

file.txt
``` 
First commit
```

## Recover commits with reflog

### Find reflog hash

Prints information about pointer changes in repository, including information about commits, branch switching, and other operations

```sh
git reflog
```

### Output
```
380daa3 (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
73d4959 HEAD@{1}: reset: moving to HEAD~1
d2b4855 HEAD@{2}: commit: Third commit
73d4959 HEAD@{3}: commit: Second commit
380daa3 (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
61404c0 (origin/master, origin/HEAD, master) HEAD@{5}: checkout: moving from master to git-reset-practice
61404c0 (origin/master, origin/HEAD, master) HEAD@{6}: checkout: moving from lab3 to master
4b2b188 (lab3) HEAD@{7}: commit: Added outputs of git commands
5a66281 HEAD@{8}: checkout: moving from master to lab3
61404c0 (origin/master, origin/HEAD, master) HEAD@{9}: checkout: moving from lab3 to master
5a66281 HEAD@{10}: checkout: moving from lab3 to lab3
5a66281 HEAD@{11}: commit: Commit 3 to inspect git
66a754f HEAD@{12}: commit: Commit 2 to inspect git
cf48805 HEAD@{13}: commit: Commit to inspect git
61404c0 (origin/master, origin/HEAD, master) HEAD@{14}: checkout: moving from master to lab3
61404c0 (origin/master, origin/HEAD, master) HEAD@{15}: clone: from github.com:liaaana/F24-intro-labs.git
```

### Recover

Restores the repository to needed state (d2b4855 HEAD@{2}: commit: Third commit).

```sh
git reset --hard d2b4855
```


