# ChainAPI Documentation

## Getting Started

Pull the docker container for the material theme - it contains all the pre-requisites for mkdocs:

```shell
docker pull squidfunk/mkdocs-material
```

## Running Locally

Run the container with this command and the docs will be built and available at `localhost:8000`. It will also auto-reload as you make changes.

```shell
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
```

## Deployments

The docs site is hosted on Github Pages in this project.

The main workflow builds the site and pushes this to the `gh-pages` branch. Github then takes over and deploys this, which can be viewed in the auto-created pages-build-deployment workflow.

### Hyperlink Checks

The main workflow also checks for any broken hyperlinks using [markdown-link-check](https://github.com/tcort/markdown-link-check) wrapped in the [related action](https://github.com/marketplace/actions/markdown-link-check).

The config file [link-config-check.json](link-check-config.json) defines a few rewrites we need to do due to the API3 docs site returning 404s instead of 302s when the `/latest/` link redirects to the latest version.

When a new version of Airnode or OIS is released, the version number should be updated in this file.

To run this locally, use this command:

```shell
find . -name \*.md -print0 | xargs -0 -n1 markdown-link-check -c link-check-config.json
```
