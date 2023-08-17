# Contributor Information

## Creating a new repo for a course

Instructors may choose any tool they are comfortable with. For instructors new to github pages, we created a template repository containing a Hugo site and theme ready to go. To use this template, go to https://github.com/UofTDoSSEducation/STA000, click on 'Use this template', 'Create a new repository'. Then configure with in
structions in the section [Course repo settings](#Course-repo-settings).

## git workflow

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

# Repo Admin Information

Each course should have its own repository named after its course code. Once GitHub Pages is enabled for the repo, it will automatically receive a URL under the departmetn domain. For example, repo UofTDoSSEducation/STA101 will receive URL https://courses.utstat.utoronto.ca/STA101.

In GitHub Pages terminology, the repo named "uoftdosseducation.github.io" hosts https://uoftdosseducation.github.io and is mapped to https://courses.utstat.utoronto.ca. This is the organization site.

Each course repo hosts https://courses.utstat.utoronto.ca/STAxyz. This is a project site.

It is also possible to give a course website a URL like xyz.utstat.utoronto.ca. Please contact the DOSS IT team with usecase.

## Repo contributor management

Organizing collaborators into Github Teams simplifies permission management.
Create one team for each repository. Add team members by github ID.
Go to the repository > Settings > Access : Collaborators and teams. Add the newly created Team and set Role to "Maintain".

## Course repo settings

Under "General" set "Default branch" to 'main'.

To enable GitHub Pages for a repo, go to Settings > Code and automation > Pages. Set Build and deployment source to GitHub Actions. Leave Custom domain empty. Check the box for Enforce HTTPS.

Hugo site build and deployment insturctions are defined for each repo inside the directory .github/workflows. The main workflow that runs the course website is hugo.yml. There we define that the course website should run on the 'main' branch of the codebase.

To reduce the chance of new code commit breaking running site, we require all work to be pushed to a different branch and test that it can successfully build before merging to the main branch. This procedure is performed automatically with branch protection rules and an additional workflow definition.

Go to Settings > Code and automation > Branches, Add a branch protection rule. Branch name is "main". Check the boxes "Require merge queue", "Require deployments to succeed before merginging", Deployment environments found in this repository "github-pages", and "Do not allow bypassing the above settings".

The worflow that defines the work queue action is .github/workflows/hugo-mergeque.yml. This file is hugo.yml truncated up to the step of running hugo. By default Github Pages only allows deployment to the main branch, therefore the deployment step on another branch would fail anyway, and that is okay because we only need to verify that it builds. This rule is defined under Settings > Code and automation > Environments > Deployment branches.
