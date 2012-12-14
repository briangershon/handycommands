# Favorite Commands

## Shell

Recursively remove directories from current directory

	find . -name .svn -exec rm -rf \{\} \;

## Github

Creating an OAuth Token for Updating GISTs

    curl -v -u USERNAME_HERE https://api.github.com/authorizations --data '{"scopes":["gist"], "note":"DESCRIPTION_HERE"}'