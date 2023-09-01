# Git and Github cheatsheet

## Setting git for the first time

```bash
git --version
git config --global user.name "User name"
git config --global user.email useremail@email.com
git config --global user.ui true
git config --global init.defaultBranch main
git config --list
#Setting VS Code as the default editor
git config --global core.editor "code --wait"
git config --global -e
# standardize line breaks in windows
git config --global core.autocrlf true
# standardize line breaks in linux/mac
git config --global core.autocrlf input
# see all configurable options in the CLI
git config -h
# see all the configurable options in the browser
git help config

```

### Initialize Git in a local repository

```bash
mkdir directory name
cd directory name
touch README.md
touch .gitignore
git init
code .
```

### Git and GitHub basic flow

The Git flow consists of three local states, that is, on the computer where you are working and one more remotely when we access the centralized code on platforms such as GitHub, Gitlab, Bitbucket, etc.

These states are modified, staged, committed, and remote. Each of them corresponds to a work area:

- Working Directory: It is the area corresponding to the modified state and it is the local folder of your computer where you store the files of your project.

- Staging Area: It is the area corresponding to the staged state, it is also called index because it is the area where git indexes and adds the changes made to the files prior to committing them in its registry.

- Local Repository: It is the area corresponding to the committed state, where the changes have already been registered in the git repository. It is also called HEAD because it indicates in which change the repository pointer is located.

- Remote Repository: It is the area corresponding to the remote state and it is the remote directory where we store the project files on a web platform such as GitHub, GitLab, BitBucket. Git names the remote repository origin.

