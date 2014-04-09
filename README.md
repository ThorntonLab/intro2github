#The very basics

This is a terse "bootcamp" in on the use of git/github.

Hint: practice with dummy repositories until you get what the commands are doing.

Good links include [this](http://githowto.com/), [this](https://help.github.com/)), and [this](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Mergin).

##An aside: best practices

To maximize safety of your projects, I __strongly__ suggest the following behavior:

<ol>
<li>You have a "central" server.  On that server, there is a directory called ~/git</li>
<li>You keep all projects you care about in ~/git on that server</li>
<li>You __NEVER__ do __ANY__ editing of code in those repos</li>
</ol>
##Creating a repository on github

From your account (github.com/username):

<ol>
<li>Click "Repositories"</li>
<li>Click "New" (green button near top right of screen)</li>
<li>Give it a name and a description</li>
<li>Click "Create Repository"</li>
</ol>

You will then see something that looks like the following, and is instructions for how to create a new repo on your own server:

> touch README.md<br>
> git init<br>
> git add README.md<br>
> git commit -m "first commit"<br>
> git remote add origin https://github.com/molpopgen/dummy.git<br>
> git push -u origin master<br>

and this, which is how to connect an existing repo to github:

>git remote add origin https://github.com/molpopgen/dummy.git<br>
>git push -u origin master<br>

The above two blocks are recipes.

##Creating a repo on your own machine

```
mkdir reponame.git
cd reponame.git
git init
```

That's all--you now have an empty repo!

###Connecting your new repo to github

```
git remote add https://github.com/username/reponame.git
```

Now, the "master" branch of your repo thinks that it originated from your github repo.  You are now ready to add some files.

##Adding files

```
echo "Not much of a README" > README.md
git add README.md
git commit README.md -m "Inadequate README added"
```

##Committing changes to files

Use your favorite __PLAIN TEXT__ editor.  That means __NOT__ MS Word or some RTF editor.  ___PLAIN  TEXT ONLY!!!___

Then:
```
git commit filename -m "short description of the changes"
```

#Branches

Branches are important:  they let you mess around with files in a way that is totally safe.  In other words, you can delete the branch if you don't like your changes.  No harm has been done, other than some time lost.

__The default branch is called "master"__

Important point that newbies will find frustrating:  if you clone a repo from your server, __you cannot work on the master branch and push those changes back to your server!__  It is simply not allowed.  You _must_ work on a branch.  This puts a level of protection on your master branch back on the home server.  However, you __can__ push a master branch back to github.  (Yes, this is confusing, but it is what it is, so learn it now).

##Creating a branch

```
git branch branchname
```

##Listing all branches

```
git branch -a
```

##Switching to a branch

```
git checkout branchname
```

##Example

First, clone the repo from your server to your laptop (for example):

```
git clone username@server:~/git/reponame.git
cd reponame
git branch dev
git checkout dev
```

Now, you can make whatever changes you like.  If you hate the changes:

```
cd ..
rm -rf reponame
```

That's right, you can just delete the whoe thing.  Why?  Because you are too smart to actually work on the repo that you store on your server, right?  You __always__ work from a copy.

If you like them, commit your changes and send the dev branch back to your server:

```
git push origin dev
```

Then, back on your home server, if you __really__ like the changes and think that they are stable:

```
git merge dev master
```


Then, share your new master branch with the world by pushing from your server to github:

```
git push origin master
```

You can push any branch to  github (more generally, to any "origin"):

```
git push origin branchname
```

##Deleting branches

In the current repo:

```
git branch -d branchname
```

On a remote repo (your server, github, etc.):

```
git push origin :branchname
```

