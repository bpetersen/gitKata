#gitKata
The purpose of this kata is to learn some of the basic workflows outlined in Vincent Driessen's excellent blog post, [A Successful Git Branching and Merging Strategy](http://nvie.com/posts/a-successful-git-branching-model/).  Before starting the kata, I recommend you read his post and print off the workflow .pdf at the end of his post. It might be helpful to print off the git cheatsheet in this repository. 

##Introduction

This kata contains 3 workflows - Branch/Merge, Release, and Hotfix.  We'll go through each of them.

Before we get started, let's get our system set up.

####TODO: Setup git, MinGW?, get local repository set up.

##Branch/Merge Workflow
In the branch and merge portion of this kata, we will branch from the develop branch, make some code changes, and then merge back into develop.  Here are the steps to follow:
### Steps
1. Clone the repository and ensure you are currently using the 'develop' branch. 
```bash
$ git branch
  develop
 * master
$ git checkout develop
Switched to branch 'develop'
```
2. Create a new branch so that we can implement a new feature.  Make sure you're branching from develop.
```bash
$ git branch <teamname> develop
$ git checkout <teamname> 
Switched to branch '<teamname>'
Alternately, you can use a command to simultaneously create the branch and switch to it.
$ git checkout -b <teamname> develop
```
3.  Create a new file and commit it to your repository.  
```bash
$ echo "And now we shall present the proof for P = NP:" > proof.txt
$ git status
# on branch <teamname>
# Untracked files:
#    (use "git add <file>..." to include in what will be committed)
#
#        proof.txt
nothing added to commit but untracked files present (use "git add" to track)
$ git add proof.txt
$ git status
# On branch <teamname>
# Changes to be committed:
#    (use "git reset HEAD <file>..." to unstage)
#
#        new file:    proof.txt
#
$ git commit -m "Adding proof file."
```
4.  Merge the changes to the <teamname> repository back into develop while maintaining the history of a branch.
```bash
$ git branch
  develop
 * <teamname>
  master
$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff <teamname>
Merge made by the 'recursive' strategy.
 proof.txt | Bin 0 -> 100 bytes
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 10064 proof.txt
$ git branch -d <teamname>
Deleted branch <teamname> (was e63e694).
$ git push origin develop
(Summary of changes from github).
```

### Branch/Merge Summary
We've now completed the first workflow.  I've been very pedantic about the steps involved.  You'll notice I've used git status when it's not necessary and I check which branch I'm using regularly.  I do this to make sure we get in the habit of always knowing the status of our repository before making any changes.

##Release Workflow
Now that we have a firm understanding of how new features are implemented, let's go through the workflow to release new features into our master repository.  Vincent advises that we use a seperate branch to release, that way, the develop branch without being hindered by the release process.  With that in mind:
+ We may branch off from develop.  
+ We must merge back into develop AND master.  
+ We should follow a naming convention for release branches, i.e. release-\*. Let's get started.
Let's get started.

###Steps
1.  Create the release branch from the develop branch.
```bash
$ git checkout -b release-1.2 develop
Switched to a new branch 'release-1.2'
```
2. Make required changes to the release branch such as a critical bug fix.
3. Commit changes. The -a switch will automatically include all modified and deleted files.
```bash
$ git commit -a -m "Included minor ommitance in proof."
```

### Summary

