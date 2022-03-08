# Comics

This repo contains the webpage for translation and source images of the lianhuanhua comics.

## Requirements

- [Hugo (extended)](https://gohugo.io)
- [pandoc](https://pandoc.org)

## Installation

These steps are only required once, to install the requirements on your local machine:

```bash
brew install pandoc hugo
```

## Getting the Sources

Before you can get local copy of the webpage up and running on your machine you need to clone this repo. The [hugo-book theme](https://github.com/alex-shpak/hugo-book) is installed as a submodule.

```bash
git clone --recurse-submodules --remote-submodules https://github.com/readchina/comics.git
```

If you forgot to include the submodule flags when cloning the repo run the following:

```
git submodule update --init
```

## Building

To Build a local dev version run:

```bash
hugo server -D  
```

(`-D` will also build drafts)

You should see something like this:

```bash

                   | EN   
-------------------+------
  Pages            |  57  
  Paginator pages  |   0  
  Non-page files   |   0  
  Static files     | 218  
  Processed images |   0  
  Aliases          |  11  
  Sitemaps         |   1  
  Cleaned          |   0  

Built in 150 ms
Watching for changes in /Users/hal1000/Documents/GitHub/comics/{archetypes,content,static,themes}
Watching for config changes in /Users/hal1000/Documents/GitHub/comics/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

The page is visible in your broswser at [http://localhost:1313/](http://localhost:1313/)

## Contents

As always avoid spaces in file or foldernames: ~~`zhu fu/zhu fu Version 2022.md`~~ -> `zhufu/zhufu.md`. You must stick with the project layout of this repo.

### Text

First we need to convert the original MSWord documents into markdown using pandoc.

```bash
pandoc …
```

Each comic needs to be inside a top level folder using the translated title for the comic (no spaces), e.g. `the-watch/_index.md`.
Each file is then split into:
- `_index.md` (contains the introduction)
- `A-translation-notes.md`
  - `B-cover.md`
  - `B-front.md`
  - `B-page-XX.md`
- `C-references.md`

The basic template for a translation page is

```md
# Page XX

 ![biao front](./../../../images/biao/seifert0726_biao_ZZZZ_ZZZ.jpg)

{{< columns >}}

## Source

<--->

## Translation

```

<!-- TODO location of the .md files -->

<!-- We then split the converted markdown into sections:

```bash
TODO
``` -->

### Panels

Panels go inside a folder with the comic name inside `static/images`:

```bash
static
└── images
    ├── biao
    │   ├── seifert0726_biao_0001_0.jpg
    │   ├── seifert0726_biao_0003_0.jpg
    │   ├── …
    └── niqiu
        ├── seifert0397_nqkg_0001_0.jpg
        ├── seifert0397_nqkg_0003_0.jpg
        ├── …
```

To include images in your markdown use:

```md
 ![biao cover](./../../../images/biao/seifert0726_biao_0001_0.jpg)

```

## Deployment

Deployments is fully automated on GitHub Actions. In cases where you need to debug the build, run:

```bash
hugo 
```

This will create a `public/` folder containing the compiled webpage. You should delete this folder after debugging as Hugo will not remove its contents before subsequent builds.