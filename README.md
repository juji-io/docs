# Juji Documentation

This is the source for Juji's documentation Web site https://docs.juji.io. The site is built with [mkdocs](https://mkdocs.org).

We welcome pull requests for this repository.

## Setup

Make sure you have python on your system. Now install needed extensions:

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

Only Juji staff can deploy the site at https://docs.juji.io

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
