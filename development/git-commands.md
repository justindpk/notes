# Basics

## Branch management

Clone repository

> git clone -b my-branch git@github.com:user/myproject.git

Delete local branch

> git branch -d localBranchName

Delete remote branch

> git push origin --delete remoteBranchName

Rebase a branch to main

> git branch - m branchToRebase main
> git fetch origin
> git branch -u origin/main main
> git remote set-head origin -a
