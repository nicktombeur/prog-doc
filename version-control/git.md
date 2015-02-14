**Links**

  * [Documentation](http://git-scm.com/docs)
  * [Book](http://git-scm.com/book/en/v2)

<br />

**Initializing**
    
    
    $ git init
    
<br />

**Current state of the project**
    
    
    $ git status

Tip: use git status often.

<br />

**Adding a file**
    
    
    $ git add <file>
    
<br />

**Adding multiple files with a wildcard**
    
    
    $ git add '*.txt'
    
<br />

**Add all files**
    
    
    $ git add -A .
    

Where the dot stands for the current directory (recursive).

-A ensures even file deletions are included.

  * staged: Files are ready to be committed.
  * unstaged: Files with changes that have not been prepared to be committed.
  * untracked: Files aren't tracked by Git yet.
  * deleted: File has been deleted and is waiting to be removed from Git.

<br />

**To store our staged changes, use the commit command with a message.**
    
    
    $ git commit -m "my message"
    

Make sure to check what files and folders are staged before you commit.

<br />

**Show history of commits**
    
    
    $ git log
    

Use --summary to see more information for each commit.

<br />

**Add a remote repository**
    
    
    $ git remote add origin <url>
    

origin is the name we gave to our remote name.

<br />

**Pushing remotely**
    
    
    $ git push -u origin master
    

-u tells Git to remember the parameters. Next time we can simply run git push.

origin = name of our remote

master = default local branch name

<br />

**Pulling remotely**
    
    
    $ git pull origin master
    
<br />

**Stash changes**
    
    
    $ git stash
    

You can stash your changes, if you don't want to commit just yet. Use `git stash apply` to re-apply your changes after your pull.

<br />

**Show differences after pull**
    
    
    $ git diff HEAD
    

HEAD points to your most recent commit.

<br />

**Staged differences**
    
    
    $ git diff --staged
    
<br />

**Unstage files**
    
    
    $ git reset <file/files>
    
<br />

**Undo changes and go back to last commit**
    
    
    $ git checkout -- <target>
    

\-- promises the command line that there are no more options after it. If you happen to have a branch and file with the same name, it will revert the file.

<br />

**Branching**
    
    
    $ git branch <name>
    

If you're working on a feature or bug, you'll often create a branch of the code so you can create separate commits. When you're done, you can merge the branch back into the main master branch.

<br />

**See all branches**
    
    
    $ git branch
    
<br />

**Switching branches**
    
    
    $ git checkout <name>
    
<br />

**Removing files**
    
    
    $ git rm <file/files>
    

It will not only remove the actual files from disk, but will also stage the removal of the files. Use -r to recursively remove folders and files.

If you didn't use git rm to delete a file, you can still do it by using '-a' on 'git commit'.

<br />

**Merge branch into the master branch.**
    
    
    $ git checkout master
    $ git merge <branch-name>
    
<br />

**Deleting branch**
    
    
    $ git branch -d <branch-name>
    

-d won't let you delete something that hasn't been merged. You can either add the --force (-f) or use -D which combines -d -f.

<br />

More soon ...
