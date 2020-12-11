# Juji Documentation

This is the source for Juji's documentation Web site https://juji.io/docs. The site is built with [mkdocs](https://mkdocs.org).

We welcome pull requests for this repository. Follow instructions below.

## Get the code

First fork this repository: https://github.com/juji-io/docs,  so you have your own at https://github.com/yourname/docs

Then checkout to your own branch.

```bash
git clone https://github.com/yourname/docs
git pull
git checkout -b <mybranchname>

```
Then edit the files under `docs` directory.

Use the following commands to commit your changes and push to your own branch on github.

```
git add docs/yourfile.md
git commit -m "your commit message"
git push --set-upstream origin <mybranchname>

```

Then go to Github to create new pull requests for https://github.com/juji-io/docs, so that we can review your changes. After your changes are approved and merged. It will go live automatically.

## Local setup

To build the site, make sure you have python on your system. It is safer to use the same version of python as we do. 

```bash
brew install pyenv
pyenv install 3.6.6
pyenv global 3.6.6
```

Now install needed extensions:

```bash
pip install mkdocs
pip install mkdocs-material
```

## Assets and Links

Make sure the assets filenames and internal links use relative paths, because the site is deployed as a sub-directory of our main site. 

For example, use `../img/something.png` instead of `/img/something.png`, use `../design` instead of `/design`.

## Test

After you edit the documents, you can test the site by starting a dev-server:

```bash
cd docs
mkdocs serve
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
* javascripts/bundle.*.min.js
* javascripts/vendor.*.min.js
* stylesheets/main.*.min.css
* stylesheets/palette.*.min.css

