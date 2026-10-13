# Juji Documentation

This is the source for Juji's documentation Web site https://juji.io/docs. The site is built with [mkdocs](https://www.mkdocs.org) using the [Material](https://squidfunk.github.io/mkdocs-material/) theme.

## Deploy on Netlify at juji.io/docs/

Deploy this repository as a separate Netlify project in the same team as the
main [juji-io/site](https://github.com/juji-io/site) project. The main site proxies
`/docs/` to the documentation project, so documentation updates deploy independently.
No DNS change is needed.

1. Commit and push this repository's Netlify configuration and dependency file.
2. In Netlify, import `juji-io/docs` from GitHub. Use `master` as the production
   branch and leave the base directory at the repository root. The checked-in
   `netlify.toml` sets Python 3.11, the build command `mkdocs build`, and the
   publish directory `site`. Netlify installs `requirements.txt` automatically.
3. Name the documentation project `juji-docs`, if available. Verify its successful
   deployment at `https://juji-docs.netlify.app/`, including a nested page, images,
   and search. If Netlify assigns a different project name, use its actual
   `.netlify.app` address in the main site's proxy rule below.
4. In the **main site's** `netlify.toml`, add these rules before any catch-all
   redirects, retaining its existing configuration:

   ```toml
   [[redirects]]
     from = "/docs/*"
     to = "https://juji-docs.netlify.app/:splat"
     status = 200
     force = true
   ```

   Also add `netlify/edge-functions/docs-trailing-slash.js` in the main site:

   ```javascript
   export default function (request) {
     const url = new URL(request.url);
     const path = url.pathname;
     const isDocsPath = path === "/docs" || path.startsWith("/docs/");
     const isPage = !path.endsWith("/") && !path.split("/").pop().includes(".");
     if (isDocsPath && isPage) {
       url.pathname += "/";
       return Response.redirect(url, 301);
     }
   }

   export const config = {
     path: ["/docs", "/docs/*"],
   };
   ```

   This adds trailing slashes to extensionless documentation page URLs, preserving
   query parameters and the base path for MkDocs relative assets. File URLs pass through.
   Netlify's ordinary redirect rules treat `/docs` and `/docs/` as the same path,
   so a `/docs` to `/docs/` redirect rule creates an infinite redirect loop.
   See [Netlify's trailing-slash behavior](https://docs.netlify.com/manage/routing/redirects/redirect-options/#trailing-slash)
   and [edge function declarations](https://docs.netlify.com/build/edge-functions/declarations/).

5. After the documentation project is live, commit and push the main site's
   routing change. Its automatic deploy enables `https://juji.io/docs/`.
   Check `/docs`, `/docs/`, `/docs/tutorial/`, and `/docs/juji-studio/design/`,
   including navigation, images, and search. `/docs` should redirect to `/docs/`;
   page navigation should stay under `juji.io/docs/`.
   Also check that `/docs/tutorial` and `/docs/juji-studio/design` redirect to
   their trailing-slash URLs, so older links load the correct styles and scripts.

Keep `site_url` set to `https://juji.io/docs/`. Do not redirect the documentation
project's `.netlify.app` address back to `juji.io/docs/`, because the main site
uses it as the proxy origin. Unknown documentation paths should return 404;
do not add a single-page-app fallback to `index.html`.

See Netlify's [proxy documentation](https://docs.netlify.com/manage/routing/redirects/rewrites-proxies/)
and [Python dependency setup](https://docs.netlify.com/build/configure-builds/manage-dependencies/#python).

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
pyenv install 3.11
pyenv global 3.11
```

Test that you have the right version of python `python --version`.

Now install needed extensions:

```bash
pip install -r requirements.txt
```
The dependency versions in `requirements.txt` match the customized Material 7.1.0 theme.

### conda
Conda is another popular option for install virtual python env. Follow [conda installation on mac](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html).
```bash
conda create -n juji-doc python=3.11
conda activate juji-doc
pip install -r requirements.txt
```
Install from `requirements.txt` to use the same dependency versions as Netlify.


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
