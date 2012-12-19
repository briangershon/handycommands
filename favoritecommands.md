# Favorite Commands

## Shell

Recursively remove directories from current directory

	find . -name .svn -exec rm -rf \{\} \;

## Git

	# list branches in date order
	git for-each-ref --sort=-committerdate refs/heads/

## Github

Creating an OAuth Token for Updating GISTs

    curl -v -u USERNAME_HERE https://api.github.com/authorizations --data '{"scopes":["gist"], "note":"DESCRIPTION_HERE"}'