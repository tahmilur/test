-- https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control
-- https://git-scm.com/downloads
-- https://stackoverflow.com/questions/12254076/how-do-i-show-my-global-git-configuration
-- https://stackoverflow.com/questions/36810467/git-commit-signing-failed-secret-key-not-available
-- If you already have Git installed, you can get the latest development version via Git itself
git clone https://github.com/git/git

git --version
git help config
git add -h
git config --list
git config -l
git config --list --show-scope
-- or look at your ~/.gitconfig file. The local configuration will be in your repository's .git/config file.
git config --list --show-origin
git config user.name
git config user.email
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --global core.editor emacs
git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
git config --global init.defaultBranch main

-- git alias
git config --global alias.c commit
-- then alias will be visible 
c=commit
-- now alias will be workable
git c -m "example of alias"

-- in .gitconfig file, it will be
[alias]
c = commit

-- to edit global Git configuration
git config --edit --global


-- Showing Your Remotes
-- To see which remote servers you have configured
git remote
git remote -v
-- Adding Remote Repositories
-- To add a new remote Git repository as a shortname
git remote add pb https://github.com/paulboone/ticgit
git remote -v
-- Fetching and Pulling from Your Remotes 
git fetch pb
-- Pushing to Your Remotes
git push origin master
-- Inspecting a Remote
git remote show origin
-- Renaming and Removing Remotes
git remote rename pb paul
git remote
-- remove remote
git remote remove paul
git remote

-- Listing Your Tags
git tag
--  only in looking at the 1.8.5 series
git tag -l "v1.8.5*"
-- Creating Tags : lightweight and annotated
-- Annotated Tags
git tag -a v1.4 -m "my version 1.4"
-- You can see the tag data along with the commit
git show v1.4
-- Lightweight Tags
git tag v1.4-lw

-- Sharing Tags
git push origin v1.5
git push origin --tags
-- To delete a tag on your local repository
git tag -d v1.4-lw
-- to delete a tag from a remote server
git push origin :refs/tags/v1.4-lw
git push origin --delete <tagname>

-- Checking out Tags
git checkout v2.0.0

-- Git Branching - Basic Branching and Merging
-- https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging

-- list of local branch
git branch
-- to see all branch including remote
git branch --all
-- to see the last commit on each branch
git branch -v
-- To see which branches are already merged into the branch you’re on, you can run 
git branch --merged
-- To see all the branches that contain work you haven’t yet merged in, you can run 
git branch --no-merged
-- to check merged status whithout checkout with branch
git branch --no-merged master

-- create a new branch named "feature_x" and switch to it using
git checkout -b feature_x
-- switch back to master
git checkout master
-- to merge another branch into your active branch
git merge <branch>
-- push the branch to your remote repository
git push origin <branch>

-- to change branch name in local
git branch --move bad-branch-name corrected-branch-name
-- to change branch name in remote
git push --set-upstream origin corrected-branch-name
-- delete the branch locally
git branch -d feature_x
-- force branch delete when not fully merged
git branch -D feature_x
-- delete remote branch 
git push origin --delete branch-name

-- update your local repository to the newest commit
git pull

-- Git Aliases
git config --global alias.last 'log -1 HEAD'
-- to see last commit
git last

-- create a file named 'README.md' in windows
echo "# test" >> README.md
-- to mark them as merged with
git add <filename>
-- before merging changes, you can also preview them by using
-- to see change files
git diff --name-status <remote-branch> <local-branch>
-- chnage details
git diff <source_branch> <target_branch>
git diff <remote-branch> <local-branch>
git diff origin/master
-- to see what you’ve changed but not yet staged
git diff
-- If you want to see what you’ve staged that will go into your next commit  (--staged and --cached are synonyms)
git diff --staged
git diff --cached
-- add file
git add *
git add README.md
git commit -m "first commit"
-- Skipping the Staging Area during commit , use -a
git commit -a -m "Add new benchmarks"

-- Undoing Things
git commit --amend

