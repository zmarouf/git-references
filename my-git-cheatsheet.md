

----------------------------------------------------
## UNCOMMON BUT USEFUL COMMANDS


### interactive rebase

`git rebase -i HEAD~3`

Follow the prompts to wield the power to rewrite history.


### throw away changes that aren't checked in.

Warning! You can lose code doing this.

`git reset --hard`


### create a patch

`git format-patch <branch_name> --stdout > ~/a-handy-patch-name.patch`


----------------------------------------------------
## BRANCH HYGIENE


### push a local only branch remote

`git push --set-upstream <remote> <branch_name>`


### delete a local branch

`git branch -D <branchName>`


### delete a remote branch

`git push origin --delete <branch_name>`

Don't use the prefix `origin/` within `<branch_name>`.


### clean up local list of available remote branches

`git remote prune origin`


### set an upstream branch

`git branch -u <remote>/<branch_name>`


### force a branch to exactly match the remote branch after diverging:

Warning! You can lose code doing this.

```
git fetch origin
git reset --hard origin/<branch_name>
```


----------------------------------------------------
## DEALING WITH REMOTE URLS


### show all remote destinations and their URLs

`git remote -v`


### add a remote

`git remote add <remote_name> <url>`

Example 1 (this git-references repository):

`git remote add origin git@github.com:crybx/git-references.git`

Example 2 (foo.git on a Linux server):

`git remote add origin ssh://<username>@<serverurl>/foo.git`


### remove a remote

`git remote rm <remote_name>`


### update an existing remote's url

`git remote set-url origin <new_origin_url>`


----------------------------------------------------
## GIT JUST INSTALLED - SETUP STEPS


### check current user information

```
git config --global user.name     
git config --global user.email
```


### set current user information

```
git config --global user.name "Username"     
git config --global user.email "your.email@example.com"
```


### check line endings setting

`git config core.autocrlf`


### set line endings setting

`git config core.autocrlf <true/false>`

false means don't convert anything
true is what you want if all work will be done on Windows
I've read so much about git and line endings and I still get frustrated. I don't like any of the options.


### generate an SSH key

on pc (per GitHub's directions):

`ssh-keygen -t rsa -b 4096 -C "your.email@example.com"`

on pc:

`ssh-keygen -t rsa -C "your.email@example.com"`

add key to server (on a Linux box serving as a Git server):  

`cat ~/.ssh/id_rsa.pub | ssh user@hostname 'cat >> ~/.ssh/authorized_keys'`
