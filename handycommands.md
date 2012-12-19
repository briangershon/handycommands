## Shell

Recursively remove directories from current directory

	find . -name .svn -exec rm -rf \{\} \;

## Git

	# list branches in date order
	git for-each-ref --sort=-committerdate refs/heads/

## Git with SVN

	# Which SVN branch do you want to create a repo for? (versus pulling down all svn branches and all history)
	svn ls https://MYREPO/branches

	# If you want history for a complete branch, find branch's first revision
	svn log --stop-on-copy https://MYREPO/branches/branch-i-want
	
	# Create a local git repo, and pull in history starting from a specific svn revision for 'branch-i-want', which is 16759 in this case
	git svn clone --log-window=10000 -r16759 https://MYREPO/branches/branch-i-want branch-i-want

## Github

Creating an OAuth Token for Updating GISTs

    curl -v -u USERNAME_HERE https://api.github.com/authorizations --data '{"scopes":["gist"], "note":"DESCRIPTION_HERE"}'