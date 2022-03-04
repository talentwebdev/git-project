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