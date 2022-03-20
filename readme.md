https://www.youtube.com/watch?v=apGV9Kg7ics - alexander

## Git Diff command - https://www.youtube.com/watch?v=f8YUWe0De6Q - phoenix

**Req1: To see the difference in File Content between Working directory and staging area**

```gitbash 
git diff package.json
```

```
diff --git a/athena/templates/package.json b/athena/templates/package.json
index f32222579..7b2215c76 100644
--- a/athena/templates/package.json
+++ b/athena/templates/package.json
@@ -76,6 +76,7 @@
     "react-chartjs-2": "^2.9.0",
     "react-loading-skeleton": "^3.0.1",
     "react-router-dom": "^5.2.1",
+    "react-tooltip": "^4.2.21",
     "regenerator-runtime": "^0.13.9",
     "sortablejs": "1.10.0-rc3",
     "sweetalert2": "^9.17.1",
```

a/athena/templates/package.json     --> represents source(staging area) 
b/athena/templates/package.json     --> represents dest(working directory)

f32222579   --> Hash of file content from source/staging 
7b2215c76   --> Hash of file content from destination/working dir

100644      --> git file mode
                100 -- represents type of the file
                644 - File permission rw-r-r
                    4 - r
                    2 - w
                    1 - e


--- a/athena/templates/package.json Source file missing some lines (staging)
+++ b/athena/templates/package.json New lines added in destination file(working dir)


        if anyline prefixed with space means it is unchagned, 
        if anyline prefixed with + means it is added in destination copy 
        if anyline prefixed with - means it is removed from destination copy


**Req2: To see the difference in File content between working directory and Last commit**

* Last commit refered using HEAD
```
git diff HEAD names.txt
```

**Req3: To see the difference in File Content between staged copy and last commit**
```
git diff --staged HEAD names.txt
```

**Req4; To see the difference in File content between specific commit and working directory copy**

To see git ids 
```
git log --oneline
```
```
git diff 27c49c6 names.txt
```


## How to remove commit in git history? 
```
git reset [commit-id]
```

## How to merge commit together?
- You can reset to the pevious commit of the commits that you're going to merge. 

```
commit 9ce8a4492534edfaaa11405f47d6d1e7e58c5fe7 (HEAD -> new-branch)
Author: TalentWebDev <49565243+talentwebdev@users.noreply.github.com>
Date:   Sat Mar 5 05:04:09 2022 +0800

3

commit 7eb4bba38404b85127e0c175b97dc603e97bd59d
Author: TalentWebDev <49565243+talentwebdev@users.noreply.github.com>
Date:   Sat Mar 5 05:00:33 2022 +0800

1

commit 7ecf146bae5ff4a11cc53d98c01d659a7bca16e9 (origin/new-branch, origin/master, temp, master)
Author: TalentWebDev <49565243+talentwebdev@users.noreply.github.com>
Date:   Sat Mar 5 04:53:54 2022 +0800

rename readme.md

commit e1fd70a2a4385ec9546159a0ce7312b0b4d0e6d5
Author: TalentWebDev <49565243+talentwebdev@users.noreply.github.com>
Date:   Mon Jan 24 16:54:03 2022 +0800

first commit file contains 1 line

commit 27c49c618ca8e170fd3918957a5cfac695d920f7
Author: talentwebdev <zhuping.man@outlook.com>
Date:   Fri Jan 14 14:02:09 2022 +0800

adding names.txt file
```
In the above case, if you reset commit to `7ecf146bae5ff4a11cc53d98c01d659a7bca16e9`, the later changes/commits will be staged. 
Then, you can creat a new commit from there.
```
git reset 7ecf146bae5ff4a11cc53d98c01d659a7bca16e9
git add ./ 
git commit -m "new commit" 
```

- You can also use rebase and squashing commits.
There are two types here: pick / squash
Pick represents the separate commit. 
Squash reprseents merging into one commit. 

```
git rebase -i 7ecf146bae5ff4a11cc53d98c01d659a7bca16e9
```
Then, you'll see something like this:
```
pick 7eb4bba 1
pick 9ce8a44 3
pick f21e7fe 2
```
You can squashing by changing pick to s.
```
pick 7eb4bba 1
s 9ce8a44 3
s f21e7fe 2
```

## Git Rebase vs Merge

[Docs](https://git-scm.com/docs/git-rebase)

Let's assume that there are 3 commits in master branch(m1, m2, m3). And we create feature branch based on m2(master). 
Then, we added f1 and f2 in feature branch. So the history will be (m1, m2, f1, f2) in feature branch. 

In master branch and run this command

```
git merge feature
```

It'll create merge commit by merging master and feature. 

```
git merge --squash feature
```

This will merge f1 and f2 into one and not create a commit. But changes will be brought in. 

In feature branch, if we do git rebase, it'll compare the latest commits and brought them as base commit. 

E.g. 
the history will be m1, m2, m3, f1, f2 

when you run in feature branch
```
git rebase master
```
