Basic steps
=========================================================
1.) start
git init - create the folder structure
git status - check status

2.) add files to stage
git add file.txt - add file to staging - now it is tracked (to be committed)
git add -A . (add all recursively, and also file deletions are included)
git add --all
git add '*.txt' (need quote so Git can receive the wildcard before shell, and search recursively)

git rm --cached file.txt (remove from staged, but keep in working dir)
git reset file.txt (to remove a file from staging)

3.) commits
git commit -m "Add title"
git commit -am "delete stuff" (this will remove deleted files plus commit)

git log (show commit history)
git log --summary (more detail)

4.) push to remote
git remote add origin "https://github.com/github-site/try.git" (origin can be any name but first is origin)
git push -u origin master (name of remote=origin, name of default local branch=master; u to remember settings)
git push (next time)

5.) pull from remote
git pull origin master
or 
git stash (to stash your changes, and...)
git stash apply (call this to re-apply changes after pull)

6.) diff
git diff HEAD
git diff --staged

7.) removing files from staged (reset will move current branch to the new location - and remove commits?)
(the only usage of reset file is to separate it back out to unstage so the stage can have the files you want for 1 commit -- that is if you add file unintentionally to the current commit)
git reset file.txt (file cannot do --soft or --hard; so just put the file out of index -- become unstaged; if already unstaged, it does nothing)

7a.) remove commit
git reset --soft HEAD~ (move the branch which is pointed by HEAD to parent of HEAD - uncommit; and index remainds the same = the last commit -> staged contents)
git reset --mixed HEAD~ (move the branch which is pointed by HEAD to parent of HEAD and make index same as HEAD - uncommit and last commit will become unstaged contents) <- --mixed is default
git reset --hard HEAD~ (move the branch which is pointed by HEAD to parent of HEAD and make index same as HEAD PLUS also make the working dir same as HEAD - uncommit remove all changes; they are lost forever!)
git reset 9e5e6a4 (move the branch which HEAD is currently pointing (e.g. master) to commit 9e5e6a4, make index the same; last commit will become unstaged contents)

8.) undo changes (checkout will only move HEAD without moving branches)
git checkout -- file.txt (-- is placeholder to tell git no option)
git checkout stuff       # checkout the branch 'stuff'
git checkout -- stuff    # checkout the file 'stuff'

9.) branch
git branch bname
or
git checkout -b new_branch (= git branch new_branch + git checkout new_branch)

10.) remove files from local + staged
git rm '*.txt'
or git rm -r foldername (to recursively remove folders and files)
then commit by
git commit -m "some title"
or
git commit -am "delete stuff" (this will remove deleted files plus commit)

11.) go back to master branch to merge chaages
git checkout master

12.) merge
git merge clean_up

13.) now remove branch that is already merged
git branch -d bname (this only work if branch has been merged)
git branch -d -f bname (this will work even if banch hasn't been merged)

14.) push back
git push (no need param this time)



Cycle of file in git (push is to update cloud)
=========================================================
untracked (new file) -add->   staged/tracked-modified (added)   -commit-> staged/tracked-unmodified (committed) ---push to github--->
untracked (removed) <-remove- staged/tracked-modified (changed) <-modify- staged/tracked-unmodified (synced)    <---pull/clone from github---



How I clone my project to organization 
=========================================================
(don't fork, do mirror, because fork can't change original public project to private)
1.) In organization, create new repository
  a.) give it name and description, but don't select any setting (except private)
  b.) don't select Initialize this repository with a REAME
  c.) create it empty for later use
2.) copy project to new location (e.g. D:\GitHub\ttskpiraw -> D:\GitHub\ttsdev\ttskpiraw)
3.) New repository in Github Desktop and select the folder
4.) Click on add this repository instead
5.) In Repository settings, change primary remote repository to the new address (e.g. https://github.com/ttswirelessdev/test.git)
6.) Push the sync button and again for Publish branch
7.) from now on, to sync from original project (in my side), open git bash in that folder
  a.) add remote, first by verifying: git remote -v, should show
    origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
    origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
  b.) git remote add upstream https://github.com/wwywong2/ttskpiraw.git
  c.) git remote -v again, should show
    origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
    origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
    upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
    upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)
  d.) to sync anytime from original/remote, git fetch upstream
  e.) git checkout master (reset branch to point to 'master')
  f.) git merge upstream/master (merge code with upstream/master)
  g.) click the sync button in Github Desktop to push the merged update to server



How to modify/rename/copy master
=========================================================
1.) git branch -m master old_master (rename master to old_master for removal later)
2.) git checkout other_place
3.) git branch new_master (create new branch call new_master)
4.) git push testorig new_master (create new branch in web)
5.) in web, set default to new_master, to free up master
6.) in web, remove master
7.) in web, create new branh from new_master, call it master
8.) in web, set default to master (this time it is the new one)
9.) in local, git branch -m new_master master (rename new master back to master)
10.) in local, git checkout master
11.) in local, if extra new_master, do this: git branch -d new_master
12.) in local, if extra old_master, do this: git branch -d old_master



How to get reflog from local (to revive branch/commit)
=========================================================
1.) git reflog
2.) use commit info to do whatever you want (git reset, git checkout, etc)



How to get reflog from remote (github) (to revive branch/commit)
=========================================================
1.) curl https://api.github.com/repos/wwywong2/hello-world2/events > test.txt
2.) find the commit sha you needed
3.) go click any commit get the url, e.g. https://github.com/wwywong2/hello-world2/commit/ccd3f433d4faf01a490cc0150ad7d672b876a62d
4.) replace the sha by the one you needed, it will load that commit (detached), then click "Browse files"
5.) click on Tree, and type new name to create branch from that commit
6.) done. branch revived (so you can pull files and work with pass files)


