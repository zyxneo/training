# git cheat sheet

Read your group instruction in the text files 

[group1.md](group1.md)

[group2.md](group2.md)

[group3.md](group3.md)

[group4.md](group4.md)

and place your solution in a fitting category in this file.


## Creating repositories

    $ git init                    turns the  local folder into a git repository

    $ git clone https://...       copies the whole repo with all branches to local

## Staging and committing

    $ git add test.txt            Add the test.txt file to the stage

    $ git add .                   Add all changes and new files (but no deletions)

    $ git add -u                  stages everything which was already tracked (modifications and deletions)
    
    $ git add -A                  Same like above but also adds new files.


    $ git reset HEAD test.txt     Resets test.txt to thes state of HEAD, means unstage already staged changes

    $ git diff --staged           Show diff of already staged changes to HEAD

    $ git commit                  Starts committing and opens a text editor for putting in the message

    $ git commit -a               also adds changes from all known files (skips add)

    $ git commit -m "Add smthg"   Commit with the commit message "Add something"

## Inspecting the repository and history

    $ git status                

prints the current state of the repository, hints at next steps
        
    $ git log 

shows the commits of the current branch

    $ git log --oneline 

shows all commits but only one line commit info
 
    $ git log --oneline --all

shows the history of all files including all branches, but only with one line commit info

    $ git log --oneline --all --graph

graph that shows the branches and shows the branch and merge history

    $ git log --oneline --all --graph --decorate

shows the branch and merge history, and puts more colors in there and gives the names to the branch

    $ git log --follow -p -- filename 

shows the history of the file, with pretty printing, following the history even in case of renaming.

    $ git log -S'static void Main'

searches for the "static void main" string (pickaxe)

    $ git log --pretty=format:"%h - %an, %ar : %s"

allows you to specify your own log format (commit hash, author name, author date, subject)

    $ git cat-file -p a3798b    

reads content of the file where the hash begins with a3798b, with pretty option
    
    
## Managing branches

    $ git checkout work         Command switches to a branch named work.
    $ git checkout master       Switch to commit that master points to
    $ git branch feature1       Create a branch named "feature1"
    $ git checkout -b work      Switch to newly created branch "work"
    $ git checkout work         Switch to existing branch "work"
    $ git branch                List of existing branches, highlights current branch
    $ git branch -v             List of existing branches with reference to latest commit
    $ git branch -a             List of all existing branches, both local and remote
    $ git branch --merged       List branches, that where merged into the current named branch
    $ git branch --no-merged    List branches, that were not merged into the current named branch
    $ git branch -d work        Delete branch "work", stop when something is open/pending/not merged
    $ git branch -D work        Delete branch "work", hard delete also when something is still open

## Merging


    $ git diff                  shows changes of the file and opens kdiff 
    $ git diff --staged         shows difference of staged files
    $ git diff test.txt         shows difference in this file and between two commits
    $ git diff --theirs         shows theirs version and shows difference
    $ git diff --ours           shows what you had in your branch before commit and merge
    $ git merge work	        Command merges work branch into the current branch
    $ git merge --abort         Command canceles the merge if in conflict state 

Here are some standard situations, and a git command. Draw the result, and add some explanation:

Example 1:

    A - B (master)
         \
          C (work)
    
    $ git checkout master
    $ git merge work

Result and explanation here:

    A - B - C (HEAD -> master, work)


Example 2:

    A - B - C - D (master)
         \
          X - Y (work)
    
    $ git checkout master
    $ git merge work

Result and explanation here:

    A - B - C - D - E (HEAD -> master)
         \        /
          X - Y (work)


Example 3:

    A - B - C - D (master)
         \
          X - Y (work)
    
    $ git checkout work
    $ git merge master
    $ git checkout master
    $ git merge work

Result and explanation here:

    A - B - C - D
         \       \
          X - Y - E (HEAD -> master, work)

