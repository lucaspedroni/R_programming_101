R nuts and bolts: Workspace & Files
========================================================
author:
date:
autosize: true

Workspace & Files
========================================================

R provides a common set of commands for interacting with files

- managing the working directory
- managing objects in the local workspace
- managing files in the working directory

The Working Directory
========================================================

The __Working Directory__ is where R finds all of its files for reading and for writing on your computer. R provides some simple commands to manage the __working directory__:


```r
#Find the current working directory
getwd()
[1] "E:/APPL/workspace_r/R_programming_for_dummies"
```



```r
#Change the working directory to a new dir
setwd(...)
```

Managing objects in the workspace
========================================================


```r
#View all the objects in your local workspace
ls()
```


```r
#Remove objects from your local workspace
rm()

#example 1
## tmp <- 1
## ls()
## rm(tmp)

#example 2
## tmp1 <- 1
## tmp2 <- 1
## ls()
## rm(list = c("tmp1", "tmp2")
```

Managing files in the working directory
========================================================


```r
#View all dirs in your working directory (including hidden dirs)
list.dirs()

#Create a directory in the working directory
dir.create()
```


```r
#View all files/ dir in your working directory
list.files()

#Create/ Rename/ Copy/ Remove a file in the working directory
file.create(), file.rename(), file.copy(), file.remove()

file.exists() #Check if a file exists

file.info() #Info about a file

file.path() #Build a path OS agnostic
```

Hands-On (15 minutes)
========================================================


```r
library(swirl)
swirl()
#.....
# Select the "R Programming" entry
# Select the "Workspace and Files" entry [2]

# Enjoy :)
```