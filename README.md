# docs

This is the source for Web site https://docs.juji.io. The site is built with mkdocs.

## Setup

```bash
pip install mkdocs
```

You should have also cloned the repo for the built site at git@github.com:juji-io/juji-io.github.io.git
So you should have the following file structure:

```
docs/
    mkdocs.yml
    docs/
juji-io.github.io/
```

## Test 

```bash
cd docs
mkdocs serve
```

And point browser to http://localhost:8000

The dev-server also supports auto-reloading, and will rebuild your documentation whenever anything in the configuration file, documentation directory, or theme directory changes.

## Deploy 

```bash
cd ../juji-io.github.io/
mkdocs gh-deploy --config-file ../docs/mkdocs.yml --remote-branch master
```
