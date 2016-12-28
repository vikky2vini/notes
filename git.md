## git

###### List current settings:
	$ git config --list'

###### Set user info:
  1. git config --global user.name "Jay LaCroix"
  2. git config --global user.email somebody@somewhere.net
  3. git config --global core.editor vim
  4. Note: Run the above commands without the --global option to set the parameters for a single project.

###### Check specific user value:
	$ git config user.name (to show what the user's name is set to)

###### Create a repository:
	$ git init

###### Create a bare repository:
	$ git init --bare

###### To inspect a Remote:
	$ git remote show origin

###### To remove a file from version control and working directory:
	$ git rm

###### To remove a file from version control but not remove it from your working directory:
	$ git rm --cached myfile.txt

###### To restore a deleted file:
	$ git rev-list -n 1 HEAD -- <file_path>
	$ git checkout <deleting_commit>^ -- <file_path>

###### To move or rename a file:
	$ git mv myfile myrenamedfile

###### Stage a file for commit:
	$ git add <filename>

###### To commit all files that are set to be staged, run:
	$ git commit

###### To commit all files that are set to be staged, and git an overview of what was changed:
	$ git commit -v

###### To commit everything:
	$ git commit -a

###### To commit and write the comment inline:
	$ git commit -m "This is a message."

###### Show information regarding a commit:
	$ git show <checksum> (or tag id)

###### To get more info than the git status command provides, use (doesn't show staged changes):
	$ git diff

###### To get more info that the git status command provides and view cool colors, use:
	$ git diff | colordiff

###### To view what was staged that will go into the next commit:
	$ git diff --staged (or git diff --staged | colordiff)

###### To view a log of changes:
	$ git log

###### To view a log of the last two entries with the diff included:
	$ git log -p -2

###### To view log with abbreviated stats:
	$ git log --stat

To view log with easier to read output:
	git log --pretty=oneline

###### View tags:
	$ git tag

###### Create an annotated tag (annotated tags vs lightweight tags are stored on the server as actual objects):
	$ git tag -a v1.4 -m "my version 1.4"

###### Create an annotated tag after the fact:
	$ git tag -a v1.2 <checksum>

###### Push tag to the server (by default these are not pushed):
	$ git push origin <tag_id>

###### Transfer tags along with changes:
	$ git push origin --tags

###### List all branches:
```$ git branch```
or:
```$ git show-branch (more info)```

###### View last commit on ech branch:
	$ git branch -v

###### Create a new branch:
	$ git branch branch_name

###### To switch to an existing branch, run:
	$ git checkout mybranch

###### Create a branch but also switch over to it at the same time:
	$ git checkout -b branch_name

###### To delete an existing branch (currently checked out branch is marked by '*'):
	$ git branch -d mybranch

###### To push a new branch to the server:
	$ git push origin mynewbranch

###### Merging a branch
First checkout the branch you would like to merge into. Then:
```$ git merge mybranchtomerge```
Note: If there are conflicts, git adds conflict-resolution markers to the files that have conflicts so that you can open them manually and resolve the issues.

###### To view where a git repository came from:
	$ git remote -v

###### To set the origin to something else (using Github as an example):
	$ git remote add origin https://github.com/jlacroix82/Project_Name.git

###### To add an additional push URL:
    $ git remote set-url --push --add origin <origin-url>
    $ git remote set-url --push --add origin <additional-url>

###### To create a shortname to use to eliminate needing to type the entire origin URL:
	$ git remote add <shortname> git://github.com/mygiturl/myproject.git

###### To rename a shortname:
	$ git remote rename current new

###### Add a submodule:
    $ git submodule add https://github.com/scrooloose/nerdtree.git vim/bundle/nerdtree

###### Show installed submodules:
    $ git submodule status

###### Pull submodules after cloning the main repository:
    $ git submodule init && git submodule update

###### Update all submodules:
    $ git submodule foreach git pull origin master

###### Remove a submodule:
1. Delete the relevant section from the .gitmodules file
2. Stage the .gitmodules changes (git add .gitmodules)
3. Delete the relevant section from .git/config
4. Run git rm --cached path_to_submodule (no trailing slash)
5. rm -rf .git/modules/path_to_submodule
6. Delete the now untracked submodule files
7. Commit changes