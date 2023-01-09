# git

git is an open surce, distributed version control system disigned for speed and efficiency

git is a command line, GitHub is the web interface. GitHub is also a code hosting site, free for public repositories. Gitlab the open-source github, that enterprises can run on their own servers.
# Version Control
* A system that keeps records of your cahnges
* Allows for collaborative development
* Allows yu to know who made what changes and when
* Allows you to revert any changes.

# installation & configuration
```console
$ git config --global user.name "gdagdg"
$ git config --global user.email "ks@visotech.com"
```

//Intializing a Repositry in an Existing Directory
```console
$ touch hello-world.py             # create a file
$ git init                         # Initialize git in current directory
$ tree -a .git/objects             # show tree list of files
$ git add .                        # stage the changes
$ git status                       # Review your changes
$ git commit -m "intial version"   # commit the changes
$ git branch                       # shows a list of local branches
$ git checkout branch_name         # to move to other branch
```