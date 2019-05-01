# gitconfig.d
RefWorks specific git configuration files.

Table of Contents
=================

  * [Setup](#setup)
  * [Available commands](#available-commands)
      * [lg - Show log as a tree](#lg---show-log-as-a-tree)
      * [sync - Synchronize branches](#sync---synchronize-branches)
      * [cleanup - Clean up merged branches](#cleanup---clean-up-merged-branches)
      * [publish - Publish branch to origin remote](#publish---publish-branch-to-origin-remote)
      * [url - Get the url for the project origin(GitHub project url)](#url---get-the-url-for-the-project-origingithub-project-url)
      * [create-pr - Create Pull Request](#create-pr---create-pull-request)
      * [create-release - Create a new release](#create-release---create-a-new-release)
      * [create-patch-release - Create a patch release](#create-patch-release---create-a-patch-release)
      * [release - Release the code in the current branch](#release---release-the-code-in-the-current-branch)
  * [Hooks](#hooks)
      * [pre-commit](#pre-commit)
      * [prepare-commit-msg](#prepare-commit-msg)



## Setup
Clone this repository to ~/.gitconfig.d

SSH
```
git clone git@github.com:proquest/gitconfig.d.git ~/.gitconfig.d
```

Include the aliases in your existing .gitconfig file
```
[include]
  path = ~/.gitconfig.d/release-aliases 
  path = ~/.gitconfig.d/general-aliases
```

It should look something like this:
```
# This is Git's per-user configuration file.
[user]
# Please adapt and uncomment the following lines:
  name = Michael Nishizawa
  email = michael.nishizawa@proquest.com

[include]
  path = ~/.gitconfig.d/release-aliases
  path = ~/.gitconfig.d/general-aliases
```

To validate that your setup is correct, the following command should show you the aliases that are recognized:
```
git config --get-regexp alias
```

## Available commands
---
#### lg - Show log as a tree
---
Show a tree representation of the state of the repository

*Usage:*
```bash
git lg
```

*What does it do?*
  * git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all

```
* 20fa088860 - Mon, 19 Feb 2018 10:19:17 -0500 (4 days ago)
|           Updating templates for file attachments to use the Progress Bar directive Fixing Language Dropdown to use ng-cloak Dropdown/dropdown-up style cleanup - Scott A. Engemann
* d2e940d3ee - Tue, 13 Feb 2018 12:36:30 -0500 (10 days ago)
|           Initial Branch Commit - Scott A. Engemann
| * d108cf4ff3 - Thu, 22 Feb 2018 18:06:15 -0500 (21 hours ago) (HEAD -> master, origin/master, origin/HEAD)
| |           Undoing my commit - Scott A. Engemann
| * f59604bc4e - Thu, 22 Feb 2018 18:02:13 -0500 (21 hours ago)
| |           Resolving what would be a conflict - Scott A. Engemann
| *   34ae4eaf01 - Thu, 22 Feb 2018 10:10:40 -0500 (29 hours ago)
| |\            Merge pull request #584 from proquest/feature/RW-253-sbtDeployStyles - Gordon McCowey
| | * 7ced7a9bd6 - Tue, 20 Feb 2018 09:18:37 -0500 (3 days ago) (origin/feature/RW-253-sbtDeployStyles)
| | |           RW-253 review comments and fail on exceptions - PQ\MSwanson
| | * f669f842f5 - Mon, 19 Feb 2018 21:40:01 -0500 (4 days ago)
| | |           RW-253 improve logging for s3 access - PQ\MSwanson
| | * 5167320a93 - Mon, 19 Feb 2018 17:09:25 -0500 (4 days ago)
| | |           RW-253 Support RW3-PROD-OUTPUT-STYLES for updating OutputStyles.zip for staging and prod - PQ\MSwanson
| * |   8e392269e0 - Wed, 21 Feb 2018 17:05:20 -0300 (2 days ago)
```

---
#### sync - Synchronize branches
---
Merge the current branch with the latest specified branch.

*Usage*
```bash
git sync {branch-to-sync}
```
*What does it do?*
  * checkout {branch-to-sync}
  * pull
  * checkout my-branch
  * merge {branch-to-sync}
  
*Example: Merge current branch with latest from master*
```bash
  git sync master
```

---
#### cleanup - Clean up merged branches
---
Deletes local branches that have been merged with master

*Usage*
```bash
git cleanup
```
*What does it do?*
  * git checkout master
  * git branch --merged
  * git branch -d {list of branches}

---
#### publish - Publish branch to origin remote
---
Publishes the current branch to origin(github).

*Usage*
```bash
git publish
```

*What does it do?*
  * git push -u branch-name origin branch-name

---
#### url - Get the url for the project origin(GitHub project url)
---
This returns a url for github that can be used to navigate to the website

*Usage*
```bash
git url
```

*What does it do?*
  * git remote get-url --push origin
  * Reconfigures the url to something you can open in a browser

*Example: Navigate to the project page in github*
```bash
# Mac
open `git url`

# Linux (Ubuntu)
xdg-open `git url`

# Windows
start `git url`
```

---
#### create-pr - Create Pull Request
---
Takes you to the GitHub Pull Request page for this branch.  Currently only available for OSX users

*Usage*
```bash
git create-pr
```

*What does it do?*
  * git publish(see above)
  * Open a web browser to the pull request creation page in GitHub

---
#### create-release - Create a new release
--- 
Creates a new release tag and branch from master

*Usage*
```bash
git create-release {release-name}
```
*What does it do?*
  * git checkout master
  * git pull
  * git checkout -b release/{release-name}

*Example: Create a new release named release/20180201*
```bash
git create-release 20180201
```
---
#### create-patch-release - Create a patch release 
---
Creates a new release branch from the production branch.

*Usage*
```bash
git create-patch-release {release-name}
```
*What does it do?*
  * git checkout production
  * git pull
  * git checkout -b hotfix/{release-name}
   
*Example: Create a new patch release named hotfix/20180201*
```bash
git create-patch-release 20180201
```
---
####  release - Release the code in the current branch
---
Merges a release or patch into the production branch and cleans up the branch.  It expects that you are already have the release branch checked out.

*Usage*
```bash
git release
```
*What does it do?*
  * Check that the current branch is either a release or a hotfix
  * git checkout production
  * git pull
  * git merge --no-ff my-branch
  * git push origin production
  * git push origin --tags 
  * git branch -d my-branch
  * git push origin --delete my-branch
=======
