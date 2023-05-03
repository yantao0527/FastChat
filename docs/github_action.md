# Github Actions

## Publish and Release

When starting a new Python project on GitHub, it's a good practice to follow a version management policy that adheres to semantic versioning, is automated, and makes it easy to maintain and understand the project's release history. One of the widely adopted version management policies for Python projects is using setuptools_scm with semantic versioning and Git tags.

To keep version management simple, we still use static version in `pyproject.toml` to release the formal version manually. We use auto release to release the dev version that get from setuptools_scm.

## Set up secrets

1. Store your PyPI API token as a secret in your GitHub repository. Go to your repository's "Settings" tab, click on "Secrets and variables → Actions" in the left menu, and then click the "New repository secret" button. Create a new secret named `PYPI_API_TOKEN` and paste your PyPI API token as the value.
2. Go to your GitHub account settings, go to "Developer settings → Personal access tokens → Tokens(classic)" , and click "Generate new token". The token needs to have the repo scopes but doesn’t need any of the others. Then go to the project’s GitHub Actions secrets and create a new secret named `PERSONAL_ACCESS_TOKEN` with the value of the token you just generated.

## User guid

**Manual Release**

To trigger the workflow `manual_release.yml` manually:

1. Check version, like `version = "0.0.12"`, in pyproject.toml.
2. Go to the "Actions" tab in your GitHub repository.
3. Select the "Manual Release" workflow from the list of workflows.
4. Click the "Run workflow" button.
5. Choose the branch you want to run the workflow on.
6. Click the "Run workflow" button to start the workflow.

GitHub Actions will run the workflow, create a new release with the specified version, and publish it to PyPI.

**Auto Release**

The workflow `auto_release.yml` was created to automatically create a new release when a pull request with the label 'release' is merged into the main branch. Auto release doesn't publish package to PyPI.

## Git tags

Use semantic versioning for Git tags. For example when you manual release `0.0.12` it creates Git tag `v0.0.12`. Then pull request with label 'release' trigger auto release to create Git tag `v0.0.13.dev16`. I recommend that the next formal version is set `0.0.14`. 

It can't work! Why?

## Roadmap

- [ ] Enhance to diplay tag name on title of workflow log when running `Manual Release`.
- [ ] Research dynamic version in pyproject.toml 
- [ ] Add test workflow

