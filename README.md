# Exonum Documentation

[![Build status][travis-image]][travis-url]
[![Generator][generator-image]][generator-url]
[![Gitter][gitter-image]][gitter-url]

[travis-image]: https://img.shields.io/travis/exonum/exonum-doc.svg?style=flat-square
[travis-url]: https://travis-ci.org/exonum/exonum-doc
[generator-image]: https://img.shields.io/badge/generator-mkdocs-blue.svg?style=flat-square
[generator-url]: http://www.mkdocs.org/
[gitter-image]: https://img.shields.io/gitter/room/exonum/exonum-doc.svg?style=flat-square
[gitter-url]: https://gitter.im/exonum/exonum

This is the documentation repo for the Exonum platform. It contains source files
used to build the documentation displayed on the [Exonum
website](https://exonum.com/doc/).

The Exonum documentation is written in [Markdown](https://en.wikipedia.org/wiki/Markdown),
and uses [mkdocs](http://www.mkdocs.org/) to generate HTML from sources.
You can read about Markdown [here](https://guides.github.com/features/mastering-markdown/)
or [other](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
[places](http://www.mkdocs.org/user-guide/writing-your-docs/).

Code examples are included from source using 
[`mkdocs-codeinclude-plugin`][codeinclude-plugin] to ensure they are
always up-to-date and correct.

<!-- todo: Replace the link to our fork with the upstream link once our PRs
       are integrated: https://github.com/rnorth/mkdocs-codeinclude-plugin/pulls -->
[codeinclude-plugin]: https://github.com/exonum/mkdocs-codeinclude-plugin/tree/develop#usage 

## Contributing

In order to contribute, fork this repository, make some changes, and then submit
them as a pull request. Simple! Note that the repository uses
[`master` / `develop` branching][git-branching] to allow for continuous deployment
on the exonum.com website.

Notice that the repository uses a set of [linters][wiki:lint] to check possible
problems with the contributed documents:

- [markdownlint][mdl] is used to lint Markdown files. Please see
  [the rules list][mdl-rules] to fix possible problems with this linter
- [html5validator][html5validator] is used for checking problems with the
  generated HTML pages
- [linkchecker][linkchecker] is used to find missing links
- [cspell][cspell] is used for spellchecking

You can set up these tools locally (see the `install` step in [the Travis config](.travis.yml)
for more details) and run them using the `./misc/lint.sh` script with `md`, `html`,
`links`, `cspell`, or `all` arguments.

### Page Meta

During the build process, `mkdocs` gathers meta information for each page, which
is then used to provide page summary on social media, for search engines, etc.
The main meta information of interest is the page description. By default,
it is equal to the first paragraph of the page. You can override this default
by providing an explicit description on the very top of the page
with a front matter formatting:

```markdown
---
description: 1-3 sentence description of the page
---
# Page Title

Page contents...
```

Similarly, you can redefine the displayed page title by providing a `title` property
in the front matter. The site-wide “Exonum Documentation” suffix will be added
automatically.

**Note.** Although it looks like YAML front matter in [Jekyll][jekyll]
and some other static site generators, `mkdocs` actually uses [a simpler parser][mkdocs-meta]
for the front matter. Be advised for possible discrepancies.

## Build Instructions

It is a good idea to preview your changes locally before sending a pull request. 

### Requirements

To build the docs you need installed:
- [Python](http://python.org/) version 3.7+
- [python-pip](https://pip.readthedocs.io/en/stable/installing/)
- Node version 10+ (actually verified on v10.16.0 and v12)

### Installation

Fetch and initialize the repository:

```
git clone https://github.com/exonum/exonum-doc
cd exonum-doc
git submodule update --init --recursive
```

If you build the docs locally it is recommended to use
python virtual environment:
```
python3 -m venv .env
source .env/bin/activate
```

Then, install the `mkdocs` theme together with its dependencies:

<!-- Remove 3rd-party in ECR-4265 -->
```
pip install -r requirements.txt --src 3rd-party
```

You may use [`requirements.lock`](requirements.lock) instead of [`requirements.txt`](requirements.txt)
in order to get repeatable builds.

To install linters, use

```
pip install -r dev-requirements.txt
```

`markdownlint` and `cspell` need to be installed separately. Both these tools
utilize Npm package manager, so you can install them using

```
npm install
```

### Viewing Documents Locally

In order to run a local web server serving docs, use:

```
mkdocs serve
```

The web server will be available on [127.0.0.1:8000](http://127.0.0.1:8000/).

To generate HTML files from the Markdown source files, use:

```
mkdocs build
```

The generated pages will be available in the **site/** directory.

### Build versioned documentation

To generate versioned HTML files from the Markdown source files, use:
```
node run versioned
```
The generated folders will be available in the **version/** directory. It will contain folders named with its versions.
Folder of the latest version will be named `latest`.

## License

Copyright 2020, Exonum Team

The Exonum documentation is licensed under the Creative Commons Non-Commercial
Share-Alike International License (version 4.0). Code samples are licensed
under the Apache License (version 2.0).
See [LICENSE](LICENSE) and [LICENSE-CODE](LICENSE-CODE) for details.

[wiki:lint]: https://en.wikipedia.org/wiki/Lint_(software)
[mdl]: https://github.com/DavidAnson/markdownlint
[mdl-rules]: https://github.com/DavidAnson/markdownlint/blob/master/doc/Rules.md
[html5validator]: https://github.com/svenkreiss/html5validator
[linkchecker]: https://github.com/wummel/linkchecker
[mkdocs-meta]: https://python-markdown.github.io/extensions/meta_data/
[jekyll]: http://jekyllrb.com/
[git-branching]: http://nvie.com/posts/a-successful-git-branching-model/
[cspell]: https://github.com/Jason3S/cspell
