# CMS, sort of

Well, this isn't a CMS actually, it's just a tiny wrapper around [discount][] [markdown][] converter.

This tiny tool can be handy if you want to convert a bunch of [markdown][] files into html pages and (optionally) automatically create an index file for them. As it supports templates, quite pleasing results can be achieved, so it can be used to manage a small static website.

## Usage

	pmcms ACTION | filename.md
	
	Actions supported:
	
	- all: process all .md files (but not index)
	- index: create index file (list appended to index.head)
	- clean: remove ALL .html files (be careful!)
	- gc: collect garbage (remove .html files with no
	  corresponding .md files)
	
	DOCROOT environment variable is looked for files, otherwise,
	PWD is used

Markdown files can have optional [pandoc-style title block][pandoc-title] (headers containing metadata):

	% title
	% author
	% date

Any field may be left blank. These fields can be used in html template, refer to example file.

Extra features:

- [markdown][] files should have `.md` suffix;
- path to [markdown][] files looked up from `DOCROOT` envoronment variable, if unset, current workdir is used;
- generic template is called `template.tpl`, but each page can use its own one, just call it as your page with `.tpl` suffix instead of `.md`;
- automatically updates files on `all` target if template's changed;
- autoindex feature appends index to `index.head` file, if it exists.

## Usage examples

Create html pages from existing [markdown][] files:

	pmcms all

Clear all html files:

	pmcms clean

Automatically create `index.md` file and update/create html pages:

	pmcms index && pmcms all

Remove old html files if you already removed its [markdown][] sources:

	pmcms gc

* * *

This tool is provided 'as-is'. I do not intend to transform it into something complex or feature-rich. If you want something similar with more bells and whistles, look at [nikola][] or something similar.


[discount]: http://www.pell.portland.or.us/~orc/Code/discount/
[markdown]: http://daringfireball.net/projects/markdown/
[pandoc-title]: http://johnmacfarlane.net/pandoc/README.html#title-block
[nikola]: http://nikola.ralsina.com.ar
