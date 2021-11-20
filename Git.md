[<- Home](README.md)

# Git
Rebase the N last commits of branch A on branch B : `git rebase --onto B A~N A` or `git rebase --onto B HEAD~N` if HEAD is on latest commit of branch A.

In case of empty file error "object file ... is empty" and "fatal: loose object ... is corrupt" :
```
find .git/objects/ -type f -empty | xargs rm
git fetch -p
git fsck --full
```