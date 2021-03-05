# Installation

## Windows

https://git-scm.com/

> reboot

    git --version

# Basic Operating

## Config Git

    git config --global user.name "<username>"
    git config --global user.email <user e-mail>
    git config --list

Selected.

    git config --global core.editor "<your editor destination>"

## With VS Code

### Push to Newly Repository

If use Github, the first branch is "main".

    git init
    git add README.md
    git commit -m "<commit details>"
    git branch -M <branch name>
    git remote add origin https://github.com/<your account>/<your repository>.git
    git push -u origin <branch name>

The -u is --set-upstream, after setted. You can use this.

    git push

### Push to Existed Repository

If use Github, the first branch is "main".

    git remote add origin <https url>
    git branch -M <branch name>
    git push -u origin <branch name>

The -u is --set-upstream, after setted. You can use this.

    git push