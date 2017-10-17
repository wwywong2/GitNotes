
Basic steps
=========================================================
git init






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
  e.) git checkout master (reset branch to point to 'master'
  f.) git merge upstream/master (merge code with upstream/master)
  g.) click the sync button in Github Desktop to push the merged update to server



