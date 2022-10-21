https://github.com/ofrymakdasy/Crash-course.git# GitHub Crash Course
> GitHub is an Internet hosting 
> service for software development and 
> version control using Git.


## What is version control?

## What is in this README and what not?
* GitHub Workflow
* Basic Git Commands
* ~~Rollbacks~~
* GitHub Actions
* MD File
* ~~How git version control works~~


## Basic Terms

_Repositories, Branch, Pull Request_

![github workflow](https://www.legitsecurity.com/hs-fs/hubfs/Frame%201%20(1).png?width=1575&name=Frame%201%20(1).png)

## [Git Commands](https://dzone.com/articles/top-20-git-commands-with-examples)

Using the next commands is from the command prompt when navigating to the desired directory.

`git clone`
This command is used for downloading the latest version of a remote project and copying it to the selected location on the local machine. It looks like this:
```commandline
git clone https://github.com/ofrymakdasy/Crash-course.git
```

`git status`

`git add` This is the command you need to use to stage changed files. You can stage individual files or all the files:
```commandline
git add .
git add styles.css 
```

`git commit` A commit is like local a snapshot of the current state of the branch, to which you can always come back. To create a new commit, type this command:
```commandline
git commit -m "Special msg about this commit"
```

`git push` Git push will push the locally committed changes to the remote branch.

`git pull` Using git pull will fetch all the changes from the remote repository and merge any remote changes in the current local branch.

`git branch`

`git init`

## PR - Pull Request
Pull requests are a mechanism for a developer to notify team members that they have completed a feature.
When you file a pull request, all you’re doing is requesting that another developer (e.g., the project maintainer) pulls a branch from your repository into their repository. 

## Important Files

**.gitignore**

It is true that uploading to GitHub is important, but equally important is what we do not upload to GitHub.
`.gitignore` file can be in every folder in a project! The file looks something like this:

```commandline
# Secrets
venv/
.env

# tests
test.py
```

## Using Git in Local Machine

## [GitHub Actions](https://docs.github.com/en/actions)
GitHub Actions makes it easy to automate all your software workflows, now with world-class CI/CD.
### CI - continuous integration / CD - continuous delivery
A method to frequently deliver apps to customers by introducing automation into the stages of app development.

[Buildozer Ex.](https://github.com/ofryma/Dawn-kivyMD-app/tree/master/.github/workflows) - automatic build of the dawn app using buildozer

[Heroku Ex.](https://github.com/ofryma/shambala-schedual/tree/master/.github/workflows) - automatic deploy a website to heroku servers

## [.md - Markdown File](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) 
The purpose of the README file is to convey the nature 
of the project (or part of the project) to anyone who 
enters the project. The README file found in the root 
directory will be displayed automatically upon entering 
the repo.







