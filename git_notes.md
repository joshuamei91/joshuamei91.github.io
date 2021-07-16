---
layout: page
title: Git Notes
permalink: /git-notes/
---

## Common workflows
- Save changes to a new branch
```
git checkout -b <new_branch_name>
git add .
git commit -m "new feature"
```
- [Delete the last commit that was pushed to the remote](https://christoph.ruegg.name/blog/git-howto-revert-a-commit-already-pushed-to-a-remote-reposit.html)
```
# git interprets x^ as the parent of x and + as a forced non-fastforward push
git push <remote> +HEAD^:<branch>

# Alternative
git reset HEAD^ --hard
git push <remote> -f
```
- [Rebase feature branch onto main branch](https://stackoverflow.com/questions/7929369/how-to-rebase-local-branch-onto-remote-master)
```
# Ensure that your local feature-branch is up to date with the remote feature-branch
# and no one else is working on the branch with uncommitted changes
git checkout main
git pull <remote> main
git rebase main <feature-branch>
git push --force-with-lease <remote> <feature-branch>
```

## Config
- Rebase on pull: `git config --global pull.rebase "true"`

## Stash
- List stash: `git stash list`
- Stash with a message: `git stash push -m "my message"`
- Stash a specific file: `git stash -- filename.ext`
- Stash a specific file with message: `git stash push -m "my message" filename.ext`
- Apply stash: `git stash pop` or `git stash apply` or `git stash apply stash@{2}`
- Create branch from stash: `git stash branch <new branchname>`

## Fetching and pulling changes
- Fetch from specific remote: `git fetch <remote>`

## Branch management
- Delete local branch: `git branch -d <branch_name>`
- Delete remote branch: `git push -d <remote_name> <branch_name>`
- Create a new local branch: `git checkout -b <new_branch_name>`

## Remotes
- List remotes: `git remotes -v`
- Add remote: `git remote add <shortname> <url>`
- Pushing to specific remote: `git push <remote> <branch>`
- Get details of a remote: `git remote show <remote>`
- Rename a remote: `git remote rename <old name> <new name>`
- Remove a remote: `git remote remove <remote_name>`

## Commits
- List commits: `git log`
- Move HEAD to a previous commit: `git checkout <commit>`
- [Reset](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset) state to before the commit was done with working changes intact: `git reset` equivalent to `git reset --mixed`
- Reset state to previous commit with working changes GONE: `git reset --hard`
- Revert all changes in a previous commit by creating a new commit: `git revert <commit>`


