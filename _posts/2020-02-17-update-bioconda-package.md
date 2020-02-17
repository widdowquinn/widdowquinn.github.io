---
title: "Updating a package on bioconda"
categories: Coding
tags: [python, conda, bioconda, packaging, github]
toc: true
toc_label: "Table of Contents"
toc_icon: "book-reader"
---

- Suppose:
    - You have a package that has already been released on `bioconda`
    - You have implemented a bugfix or other update and pushed to `master` (or equivalent branch) in the `GitHub` repository
    - You have tagged the update as a `Release` on `GitHub` (and, optionally, obtained a DOI using `Zenodo`)

## Read this first: `bioconda-bot` will update your package automatically 

In most cases, you will not need to act. The `bioconda-bot` [webpage](https://bioconda.github.io/developer/_autosummary/bioconda_utils.bot.html#) will detect your new version release, and package it up accordingly.
{: .notice--info}

You will receive an email from `notifications@github.com` in the name of `Bioconda Bot`, which will provide details of the pull request it has already created on your behalf.
{: .notice--info}

The kind people who maintain `bioconda` will review the changes and merge when the required standards are met.
{: .notice--info}

## Manually updating your package

- See also:
    - [Initial local setup of `bioconda`](https://bioconda.github.io/contributor/setup.html)

### 1: Fork `bioconda-recipes` to your `GitHub` account

Create or update an existing fork of the `bioconda-recipes` repository on `GitHub` in your account
{: .notice--primary}

- Click [here](https://github.com/bioconda/bioconda-recipes/fork) to create the fork

### 2: Get a current local fork of `bioconda-recipes`

Clone, or update your local copy of *your fork* of `bioconda-recipes` repository.
{: .notice--primary}

```bash
git clone git@github.com:<YOUR_GITHUB_USERNAME>/bioconda-recipes.git
```

### 3: Set the upstream remote

Go into the repository and set the upstream remote to be the official `bioconda` repository:
{: .notice--primary}

```bash
cd bioconda-recipes
git remote add upstream https://github.com/bioconda/bioconda-recipes.git
```

### 4: Symc local and remote repositories

Make sure the local fork is up to date with the remote repositories
{: .notice--primary}

```bash
git checkout master          # change to master branch
git pull upstream master     # get changes from official repository
git push origin master       # push changes to your fork
```

### 5: Create and checkout a new branch for this package update

Name the branch `update_<package>` where `<package>` is the package name.
{: .notice--info}

```bash
git checkout -b update_<package>
```

### 6: Edit your package recipe to point to the new release

Change to the package recipe directory and edit with your preferred editor.
{: .notice--primary}

```bash
cd recipes/<package>
```

- Edit the `meta.yaml` file to update elements for the new version of the package.
    - Update the version variable:
        - `{% raw %}{% set version = "<NEW_VERSION>" %}{% endraw %}`
        - Updating the version variable *should* mean that the `source:` `url:` is updated automatically (so long as the versions correspond to our standard version naming scheme)
    - Update the hash:
        - `sha256: <HASH>`
        - To get the `sha256` hash on macOS, use `shasum -a 256 <PATH_TO_FILE>` on the `.tar.gz` file downloaded from the `GitHub` release.
    - If this is not the first `meta.yaml` file you've edited for this release, increment the `build:` `number:` value by one.
    - If necessary, update `requirements:` `host:` to add or remove the necessary packages (one per line)

### 7: Push your modified files to your own fork

Change to the `recipes` directory and add your modified files
{: .notice-primary}

```bash
cd ..
git add <package>
```

- Push to your fork

```bash
git push
```

### 8: Create a pull request from your fork

Go to your `GitHub` repo at `https://github.com/<YOUR_GITHUB_USERNAME>/bioconda-recipes`
{: .notice--primary}

- Change to the branch you just created
- Click on the corresponding Pull Request button, and follow the online instructions
- Go to the [official repository's Pull Requests page](https://github.com/bioconda/bioconda-recipes/pulls) and locate your PR.
    - When this goes green (gets a green tick) the tests have been passed. If there is a red cross, more attention is needed to the update.
    - If the tests have been passed, open your pull request and select a reviewer. If they approve your changes, the PR will be merged, and the new package version will be available.

### 9: **Only after merging:** delete your branch

Checkout the `master` branch, then delete the `update_<package>` branch locally.
{: .notice--primary}

```bash
git checkout master
git branch -d update_<package>
```

    - Delete the `update_<package>` branch on the remote repository
    - Sync your fork to the remote master, and update your fork on `GitHub`:

```bash
git checkout master
git pull upstream master
git push origin master
```

### 10: Congratulations, you're done!

But have you updated `pypi` yet?
{: .notice--danger}