![Git flow](https://jonmircha.com/img/blog/git-flow.png)

```bash
# to add the changes made to a file to the staged state
git add file/directory
# add all the changes made to all files and folders to the staged state
git add .

git commit -m "text describing the changes made"

# add remote origin of your repository
git remote add origin https://github.com/user/repository.git
# use this the first time you link the remote and local repository together
git push -u origin master
# after that, as long as you do not change of branch, you can use this short one
git push
# in order to download the changes made in the remote repository to the local one
git pull
```

### New repositories

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/user/repository.git
git push -u origin main
```

### Existing repositories

```bash
git branch -M main
git remote add origin https://github.com/user/respository.git
git push -u origin main

```

### (.gitignore)

In the .gitignore file, you want to put everything that you do not want to include in your repository. This can be done manually or with the help of this link: [gitignore.io](https://www.gitignore.io/)

### Cloning repositories

```
git clone https://github.com/user/repository.git

```

### Branches

```bash
A branch allows to isolate a new function of the code that afterwards can be included to the main version.

# create a branch
git branch branch-name

# change the name of a branch
git checkout branch-name

# create a branch and switch to it
git checkout -b branch

# delete a local branch
git branch -d branch-name

# delete a remote branch
git push origin --delete branch-name

# force the elimination of a branch
git branch -D branch-name

# list all branches in the repository
git branch

# list all branches that are not merged to the main version
git branch --no-merged

# list all branches that are merged to the main version
git branch --merged

# overtake/rebase branches
git checkout second-branch
git rebase main-branch
```

### Mergings

Merge two branches. The way to do it is:

1. Get into the branch that will be the final branch.

2. Merge them.

It can lead to two different results:

- Fast-forward: everything goes smoothly, without any conflict between branches or whatsoever.

- Manual Merge: there is a need to make the merge manually in order to solve any conflict or issue like content duplication.

```bash
# Get into the main/final branch
git checkout main-branch

# Initiate the merge with the secondary branch
git merge secondary-branch
```

### Lastminute changes

It is possible to modify the last changes made

```bash
# without editing the message/text of the last commit
git commit --amend --no-edit

# editing the message/text of the last commit
git commit --amend -m "new message/text"

# delete the last commit
git reset --hard commit name

```

```bash
# switch to an specific branch
git checkout branch-name

# switch to an specific commit made
git checkout id-commit

```

### History

```bash
# allows to see all the history of a project with the info, date, author and id of each change.
git log

# shows the changes in only one line
git log --oneline

# save the log in the file and directory specified
git log > commits.txt

# shows the history in the format specified
git log --pretty=format:"%h - %an, %ar : %s"

# it will show the changes made with the n number specified, in other words, -1, -2, -3, etc
git log -n

# shows the changes made after an specific date
git log --after="2019-07-07 00:00:00"

# shows the changes made before an specific date
git log --before="2019-07-08 00:00:00"

# shows the changes made in a certain range of time
git log --after="2019-07-07 00:00:00" --before="2019-07-08 00:00:00"

# shows a graphic of the changes made in the history, branches and mergings
git log --oneline --graph --all

# shows all the records of the log
# including insertions, changes, removals, mergings, etc.
git reflog

# differences between Working Directory and Staging Area
git diff

# shows a graphic of commits
git log --oneline --graph --all

```

### Reseting history

Can be made in order to delete/remove the history of changes made to a project taking an specific point as a reference.

```bash
# shows a list of new (untracked), deleted or modified files
git status

# deletes head HEAD
git reset --soft

# deletes HEAD and Staging
git reset --mixed

# deletes everything: HEAD, Staging and Working Directory
git reset --hard

# undoes all changes made after the commit specified, keeping the changes locally
git reset id-commit

# discard all history and return to the commit specified
git reset --hard id-commit
```

### Reseting a repository

If there is a need to reset the history of a repository to make it as if it was just created, follow this steps:

```bash

cd repository-directory
mv .git/config ~/saved_git_config
rm -rf .git
git init
git branch -M main
git add .
git commit -m "initial commitl"
mv ~/saved_git_config .git/config
git push --force origin main

```

### Remote

```bash
# shows the remote origin of the repository
git remote

# shows the remote origin with specific details
git remote -v

# add a remote origin
git remote add nombre-orígen https://github.com/user/repository.git

# rename a remote origin
git remote rename old-name new-name

# delete a remote origin
git remote remove nombre-orígen

# download a remote branch to a local one different from the main branch
git checkout --track -b rama-remota origin/rama-remota

```

### Tags

It makes possible to create versions of the code, library or project.

```bash
# list tags
git tag

# create a tag
git tag version-number

# delete a tag
git tag -d version-number

# shows tag info
git show version-number

# syncs tag from local repository to remote repository
git add .
git tag v1.0.0
git commit -m "v1.0.0"
git push origin version-number

# create a tag with a commit message/text
git add .
git tag -a "v1.0.0" -m "Tag message/text"
git push --tags
```

### GitHub Pages

```bash
gh-pages is a special branch to create a website hosted directly in the GitHub repository.

Repository URL: https://github.com/user/repository
Website URL: https://user.github.io/repository
In order to do this, follow this steps:

git branch gh-pages
git checkout gh-pages

git remote add origin https://github.com/user/repository.git
git push origin gh-pages

# to download the changes made on the remote repository to the local one
git pull origin gh-pages

```

### Colaborate on GitHub

In order to collaborate on projects hosted on GitHub, we need to make use of forks and pull requests, tools that the platform offers us for this purpose.

The following describes the collaboration process on GitHub.

1. Fork the repository you want to contribute to, to do so, follow the instructions in this [link.](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

2. Once the repository is forked in your GitHub account, clone it to your computer.

3. In the local repository you have to configure the remote origins of your new copy to have both the remote ones and the original, to do so, follow the instructions in this [link.](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/configuring-a-remote-for-a-fork)

4. Create a new branch in your local fork to do your collaboration, and sync it with your remote repository, to do so, follow the instructions in this [link.](https://docs.github.com/en/pull-requests/collaborate-with-pull-requests/work-with-forks/synchronize-a-fork)

5. Configure your repository to accept changes (pull request), to do so, follow the instructions in this [link.](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/work-with-forks/allow-changes-to-a-pull-request-branch-created-from-a-fork)

6. Create a pull request, to do so follow the instructions at this [link.](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

7. Wait for the owner of the original repository to accept your changes.

8. Once your pull request is accepted, it is recommended that you delete the branch where you worked on the change and update your forked repository with the changes from the original repository.

Summary of the commands to execute to collaborate in a GitHub repository:

```bash
# fork repository
git clone https://github.com/user/repository.git
git remote -v
git remote rename origin fork
git remote add origin https://github.com/user/repository.git
git checkout -b new-branch
git push fork new-branch
# make the pull request
# accept the pull request

# then, delete the branch
git checkout main
git pull origin main
git push fork main
git branch -d new-branch
git push fork --delete new-branch

```

### More info

For more info, take a look to:

[JonMirCha's Blog.](https://jonmircha.com/git) Source of this info.

- [Official Website](https://docs.github.com) de _Git_ & _GitHub_.
- [_Git_ - La guía sencilla.](http://rogerdudler.github.io/git-guide/index.es.html)
- [Libro _Pro Git_.](https://git-scm.com/book/es)
