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

Switch remote to SSH from HTTPS to allow git push

> git remote set-url git@github.com:username/public-repo.git

Using server to ssh private repositories

> set up ssh and pubkey with git
> ssh -T git@github.com
> git clone git@github.com:justindpk/frenpet-analytica.git

