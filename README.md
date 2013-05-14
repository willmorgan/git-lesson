#  Terminologies
File = blob
Directory listing = tree
Commit = commit
Parent relationships = parent
Name of commit = subject

Commits link backwards, so parent is always included as part of the commit hash
No partial checkouts

# Cloning
Copies all objects from a repository to a new repository, new working tree, etc.
Cloning parent called `origin`

## Origin
Stored in `.gitconfig`
`[origin "name"]
`origin.url`: url where it comes from
`origin.fetch`: microsyntax

`git push origin <local>:<remote>`

# Branching
Create branch using `git branch <name>`, then use `git checkout <name>` to switch working tree to that branch
master is default name of the starter branch
Commits are tip/leaf of branches, many branches => 1 commit
Branches can be moved by changing the reference (bookmark) commit
Can be deleted without deleting the underlying commits
Unstable stuff typically goes in to a new feature branch
When feature branch complete, merge back to master

# Merging
Merge a branch in to master:
`git checkout master`
`git merge <branch>`

### Resolve conflicts by editing the conflicts
`git add conflictedfile.js` to stage the resolved file

`git commit` to complete

Once done, you can delete the branch as it is _just a bookmark_ to a commit.

### Reverse merge (undoing)
`git revert` then `git commit` creates the opposite commit, but on top of previous ones

### Changing where a branch points to if you want to undo changes
Changing a branch to orphan commits means those commits may eventually be removed from the repository due to garbage collection.

## Fast forward merging
Simply repoints the branch at a later commit

# Cherry pick
Copies commits and combines them
`git cherry-pick [<hash>] [<branchname><modifier>]` like `git cherry-pick featurebranch~5`
`-n` flag = nocommit

# Rebase
Just copying a cherry picked a set of commits and applying them on top of another branch.

#### `git rebase -i` = magic
Select a range of commits and lets you plan how the applying works.


# Log
`git log` shows you where you are in the branch
`git log -<n>` shows you last n commit logs

# Create a new repository
`git init` starts new repository, creates `.git`. directory
`git add` adds a file to be tracked as a versionable file - adding to staging area, _not_ repository
`git commit -m <message>` commits staging area to repository
`git commit -am <message>` commits all staged and unstaged to repository
`git rm` removes a file, and adds this action to the staging area (requires a commit)
`git diff a/file.txt b/file.txt` shows a diff between last commit and now
`git diff --cached` shows what is in the staging area
Must `git add` the files needed __each__ commit or it will not be added to the commit
`git add -p` Patch/prepare code to be committed for next big commit (multiple commits per file)
`git checkout <files>` to restore a file (checks out a pristine copy and removes changes)
`git checkout <hash> -- <files>` to check out a file from a particular version
`git checkout <hash>` possible but don't do that... adds a commit without any branch
`git fetch` downloads objects from another repository, discovers other work, synchronises
`git pull` - fetches AND merges
`git cat-file -p <hash>` shows the metadata of a commit/object. stored in `.git/objects`

## ~/.gitconfig
Config stuff:
`git config user.name <name>`
`git config user.email <email>`
Use `--global` switch to write for .gitconfig
Each repo can be customised independently: `.git/config`

## /refs/heads/master
heads contains pointers to commits
master contains only the hash of the commit

# Remotes
Default is called origin. Used interchangeably
dVCS - not as p2p as you might think

Can track remote branches
When people add stuff to remote branches, tracking branches become updated with `git pull`
You push things using `git push`

# HEAD
HEAD is magic name for commit that is currently checked out - working copy

# Index
Staging area, index, cache. Basic concept is new changes go here.

# Committing
Can commit separate parts of a file's changes one at a time (`git add -p`)
Better to make small commits at a time

`git commit --amend` for amending work, forgot whole files maybe, or need to recode

# Microsyntax 
`HEAD^ # (before HEAD - parent)`
`HEAD^^ # (2 before HEAD - grandparent)`
`HEAD~ # (after HEAD - child)`
`HEAD~~ # (2 after HEADmaster - grandchild)`
`HEAD^<n>` or `HEAD~<n>` also work

Read more:
`man git-rev-parse` for full syntax and pretty graphs

# Stashing
`git stash` takes all local changes but not committed, creates "hidden" commit with unfinished data called "stash"
`git stash pop` applies them back (latest)
`git stash apply <hash>` apply a particular set of changes back
`git stash list` to see what's stashed
Conflicts might occur. Resolve and then `git stash drop` when done.

### Fuckup recovery (aka how to screw everything and maybe lose data)
`git reset --hard`
`git reset --soft HEAD^` takes you back to previous commit

# man pages
`git help <command>` gives you a manual for each git command

# Hashing
Don't always _have to_ type full hash - first 5 is _normally_ sufficient
