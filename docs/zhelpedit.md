# Admin links

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

[Theme documentation](https://squidfunk.github.io/mkdocs-material/reference/abbreviations/)

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.
* `mkdocs gh-deploy` - Deploy site to GitHub Pages.

## If jinja brokes

[tweet](https://twitter.com/readthedocs/status/1507388916013314048)

Just a warning to folks in the Python docs ecosystem. It looks like the latest version of jinja (which deprecated features properly) has broken the latest mkdocs & sphinx before 4.0. You can fix this by pinning `jinja2<3.1.0` in your [requirements](https://docs.readthedocs.io/en/latest/guides/reproducible-builds.html)
