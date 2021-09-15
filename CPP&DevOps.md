# Doxygen

- `doxygen -g <path>`: generate Doxyfile with the specified path
- `doxygen <path2Doxyfile>`: generate web from the specified Doxyfile


# SSH
- `.ssh/config`
- public (`.pub`) and private keys
- `ssh-keygen`, `ssh`


# Git

## Basics
- **commit** - basic element, contains changes
- **branch** - commits sequence
- **repository** - branches storage
- **HEAD** - pointer to current commit (last commit in branch)
- Workspace --[`add`]--> staging --[`commit`]--> local --[`push`]--> remote
- Remote --[`pull`]--> local

## Branches Organization
- `feature branch` -> `develop` -> `master`

## Main Commands
- `config`: user settings
- `status`, `log`, `diff`: info
  - `git log --oneline --decorate --graph --all`: beautiful info =)
- `checkout`: change branch
- `init`: create `.git` file
  - `git init`
- `clone`: copy remote repo in the directory
  - `git clone <link>`
- `add`, `rm`: staging management
  - `git add <filename>`
  - `git add -p <filename>`
  - `git rm --cached`
- `commit`: apply changes
  - `git commit --amend`
- `reset`: return to commit
  - `git reset <commit_hash> --hard`
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

## Advanced Commands
- `git grep`: search in repo
- `.gitignore`: file with names of files and dirs will be ignored
- `git checkout --orphan`: create independent branch
- `git cherry-pick`: copy last commit (without merging)
- `git bisect [run <script>] [bad] [good]`: bugs searching
- **Git Hooks** - commits forbidding
  - `.git/hooks/pre-commit`

## Continuous Integration (CI)

- `git submodule init`
- .gitlab-ci.yml
```yaml
style-check:
  variables:
    GIT_SUBMODULE_STRATEGY: recursive
  script:
    - git submodule update --remote
    - bash ci.sh
- 
```
- GitLab Runner
- GitGub Actions
- Travis CI (-> GitHub)


# Build Systems (CMake)

- bash: only commands
- make: commands organized by targets

```makefile
all: ProjectName

ProjectName:
    # commands
    
clean:
    # clean
```

- CMake: generated Makefile
```shell
vim CMakeLists.txt
mkdir build
cd build
cmake ..
make
```

- Simple CMakeLists.txt
```cmake
cmake_minimum_required(VERSION 3.16)
project(Main)

set(CMAKE_CXX_STANDARD 20)

set(SOURCE main.cpp)

add_executable(${PROJECT_NAME} ${SOURCE})
```

- Shared Library
```cmake
# ================================================================
# Library CMakeLists

set(LIB_NAME MyLib)
set(LIB_SOURCE my_lib.cpp)
add_library(${LIB_NAME} SHARED ${LIB_SOURCE})
# ================================================================
# Main CMakeLists
# ...
set(LIB_DIR lib/)
add_executable(${PROJECT_NAME} ${SOURCE})
add_subdirectory(${LIB_DIR})
include_directories(${LIB_DIR})

# PUBLIC for public headers
target_link_libraries(${PROJECT_NAME} PRIVATE ${LIB_NAME})
```

- Boost Linking
```cmake
find_package(Boost COMPONENTS filesystem REQUIRED)
# ...
include_directories(${Boost_INCLUDE_DIRS})
# ...
link_directories(${Boost_LIBRARY_DIRS})
# ...

install(
        TARGETS ${PROJECT_NAME}
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
)
```
- Code Generation
```cmake
add_custom_command(
        OUTPUT gen.h
        COMMAND python generate.py data.json
        DEPENDS generate.py data.json
        COMMENT "Generate file"
)

add_custom_target(
        RunGen DEPENDS hen.h
)

add_executable(...)
add_dependencies(${PROJECT_NAME} RunGen)
```


# Docker Containerization

- Dockerfile
```dockerfile
FROM alpine:latest

# Environment variables
ENV X=8:

# Execute commands in the container
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    clang \
    clang-format \
    valgrind \
    vim
    
WORKDIR /srv/
COPY ./wspace ./src/
```

- Docker Compose
  - docker-compose.yml
```yaml
version: '2'

volumes:
  pgdata:
    driver: local

services:
  alpine:
    restart: always
    image: alpine:latest
    build:
      context: .
      dockerfile: .
    ports: ['22']
    volumes: [.]
    command: .
    depends_on: .
```