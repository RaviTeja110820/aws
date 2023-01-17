# git

git is an open surce, distributed version control system disigned for speed and efficiency

git is a command line, GitHub is the web interface. GitHub is also a code hosting site, free for public repositories. Gitlab the open-source github, that enterprises can run on their own servers.
> git is basically working locally, but github is something working like globally.

# Version Control
* A system that keeps records of your cahnges.
* Allows for collaborative development.
* Allows yu to know who made what changes and when.
* Allows you to revert any changes.

Version Control:
    * CVS - Centralized
    * SVN - Centralized
    * GIT - Distributed

* **Fork** can create an entire copy of your Original Source

# installation & configuration
```console
$ git --version         # to check git is installed or not
$ git config --list     # previous configurations
$ git config --global user.name "gdagdg"
$ git config --global user.email "ks@visotech.com"
```

//Intializing a Repositry in an Existing Directory
```console
$ touch hello-world.py             # create a file
$ git init                         # Initialize git in current directory
$ tree -a .git/objects             # show tree list of files
```
```console
$ ls -la                           # to view hidden files
$ ls .git                          # .git file is responsible for everything
```


```console
$ git add .                        # stage the changes
$ git status                       # Review your changes
$ git commit -m "intial version"   # commit the changes
$ git push                         # to push the changes
$ git branch -r                    # to view all the branches
$ git branch                       # shows a list of local branches
$ git branch branch_name           # to create a branch with a name   
$ git checkout branch_name         # to move to other branch
$ git merge branch_name            # to merge the branch
$ git branch -d branch_name        # to delete a branch
```

```console
$ git diff                         # to see the exact changes
$ git log                          # to see the commits 
$ git reset --hard commit_id       # versoinig- going back to previous commit
$ git log --oneline                # to see previous commits
$ git checkout commit_id           # to go to that version
```

> master , Feature Branch, Release Branch  

* merge:
  * fast-forward merge



## To Visualize the Git
follow this link -   http://git-school.github.io/visualizing-git/