- instantly share code, notes, and snippets
  - [**GitHubGist**](https://gist.github.com)

- check ignored files
  - `git status --ignored`

- add files to be ignored
  - [**local**](https://help.github.com/articles/ignoring-files/): `touch .gitignore` (in the git repo)
  - [**common `.gitignore` configurations**](https://gist.github.com/octocat/9257657)
  - [**global**](https://help.github.com/articles/ignoring-files/): `git config --global core.excludesfile ~/.gitignore_global` (anywhere, just open the terminal)

- error message: ```Another git process seems to be running in this repository, e.g.
  an editor opened by 'git commit'. Please make sure all processes
  are terminated then try again. If it still fails, a git process
  may have crashed in this repository earlier:
  remove the file manually to continue.```
  - `git rm -f .git/index.lock` # remove the `index.lock` file from the `.git` dir
