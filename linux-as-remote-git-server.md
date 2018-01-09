
## USEFUL FOR SETTING UP A LINUX SERVER AS A REMOTE GIT SERVER


If you're using GitHub, GitLab, Visual Studio Team Services, TFS, or another service along those lines, none of this applies to you.

If your remote server is a Linux or Unix machine, the following information might be useful.


## create a new remote only git repo

To create a new repository named foo:

```
cd /sccs/git
mkdir foo
cd foo
git init --bare --shared=2664
```

`--bare` ensures that the repository only contains the version control information and doesn't have any local files. This is necessary to be able to clone and push to it.

`--shared=2664` sets the core.sharedRepository which forces git to do all new file creation with 2664 permissions. This helps avoid issues with multiple people pushing to the repo.


## apply the above to an existing repository

Assuming that foo already exists and we need to fix it, we can do the following:

```
cd /sccs/git/foo
chgrp -R swdev *
chmod -R ug+rws *
```

Edit the file `/sccs/git/foo/config`.

Under the [core] area, add the following line:

`sharedRepository = 2664`


## push local code to the remote git server

Follow "create a new remote only git repo".

In your local Git repo, add a new remote origin:

`git remote add origin ssh://<username>@<serverurl>/sccs/git/foo`

Then push each of your branches to your new origin:

`git push origin branchname`