-- Unstaging a Staged File
git add CONTRIBUTING.md
git status
git reset HEAD CONTRIBUTING.md
-- Unstaging a Staged File with git restore
git restore --staged CONTRIBUTING.md
-- Unmodifying a Modified File with git restore
git restore CONTRIBUTING.md
-- Unmodifying a Modified File
git checkout -- CONTRIBUTING.md

-- The Three Trees
git cat-file -p HEAD
git ls-tree -r HEAD
git ls-files -s

-- get latest
git fetch --all
git reset --hard origin/master

-- 
git reset HEAD --hard # To remove all not committed changes!
git clean -fd         # To remove all untracked (non-git) files and folders!

-- 
git pull --rebase


-- example -- end up with a single commit — the second commit replaces the results of the first
git commit -m 'Initial commit'
git add forgotten_file
git commit --amend

-- Removing Files
rm PROJECTS.md
git rm --cached README
-- removes all files that have the .log extension
git rm log/\*.log
-- emoves all files whose names end with a ~
git rm \*~

-- Moving Files 
git mv README.md README
-- same as
mv README.md README
git rm README.md
git add README

-- tagging
git tag 1.0.0 1b2e1d63ff

-- log
git log
-- to see particular branch log
git log testing
-- To show all of the branches, add --all to your git log command
git log --all
-- help
git log --help
-- To see only the commits of a certain author
git log --author=bob
-- To see a very compressed log where each commit is one line
git log --pretty=oneline
-- to see an ASCII art tree of all the branches
git log --graph --oneline --decorate --all
-- See only which files have changed
git log --name-status
-- pretty log display
git log -p -2
-- limiting Log Output
git log --since=2.weeks
-- to see particular range log
git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01" \
   --before="2008-11-01" --no-merges -- t/

-- replace local changes : this replaces the changes in your working tree with the last content
git checkout -- <filename>
-- drop all your local changes and commits
git fetch origin
git reset --hard origin/master

-- Git Branching --------------------
git add README test.rb LICENSE
git commit -m 'Initial commit
-- Creating a New Branch
git branch testing
-- create a new branch and switch to it
 git checkout -b <newbranchname>
-- to see branch pointer pointing
git log --oneline --decorate
-- swtiching to branch
git checkout testing
-- Switch to an existing branch
git switch testing-branch
-- Create a new branch and switch to it: version 2.23
git switch -c new-branch
-- Return to your previously checked out branch
git switch -
-- create new fie and commit
echo "# test" >> README007.md
git commit -a -m "Make a change"

-- Basic Branching and Merging ----------------
-- Switched to a new branch "iss53"
git checkout -b iss53
-- shorthand of previous command
git branch iss53
git checkout iss53
-- create new file and commit
vim index.html
git commit -a -m 'Create new footer [issue 53]'

-- Switched to branch 'master'
git checkout master
-- create a new branch 
git checkout -b hotfix
-- Switched to a new branch 'hotfix'
vim index.html
git commit -a -m 'Fix broken email address'
-- checkout mas agin
git checkout master
-- marge hotfix into master
git merge hotfix
-- Deleted branch hotfix.
git branch -d hotfix

-- hotfix branch changes are not in the branch "iss53"
git checkout iss53
git merge master
-- 

-- Switched to branch  "iss53" again
git checkout iss53
-- create new file and commit
vim index.html
git commit -a -m 'Finish the new footer [issue 53]'
-- marge with master
git checkout master
-- Switched to branch 'master'
git merge iss53
-- Deleted branch iss53.
git branch -d iss53

-- ******************************************

-- To fix that you can remove remote origin and link it again. First, check the remote origin:
git remote -v
git remote remove origin
git remote add origin https://github.com/tahmilur/test.git
git pull --ff-only
git branch --set-upstream-to=origin/main
*****************************************************************************

git status
git status -s
git clone https://github.com/tahmilur/test.git

…or create a new repository on the command line

echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/tahmilur/test.git
git push -u origin main

