# Git Cheat Sheet

A lot of stuff in git I'd forget how to do.

## Cloning

### Clone a repo and give name other than origin

```bash
git clone -o upstream https://repo.git
```

## Branches

### Pull a Branch From Remote

**DON’T DO THIS**

```bash
git checkout -b [new_branch]
git pull origin [new_branch]
```

**DO THIS**

```bash
git checkout -b [new_branch] [remote_name]/[new_branch]
```

Example:

```bash
git checkout -b new-emails origin/new-emails
```

### Create a branch without a parent

Very useful when you are updating a project that you are rewriting. For example,
say you are using semantic versioning and are wanting to start a new major
version.

```bash
git checkout --orphan BRANCH
```

### Delete All Branches that have been merged

Great for cleaning up local branches that aren't being used any more.

```bash
git checkout master
git branch --merged | grep -v "\*" | xargs -n 1 git branch -d
```

### Push Branch to Remote Repository to a different branch name

```shell
git push origin [LOCAL-BRANCH-NAME]:[REMOTE-BRANCH-NAME]
```

**Use Case**: I will often use rebase, I will cut a branch off the branch I want to rebase and
do the rebase on the newly created branch. Once I am done, I will check the diff and see if
I screwed up. If it's all good, `git push -f`.

**NOTICE**: DO NOT `git push -f` unless you know
what you are doing.

## Working Tree

### Ignore changes to a file that is being tracked

```bash
git update-index --assume-unchanged [directory|file]
```

### Unignore changes to a file that is being tracked

```bash
git update-index --no-assume-unchanged [directory|file]
```

### Ignore Files for Repository without using `.gitignore`

Add the file `.git/info/exclude` and fill it with the contents you want to ignore. This will ONLY apply to the
repository and will not be tracked by git.

### Squash Commits

```bash
git log
```

Count the number of commits that you have made, let's say the previous 5 are your commits.

```bash
git rebase -i HEAD~5
```

The first commit leave as `pick` the rest will need to be changed to `squash`. After that you will be able to
leave a new commit message or just leave as is to keep the commit messages from all previous commits.

### Working Tree Links

- [Git Rebasing](http://jeffthomas.xyz/git-commit-cleanup)

## Advanced

### Search for an specific line of code/file in the history

```bash
git log -S[search term]
```

Example:

```bash
git log -SThatOneFile.php
```

## Copy file from one branch to current branch

Copy a file from `branch` and put into staging.

```bash
git checkout BRANCH path/to/file.ext

# Real Life Examples
git checkout origin/featureBranch web/js/random.js
# Pulls into your current branch web/js/random.js from
# origin/featureBranch
```

## Git Grep

```shell
# Basic grep (case sensitive)
git grep 'search term'

# Case Insensitive search
git grep -i 'search term'

# Search within a directory
git grep 'search term' src/

# Search only files with `php` extension
git grep 'search term' -- '*.php'

# Grep in the 'src/` directory, only yml files
git grep 'search term' -- 'src/**.yml'
```
