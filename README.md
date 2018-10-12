# The very basics

This is a terse "bootcamp" in on the use of git/github.

Hint: practice with dummy repositories until you get what the commands are doing.

Good links include [this](http://githowto.com/), [this](https://help.github.com/), and [this](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Mergin).

A "cheat sheet" on some advanced features is [here](https://github.com/tiimgreen/github-cheat-sheet).

[This] is an excellent reference on advanced git usage.

# An aside: best practices

To maximize safety of your projects, I __strongly__ suggest the following behavior:

<ol>
<li>You have a "central" server.  On that server, there is a directory called ~/git</li>
<li>You keep all projects you care about in ~/git on that server</li>
<li>You __NEVER__ do __ANY__ editing of code in those repos.  Rather, you always work on a _copy_ of a repo.  This is less convenient, but more idiot-proof.</li>
</ol>
# Creating a repository on github

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

# Creating a repo on your own machine

```
mkdir reponame.git
cd reponame.git
git init
```

That's all--you now have an empty repo!

## Connecting your new repo to github

```
git remote add https://github.com/username/reponame.git
```

Now, the "master" branch of your repo thinks that it originated from your github repo.  You are now ready to add some files.

#"Cloning" a repo

## From your server
To work on a copy of a repo, you "clone" it.  I assume that you have an account on some Unix machine somewhere at your institutions.  For simplicity, we'll assume that you are at UCI.

To clone a repo from your UCI server:

```
git clone username@servername.uci.edu:~/git/reponame
```

Concrete example for one of my projects:

>git clone kevin@REDACTED.bio.uci.edu:~/git/libsequence.git

This command spits out a bunch of stuff relating to files getting copied over.  The end result is a directory called "libsequence" containing the __master__ branch of that project.  (See more on branches below.)

__NOTE:__ you cannot get libsequence from that server because you don't have access to my account on my server.

## From github

You can, however, get a libsequence from my github account by saying

```
git clone https://github.com/molpopgen/libsequence.git
```

## What is the result of cloning a repo?
You get a copy of the default "branch" of that repo.  This is usually called "master", which _should_ represent the current stable version of the code. (It may or may not correspond to the latest _tag_ or _release_ of the code. More on tags below.)

## An aside: getting specific versions of projects

Repositories may contain many "branches" of projects.  For example, if we clone a different repo of mine:

```
git clone https://github.com/molpopgen/fwdpp
```

We can then enter your local copy of my repo:
```
cd fwdpp
```

The main fwdpp repository is remote (e.g., it lives on github).  To see what branches exist on a remote repo, say

```
git branch -r
```

That command will return something like

>origin/HEAD -> origin/master<br>
>origin/dev<br>
>origin/master<br>

Ignore the first line--it is something that git has to worry about.  The second line shows that a branch called "dev" exists at "origin" (which is the remote location from where a repo was cloned).  To switch to that branch:

```
git  checkout dev
```

You usually only want to check out branches if you are interested in the cutting-edge code ( or are a developer working on that code ).  However, you may wish to get a specific __version number__ of a project.  In git-ese, these are called "tags".  In the case of fwdpp, we can ask what tags there are

```
git tag -l
```

Which spits out

> 0.1.5<br>
> 0.1.6<br>
> 0.1.7<br>
> 0.1.8<br>
> 0.1.9<br>
> 0.2.0<br>
> 0.2.1<br>
> 0.2.2<br>

For example, 0.2.2 is the most recent version number.  We can get it by saying:

```
git checkout 0.2.2
```

Note: doing this will get you the code for version 0.2.2.  This is great, as it allows us to get specific versions via the command line.  However, I (as the author) will have a hard time modifying the repo and sending my changes back to github.  This feature is really for users of software, not developers.


#Adding files

```
echo "Not much of a README" > README.md
git add README.md
git commit README.md -m "Inadequate README added"
```

#Committing changes to files

Use your favorite __PLAIN TEXT__ editor.  That means __NOT__ MS Word or some RTF editor.  ___PLAIN  TEXT ONLY!!!___

Then:
```
git commit filename -m "short description of the changes"
```

# Branches

Branches are important:  they let you mess around with files in a way that is totally safe.  In other words, you can delete the branch if you don't like your changes.  No harm has been done, other than some time lost.

__The default branch is called "master"__

Important point that newbies will find frustrating:  if you clone a repo from your server, __you cannot work on the master branch and push those changes back to your server!__  It is simply not allowed.  You _must_ work on a branch.  This puts a level of protection on your master branch back on the home server.  However, you __can__ push a master branch back to github.  (Yes, this is confusing, but it is what it is, so learn it now).

## Creating a branch

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

## Example

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

##See the difference between two branches

```
git diff branch1 branch2
```

Often, you want to see diffs compared to the master.  For example

```
git diff bugfix master
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

# Creating a specific version number for the current version of your master branch.

OK, you've done some nice work,  and you want this to be a release with a specific version number.  In git-land, you "tag" the current branch:

```
git tag 0.1.0 -m "Something about why this is a release"
```

You can then send the release to github:

```
git push origin 0.1.0
```

Once you've pushed the tag, another user can download reponame-0.1.0.tar.gz from the "Releases" tab at your repo's github URL.

## When to tag?

These are rules that I personally use:

* If the code was used in a publication, then you absolutely should create a tag for the version that you used in the paper.  The goal is reproducibility, and that includes any bugs that may be present in the version you used in your paper.  (Bugs are fine, and a fact of life.  You'll get more credit for acknowledging a bug while still allowing the erroneous results to be replicated as opposed to not making your scripts/programs/command lines available at all.)
* If a new feature was added, I often create a tag.
* If a bug was fixed, I often create a tag.

Sometimes, though, you are making additions to the master branch that are unremarkable.  For example, I may make code a bit faster, simpler, or better-commented.  I usually just leave that in "master" because the _output_ that a user would see from running the code would be the same.  Eventually, master may evolve enough so that the code is quite different from the latest release, but I try to restrict myself to the tagging scenarios described above.  Sometimes, though, I forget to tag, which is why I wrote "often" in the above list.

#Modifying someone else's repository

Say you want to work with someone else's code that is on github.  For example, you may have identified a bug and you know how to fix it.  This is what you do:

* Go to their git repo URL and "fork" the repo.  (Upper right gray-ish button that says "Fork").  This means you now have a copy of this repo in your github account!
* Clone __your__ copy of the repo to wherever you like to do your actual work.
* Make changes, commit them, and push them back to your repo
* If you think the original author would be interested in your changes, submit a "pull request".  You'll see the "Pull request" button in the gray bar above the list of files in the repo.  The author will get a notification from github about your request, and will be able to see all of your changes and review them.  The author may approve changes and integrate them into the original repo or reject them at his/her discretion.