…or push an existing repository from the command line
git remote add origin https://github.com/tahmilur/test.git
git branch -M main
git push -u origin main
git pull


'''''''''''''''''''' open git bash and then '''''''''''''''''''''''''''''''''''''
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh
https://www.w3docs.com/learn-git/ssh-key.html

---------------------------------------------- for security -------
ssh-keygen -t rsa -b 4096 -C "tahmilur@yahoo.com"
eval "$(ssh-agent -s)"
ssh-add -K  /c/Users/developer/.ssh/id_rsa
ssh-add -K  ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa  -- working in windows without -K

-- use the following command to see if more than one ssh-agent process is running
ps aux | grep ssh
kill <PID>

-- list of ssh files
ls -al ~/.ssh

--copy
clip < ~/.ssh/id_rsa.pub

copy that , go to github->setting->keys->ssh-key->new SSH Key

-- To test if SSH over the HTTPS port is possible, run this SSH command:
ssh -T -p 443 git@ssh.github.com
-- to clone the repository, you can run the following command:
git clone ssh://git@ssh.github.com:443/tahmilur/test.git

-- clone to different directory
git clone ssh://git@ssh.github.com:443/tahmilur/test.git /d/xyz

-- https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work
-- https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account
-- https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits
git config commit.gpgsign true
git config --global commit.gpgsign true

-- Signing Your Work
-- Install GPG if not
winget install GnuPG.GnuPG
-- find 
where gpg.exe

-- to set the default format of openpgp
git config --global --unset gpg.format

-- list all  public and private key
gpg --list-secret-keys --keyid-format=long

-- to see alreay installed
gpg --list-keys ~/.gnupg/pubring.gpg

-- if not exists, create one
gpg --gen-key

-- https://stackoverflow.com/questions/36810467/git-commit-signing-failed-secret-key-not-available
gpg --full-generate-key
-- Export the key in ASCII armor format
gpg --list-secret-keys --keyid-format=long
-- Then export it: rsa3072/0EA369A1D98D3ABB
see sec rsa4096/[short-key] 2021-06-14 [SC]
-- Copy the key including the BEGIN/END text.
gpg --armor --export 0EA369A1D98D3ABB


-- Add the GPG armor ASCII key to the GitHub account
-- Go to Profile > Settings > SSH and GPG keys > New GPG key

-- https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key
-- configure Git to use it for signing
C:\> git config --global user.signingkey [short-key]
C:\> git config --global commit.gpgsign true
C:\> git config --global gpg.program "C:/Program Files (x86)/gnupg/bin/gpg"
--

-- with GPG subkey ID-> add (!) at the end
git config --global user.signingkey 4BB6D45482678BE3!
-- with GPG primary key ID
git config --global user.signingkey 0EA369A1D98D3ABB
git config --global commit.gpgsign true
git config --global gpg.program "C:/Users/developer/AppData/Local/Programs/Git/usr/bin/gpg.exe"

-- Set GPG environment variable for the GPG Agent
gpg-agent --version
-- Set the environment variable:
GNUPGHOME=%USERPROFILE%\AppData\Roaming\gnupg

-- Signing Tags:  All you have to do is use -s instead of -a
git tag -s v1.5 -m 'my signed 1.5 tag'
-- show tag v1.5
git show v1.5
-- varify tags
git tag -v <tag-name>
git tag -v v1.4.2.1

-- Signing Commits
git commit -S -m "YOUR_COMMIT_MESSAGE"
git commit -a -S -m "Signed commit"
-- To see and verify these signatures
git log --show-signature -1
git log --pretty="format:%h %G? %aN  %s"

-- If the merge contains only valid signed commits
git merge --verify-signatures non-verify
git merge --verify-signatures signed-branch
git merge --verify-signatures -S  signed-branch

-- Everyone Must Sign
git config --local commit.gpgsign true

git config --global gpg.program "C:/Users/developer/AppData/Local/Programs/Git/usr/bin/gpg.exe"

C:\Users\developer\AppData\Local\Programs\Git\usr\bin\gpg.exe