---
layout: post
title:  "Pushing Multiple Git Repos"
date:   2019-10-18 11:16:19 -0700
categories: git
---

I am currently TAing the class [AM 129: Foundations of Scientific Computing](https://people.ucsc.edu/~dlee79/2019/fall/am129_209/index.html) and I need to grade code located in the student's git repo. Thus I came up with this script to add, commit, and push the students' grade all at once. This has saved me plenty of time!

```shell
# Asks to enter a commit message
# in my situation its usually something like "homework x grade"
echo 'Enter the commit message:';
read commitMessage;

# This loop finds directories/git repos in the current directory
for d in */ ; do

    # Then changes directory the git repo and adds, commits, and pushes, then changes back to top directory
    cd ./$d
    git pull
    git add -A
    git commit -m "$commitMessage"
    git push
    cd ../
    
done
```

This can be easily modified if you have a specific branch that this needs to be pushed to. You would need to add 
```shell
    echo Enter branch name:
    read branchName
```
to after the commit message prompt. Then modify the `git push` to `git push origin $branchName`.
