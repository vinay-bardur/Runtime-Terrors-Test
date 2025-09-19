# Git Cheat Sheet (for Runtime-Terrors)

## Clone repo (one-time)
git clone git@github.com:YOURUSERNAME/Runtime-Terrors.git
cd Runtime-Terrors

## Branching
# create a feature branch
git checkout -b feat/frontend-login

# see branches
git branch
git branch -r

## Work & commit
git add .
git commit -m "[feat] Add login screen (Firebase Google)"
git push -u origin feat/frontend-login

## Update local main
git checkout main
git pull origin main

## Rebase feature on top of latest main (preferred)
git checkout feat/frontend-login
git fetch origin
git rebase origin/main
# resolve conflicts, then:
git add <file>
git rebase --continue
git push --force-with-lease

## Create PR (web or CLI)
# CLI (fast)
gh pr create --base main --head feat/frontend-login --title "[feat] Add login screen" --body "Implements Google login using Firebase. Test steps: ..."

# Web:
# GitHub -> Pull requests -> New pull request -> choose base main / compare feat/frontend-login -> Create pull request

## Merge PR
# after approval, use GitHub web "Squash and merge" OR:
gh pr merge <PR_NUMBER> --squash --delete-branch

## If merge broke `main` – revert merge commit
git checkout main
git pull origin main
git revert -m 1 <merge-commit-hash>
git push origin main

## Force push safely (use --force-with-lease)
git push --force-with-lease origin feat/backend-fix

## Useful inspection commands
git status
git log --oneline --graph --decorate
git diff origin/main..feat/frontend-login

## Delete local and remote branch after merge
git branch -d feat/frontend-login
git push origin --delete feat/frontend-login

