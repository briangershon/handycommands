## Shell

Recursively remove directories from current directory

	find . -name .svn -exec rm -rf \{\} \;

## General Git

List branches in date order

	git for-each-ref --sort=-committerdate refs/heads/

## Git and SVN

Create local Git Repo from SVN Branch

	# Which SVN branch do you want to create a repo for? (versus pulling down all svn branches and all history)
	svn ls https://MYREPO/branches

	# If you want history for a complete branch, find branch's first revision
	svn log --stop-on-copy https://MYREPO/branches/branch-i-want
	
	# Create a local git repo, and pull in history starting from a specific svn revision for 'branch-i-want', which is 16759 in this case
	git svn clone --log-window=10000 -r16759 https://MYREPO/branches/branch-i-want branch-i-want

Pulling from SVN and Pushing back to SVN

	# Pull down revisions
	git svn rebase

	# Push git changes back to SVN
	git svn dcommit

Working with SVN and multiple local Git branches

	# If creating/using local git branches, use "git rebase" and never "git merge"/"git pull"
	# 	since SVN doesn't understand merging, just linear commits.
	git checkout master		# assume we're on master
	git checkout -b my-new-local-branch		# create a new branch based on master
	... make changes, make some commits...
	git checkout master		# change back to master in prep for commiting back to SVN
	git rebase my-new-local-branch 	# to add commits from my-new-local-branch back to master
	git svn rebase		# to pull down any new changes in SVN


## Github API

Creating an OAuth Token for Updating GISTs

    curl -v -u USERNAME_HERE https://api.github.com/authorizations --data '{"scopes":["gist"], "note":"DESCRIPTION_HERE"}'