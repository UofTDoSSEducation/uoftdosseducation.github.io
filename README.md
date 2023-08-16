## Contributor workflow

The course repositories are set up to validate successful site build before allowing code changes to be merged into the 'main' branch. Therefore contributors must create a different branch for their work. People often name branches after the features or issues they work on. A typical workflow looks like this

```
# Sychronize with upstream before start working locally.

git checkout main
git pull

# Create and checkout a new branch called "content-edit".

git checkout -b content-edit

# Work on the codebase, run "Hugo" or "Hugo serve" to verify changes, then commit changes.

git add .
git status
git commit -m "<some commit message>"

# Push changes to a new upstream branch with the same name

git push origin content-edit
```

The push output should display a link "Create a pull request for 'content-edit' on GitHub by visiting:". Follow the link to create pull request,then click on 'Merge when ready'. If build test passes then changes will be merged to the github main branch. Go back to the local repository and pull to synch the local repo again, then delete the working branch.

```
git checkout main
git pull
git branch -d content-edit
```
