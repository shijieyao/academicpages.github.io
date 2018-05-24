- instantly share code, notes, and snippets
  - [**GitHubGist**](https://gist.github.com)

- check ignored files
  - `git status --ignored`

- add files to be ignored
  - [**local**](https://help.github.com/articles/ignoring-files/): `touch .gitignore` (in the git repo)
  - [**global**](https://help.github.com/articles/ignoring-files/): `git config --global core.excludesfile ~/.gitignore_global` (anywhere, just open the terminal)
  - [**common `.gitignore` configurations**](https://gist.github.com/octocat/9257657)

- commit or not `.gitignore`
  - people have [**different preferences/opinions**](https://stackoverflow.com/questions/5765645/should-you-commit-gitignore-into-the-git-repos)!

- error message: ```Another git process seems to be running in this repository, e.g.
  an editor opened by 'git commit'. Please make sure all processes
  are terminated then try again. If it still fails, a git process
  may have crashed in this repository earlier:
  remove the file manually to continue.```
  - `rm -f .git/index.lock` [**# remove the `index.lock` file from the `.git` dir`**](https://stackoverflow.com/questions/38004148/another-git-process-seems-to-be-running-in-this-repository)
