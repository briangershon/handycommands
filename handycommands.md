## Shell

Recursively remove directories from current directory

	find . -name .svn -exec rm -rf \{\} \;

## Mirroring a website

	brew install wget

	# mirror a site locally
	wget --mirror --page-requisites --wait 2 --adjust-extension --convert-links https://www.example.com

	# just get items under a specific section using --no-parent
	wget --mirror --page-requisites --no-parent --wait 2 --adjust-extension --convert-links https://www.example.com/section

## Convert a mirrored website to PDF

	brew install htmldoc

	# create pdf in filename alphabetical order (ok since hyperlinks work in PDF)
	htmldoc --webpage -f example.pdf example_path/*.html

	# move a page to the first instead of default alphabetical order
	htmldoc --webpage -f example.pdf example_path/first-page.html example_path/*.html

## General Git

List branches in date order

	git for-each-ref --sort=-committerdate refs/heads/

Moving patches between separate Git repos

	# generate one patch file for n commits
	#	SHA1 is the commit before the first commit you want
	#	SHA2 is the last commit you want
	git format-patch SHA1..SHA2 --stdout > my-changes.patch

	# copy patch to /path/to/2

	# now apply patches
	git apply --stat my-changes.patch 		# check stats
	git apply --check my-changes.patch 		# verify patch will go in cleanly
	git am --signoff < my-changes.patch 	# add n commits

## Git and SVN

Create local Git Repo from SVN Branch

	# Which SVN branch do you want to create a repo for?
	# (versus pulling down all svn branches and all history)
	svn ls https://MYREPO/branches

	# If you want history for a complete branch, find branch's first revision
	svn log --stop-on-copy https://MYREPO/branches/branch-i-want
	
	# Create a local git repo, and pull in history starting from a specific
	# svn revision for 'branch-i-want', which is 16759 in this case:
	git svn clone --log-window=10000 -r16759 https://MYREPO/branches/branch-i-want

	# Make sure you set your committer name and email to new repo if differs
	# from your global settings
	git config user.email "me@here.com"

Pulling from SVN and Pushing back to SVN

	# Pull down revisions
	git svn rebase

	# Push git changes back to SVN
	git svn dcommit

Working with SVN and multiple local Git branches

If creating/using local git branches, use "git rebase" and never "git fetch/merge"
nor "git pull" since SVN doesn't understand merging, just linear commits.

	git checkout master		# assume we're on master
	git checkout -b my-new-local-branch		# create a new branch based on master
	... make changes, make some commits...
	git checkout master		# change back to master in prep for commiting back to SVN
	git rebase my-new-local-branch 	# to add commits from my-new-local-branch back to master
	git svn rebase		# to pull down any new changes in SVN
	git svn dcommit		# commit git changes back to SVN

## Github API

Creating an OAuth Token for Updating GISTs

    curl -v -u USERNAME_HERE https://api.github.com/authorizations \
    	--data '{"scopes":["gist"], "note":"DESCRIPTION_HERE"}'

## sed

Add a newline in the replacement text on OSX (and Linux)

	# Note: I'm using the pipe deliminiter in this example, not required.
	# Important part is defining nl, and then using it via: \\$nl\

	nl=$'\n'; sed "s|oneline|oneline\\$nl\twolines|" file.txt

Make changes in-place

	# use -i ''
	sed -i '' "s|oneline|oneline2|" file.txt

