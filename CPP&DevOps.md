# Doxygen



# Git

## SSH
- `.ssh/config`
- public (`.pub`) and private keys

## Git Basics
- **commit** - basic element, contains changes
- **branch** - commits sequence
- **repository** - branches storage
- **HEAD** - pointer to current commit (last commit in branch)
- Workspace --[`add`]--> staging --[`commit`]--> local --[`push`]--> remote
- Remote --[`pull`]--> local

## Git Branches
- `feature branch` -> `develop` -> `master`

## Git Commands
- `config`: user settings
- `status`, `log`, `diff`: info
  - `git log --oneline --decorate --graph --all`: beautiful info =)
- `checkout`: change branch
- `init`: create `.git` file
  - `git init`
- `clone`: copy remote repo in the directory
  - `git clone <link>`
- `add`, `rm`, `mv`: staging management
  - `git add <filename>` 
  - `git rm --cached`
- `commit`: apply changes
  - `git commit --amend`
- `reset`: return to commit / remove file from staging
  - `git reset <commit_hash> --hard`
  - `git reset <filename>`
- `stash`: hide changes
  - `git stash apply <stash@{1}>`: return hidden changes
- `merge`: merge branch to master(main)
  - Merge conflicts tool: `Sublime Merge`
- `fetch`: download to `refs/remotes/`
- `pull`: download and merge
  - `pull = fetch + merge`
- `git remote add`: upload(create) remote repository
  - `git remote add <remote_name> <remote_link>`
- `push`: apply local changes to remote
  - `git push origin --force`
- `reset`: fit local to remote
  - `git reset <branch> --hard`
- `rebase`: edit commits
  - `git rebase HEAD~<n_commits> -i`: change n commits in interactive mode
  (replace `pick` with the commands)

## Git Advanced
- `git grep`: search in repo
- `.gitignore`: file with names of files and dirs will be ignored
- `git checkout --orphan`: create independent branch
- `git cherry-pick`: copy last commit (without merging)
- **Git Hooks** - commits forbidding
  - `.git/hooks/pre-commit`

# CMake

`cmake ..`

```cmake
# Minimal CMakeLists.txt file

cmake_minimum_required(VERSION 3.16)
project(Main)

set(CMAKE_CXX_STANDARD 20)

add_executable(Main main.cpp)
```
