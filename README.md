# Juji Documentation

This is the source for Juji's documentation Web site https://docs.juji.io. The site is built with [mkdocs](https://mkdocs.org).

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

You should have cloned the repo for the built site at
`git@github.com:juji-io/juji-io.github.io.git`, so that you should have the following file structure:

```
docs/
    mkdocs.yml
    docs/
juji-io.github.io/
```
Now do the following to deploy the site:

```bash
cd ../juji-io.github.io/
mkdocs gh-deploy --config-file ../docs/mkdocs.yml --remote-branch master
```

## Upgrade software

```bash
pip install mkdocs mkdocs-material pymdown-extensions --upgrade
```

We may need to reconcile our customization in `theme/base.html` with the installed one, e.g. at `~/.pyenv/versions/3.6.6/lib/python3.6/site-packages/material/base.html`. Also need to change the names of the assets files to be the same as the built ones using `mkdocs build`.

