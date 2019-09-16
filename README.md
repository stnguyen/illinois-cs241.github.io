# Webpage for CS 241

[![Build Status](https://travis-ci.org/illinois-cs241/illinois-cs241.github.io.svg?branch=develop)](https://travis-ci.org/illinois-cs241/illinois-cs241.github.io)
[![Depfu](https://badges.depfu.com/badges/78ebc2831869c07b5ad540abdd03b457/status.svg)](https://depfu.com)
[![Depfu](https://badges.depfu.com/badges/78ebc2831869c07b5ad540abdd03b457/overview.svg)](https://depfu.com/github/illinois-cs241/illinois-cs241.github.io?project_id=6331)

## Installing

First make sure you have ruby >= 2.4. We recommend using `rvm`

```
rvm use 2.4.5
```

After, we recommend bundler to install all the dependencies

```
sudo gem install bundler
```

Then nagivate to the root of the repostory and install

```
bundle install
```

Finally, your repository has the submodules needed

```
git submodule init
git submodule update --recursive
```

## Running

To build the site it is as simple as

```
bundle exec rake
```

If you want to build and serve a simple web server, run

```
bundle exec rake serve
```

If you want to run a spell check do

```
bundle exec rake spell_check
```

## Jekyll and Github Pages

This website is made with [Jekyll](https://jekyllrb.com/) and [Github Pages](https://help.github.com/articles/what-are-github-pages/).

Jekyll is a static site generator that allows us to write markdown instead of html and comes with [Liquid Templating](http://liquidmarkup.org/) which uses a combination of tags, objects, and filters to load dynamic content and has a nice [cheat sheet](http://cheat.markdunkley.com/).

Github Pages will host this repo not only as a code base but will also as a webserver for our website.

The magic happens in the integration. Github Pages has Jekyll integration, so if you push any changes to this repo, then Github Pages will automatically have Jekyll generate a new static site and serve it. This means that you can makes changes to the webpage simply by pushing changes to it. No more package installations, no more Angular JS, no more rsync. This also means that you can take advantage of the Github UI and edit files from a web browser.

## Structure

- `_data`: stores configurations files
  - `labs.yaml`: stores the lab info
  - `mps.yaml`: stores the mp info
  - `schedule.yaml`: stores the lecture schedule
  - `staff.yaml`: stores the staff info
  - `honors_projects.yaml`
	- `honors_schedule.yaml`
	- `malloc_hof.yaml` Winners for the malloc contest
	- `man.json` Autogenerated json file that resolves man page link
	- `staff-emeritus.yaml` Staff that have contributed greatly to the course
	- `staff-gone.yaml` All staff that have left
	- `staff.yaml` Current staff
- `_includes`: holds html that is used everywhere
  - `head.html`: holds code for including other files
  - `header.html`: top nav bar code
- `_layouts`: hold layout templates
  - `doc.html`: layout template for documentation
- `_docs`: where all the documentation is stored as markdown
- `_sass`: sass files (files named appropriately)
- `css`: holds css
- `images`: holds images
- `js`: holds javascripts
- `lib`: folder for libraries
- `static`: holds other static content, like PDFs
- `_config.yml`: global site configuration
- `_pages` Keeps stray pages
- `_coursebook` Markdown directory with all the coursebook material

## How to write documentation

### Where to create the file

All documentation is stored in `assignment-docs` repository. To make any changes, go to that repository.

### Content for this file

Once you have created this file you can add all the markdown you please. Somethings to take note of is that javascript will run to make all the areas between `h2`/`##` tags into sections and add an entry to the table of content. The title of the section and the entry of in the table of content is exactly the text that comes after your `h2`/`##`. Also `h1`/`#` is reserved for the title which will automatically be added in.

### Syntax Highlighting
You might want to add syntax highlighting.

This can be done by [fencing with triple backticks](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet/e48fe59238600be6e1ec9e4add21c513cbac86d0#code):

[A full list of languages that Jekyll supports.](https://haisum.github.io/2014/11/07/jekyll-pygments-supported-highlighters/)


