# Github

Creating OAuth tokens

    curl -v -u USERNAME_HERE https://api.github.com/authorizations --data '{"scopes":["gist"], "note":"DESCRIPTION_HERE"}'