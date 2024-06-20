# Juji Documentation

This is the source for Juji's documentation Web site https://juji.io/docs. The site is built with [mkdocs](https://www.mkdocs.org) using the [Material](https://squidfunk.github.io/mkdocs-material/) theme.

We welcome pull requests for this repository. Follow instructions below.

## Get the code

First fork this repository: https://github.com/juji-io/docs,  so you have your own at https://github.com/yourname/docs

Then checkout to your own branch.

```bash
git clone git@github.com:yourname/docs.git
git pull
git checkout -b <yourbranchname>

```
Then edit the files under `docs` directory.

Use the following commands to commit your changes and push to your own branch on github.

```
git add docs/yourfile.md
git commit -m "your commit message"
git push --set-upstream origin <yourbranchname>

```

Then go to Github to create a new pull request for https://github.com/juji-io/docs, so that we can review your changes. Please summarize briefly what you have changed. After your changes are approved and merged. It will go live automatically. Thank you for your contribution!

## Local setup

To build the site, make sure you have python on your system. It is safer to use the same version of python as we do. There are multiple ways to ensure this. Below we show how you can set up with pyenv or conda.

### pyenv
One option is to install pyenv, and install the right version of python using it. Please follow [its instruction](https://github.com/pyenv/pyenv) to set it up. It is important to add `pyenv init` to your shell. Otherwise you may not be using the right version of python.

```bash
brew install pyenv
pyenv install 3.9
pyenv global 3.9
```

Test that you have the right version of python `python --version`.

Now install needed extensions:

```bash
pip install mkdocs
pip install mkdocs-material==<version>
```
Get mkdocs-material version from theme/base.html by searching for "mkdocs-material" in the file.

### conda
Conda is another popular option for install virtual python env. Follow [conda installation on mac](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html).
```bash
conda create -n juji-doc python=3.9
conda activate juji-doc
conda install -c conda-forge mkdocs
conda install -c conda-forge mkdocs-material=<version>
```
Get mkdocs-material version from theme/base.html by searching for "mkdocs-material" in the file.


## Assets and Links

Make sure the assets filenames and internal links use relative paths, because the site is deployed as a sub-directory of our main site.

For example, use `../img/something.png` instead of `/img/something.png`, use `../juji-studio/design` instead of `/design`.

## Test

After you edit the documents, you can test the site by starting a dev-server:

```bash
cd docs
mkdocs serve -a 0.0.0.0:8000
```

And point browser to http://localhost:8000

The dev-server also supports auto-reloading, and will rebuild your documentation whenever anything in the configuration file, documentation directory, or theme directory changes.

## Upgrade software

```bash
pip install mkdocs mkdocs-material pymdown-extensions --upgrade
```

We may need to reconcile our customization in `theme/base.html` with the installed one, e.g. at `~/.pyenv/versions/3.6.6/lib/python3.6/site-packages/material/base.html`.

Also need to change the names of the following assets files in base.html to be the same as the ones in `~/.pyenv/versions/3.6.6/lib/python3.6/site-packages/material/assets/`:

* javascripts/worker/search.*.min.js
* stylesheets/main.*.min.css
* stylesheets/palette.*.min.css
