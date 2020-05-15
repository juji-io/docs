# Juji Documentation

This is the source for Juji's documentation Web site https://juji.io/docs. The site is built with [mkdocs](https://mkdocs.org).

We welcome pull requests for this repository.

## Setup

Make sure you have python on your system. It is safer to use the same version of python as we do. 

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

## Test

After you edit the documents, you can test the site by starting a dev-server:

```bash
cd docs
mkdocs serve
```

And point browser to http://localhost:8000

The dev-server also supports auto-reloading, and will rebuild your documentation whenever anything in the configuration file, documentation directory, or theme directory changes.


## Deploy

The site is automatically deployed when master branch is pushed to github.

## Upgrade software

```bash
pip install mkdocs mkdocs-material pymdown-extensions --upgrade
```

We may need to reconcile our customization in `theme/base.html` with the installed one, e.g. at `~/.pyenv/versions/3.6.6/lib/python3.6/site-packages/material/base.html`. 

Also need to change the names of the assets files in `assets/javascripts` and `assets/stylesheets` in base.html to be the same as the ones in `~/.pyenv/versions/3.6.6/lib/python3.6/site-packages/material/assets/`.

