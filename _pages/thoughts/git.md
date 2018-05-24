- check ignored files
  - `git status --ignored`
  
- error message: ```Another git process seems to be running in this repository, e.g.
  an editor opened by 'git commit'. Please make sure all processes
  are terminated then try again. If it still fails, a git process
  may have crashed in this repository earlier:
  remove the file manually to continue.```
  - `git rm -f .git/index.lock` # remove the `index.lock` file from the `.git` dir
