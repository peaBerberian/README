# Documentation Files

## Overview

In this page, we're going to focus on how you will want to write your
documentation files and where to place them in your project, depending on the
wanted resulting documentation.

## Format

### CommonMark Markdown

All documentation pages you want to generate HTML pages for have to written in
the Markdown format (which generally ends with the `.md` extension), more
specifically respecting the
[CommonMark specification](https://spec.commonmark.org/0.30), which is its most
popular specified implementation.

If you're not familiar with the Markdown format, you can
[follow the CommonMark tutorial linked here](https://commonmark.org/help/tutorial/).

### About relying on plain Markdown files

Markdown files have the huge advantages of being both human-readable and
compatible to a large panel of developer-facing applications and tools. It can
also be noted than most forges (GitHub, GitLab, SourceHut, BitBucket etc.)
provide a very good support of the format natively, making it one of the
strongest format candidate for developer-oriented documentation files.

Though README generates HTML files, the source Markdown files are also intended
to be readable as is, by any of those tools, which is why we renounce at the
idea of adding any specific syntax.

Let's consider your projects' developers as an example. They probably will end
up reading much more often the source Markdown files (e.g. when re-checking some
API details in the documentation) than viewing it through its URL in a web
browser. And this can be extrapolated to some users as well.

## Content

### How much information to put in it

Each of the Markdown files you'll write will correspond to a single
documentation page once transformed by README. You should keep that in mind when
writing your documentation to get a feeling of what information to put in a file
and when another file should be created instead.

For example, this `Documentation Files` documentation page is written in a
single Markdown source page, here: TODO

As you can see, its content is just straightforward human-readable Markdown,
with [headings](https://spec.commonmark.org/0.30/#atx-headings),
[links](https://spec.commonmark.org/0.30/#links),
[code](https://spec.commonmark.org/0.30/#code-spans),
[emphasis](https://spec.commonmark.org/0.30/#emphasis-and-strong-emphasis) and
all of the other features you may be used to if you relied on Markdown before.

### Table of contents

You may have noticed that there is a table of contents in the right-side of this
page.

This table of content is automatically generated by README by relying on
"headings" (those either defined by `#` characters or
[setext headings](https://spec.commonmark.org/0.30/#setext-headings)) declared
in your documentation files.

Levels 1 (a single `#` or a `=====`-style setext heading), 2 (2 `#` characters
or `-----`-style setext heading) and 3 (3 `#` characters) are all considered to
generate it. For example this page has `Documentation Files` as its only level 1
headers, multiple level 2 headers such as `Overview` and `Format`, and multiple
level 3 headers such as `CommonMark Markdown` and `Code blocks`.

### Embedded HTML

As permitted by the CommonMark specification, you can embed HTML in your
documentation pages to have close to endless ways of expressing a layout. For
example:

```html
<p style="text-align: center; border: 1px dashed #444">
  Some <i>embedded HTML</i> block
</p>
```

Will render as:

<p style="text-align: center; border: 1px dashed #444">
    Some <i>embedded HTML</i> block
</p>

The treatment of HTML follows the exact rules of the
[CommonMark specification on HTML blocks](https://spec.commonmark.org/0.30/#html-blocks)
so you should rest assured that most other tools (e.g. GitLab, GitHub, Prettier,
editor extensions...) should have no problem handling them.

Still, keep in mind that embedded raw HTML blocks are harder to read when the
original markdown is viewed than the simpler Markdown syntax.

### Code blocks

Again, code blocks syntax just follows here the CommonMark specification. You
may already be used to using backticks (\`) for
["code spans"](https://spec.commonmark.org/0.30/#code-span) and triple backticks
for ["code fences"](https://spec.commonmark.org/0.30/#fenced-code-blocks).

For example: "\`this\`" will be transformed into "`this`", and that multiline
code:

<p style="margin-left: 20px">
```<br>
function print() {<br>
    console.log("Hello world!");<br>
}<br>
```
</p>

Will be transformed into:

```
function print() {
    console.log("Hello world!");
}
```

README also includes a syntax highlighter,
[highlight.js](https://highlightjs.org/), which will automatically hightlight
your code based on the language you associated to your code fence.

For example _(notice the `js` mention, which can also be written as `javascript`
by the way)_:

<p style="margin-left: 20px">
```js<br>
function print() {<br>
    console.log("Hello world!");<br>
}<br>
```
</p>

Will be transformed into:

```js
function print() {
  console.log("Hello world!");
}
```

### Links to other markdown files

You can add a link to another Markdown file in your documentation pages in which
case the link will be automatically translated to a link to the corresponding
documentation page in the HTML output.

For example:

```md
Here's a [link to the configuration page](./Configuration.md).
```

Will be translated to:

> Here's a [link to the configuration page](./Configuration.md).

Note: If a linked relative Markdown file is not found by README, it will output
a warning at the [Run step](./Run.md). This allows to make sure that you wrote
your links between documentation pages correctly.

### Link anchors

You can also directly link to a heading (from level 1 to 3), by adding its name
in the URL's fragment (after a `#` character).

To be compatible with URL fragments, the header names are actually updated in a
simple way:

1. All spaces at the beginning or end of the title are removed.

2. Remaining spaces are replaced by a dash (`-`).

3. Every characters not part of any of those sets:

   - Upper-case latin letters from A to Z
   - Lower-case latin letters from a to z
   - dashes (`-`)
   - underscores (`_`)

   Will be removed when put as an anchor.

4. All remaining upper-case aphabetical characters (A to Z), is transformed to a
   lower-case character (a to z).

As such, if you want to link to the `Code blocks` chapter of this page, you can
link to it like this: `[link](#code-blocks)` (we replaced the space by a dash
character and set the title in lower case). Here's the result for this example:
[link](#code-blocks)

To select a more complex example, to link an heading like this:
`##    Bonne année à tous  `, you would write something like
`[some link](#bonne-anne--tous)` (The ending space is removed, the middle spaces
replaced by dashes, the `B` is transformed into lower-case `b` and both the `é`
an `à` are removed).

For most use-cases (and at least for english headings), doing anchor generation
this way is generally compatible to how tools like GitHub and GitLab also
generate their headings, leading to anchor links in Markdown files that are
still functional in those tools.

Duplicated headings in the same page should be avoided. If README see two
conflicting anchors, it will add a numerical postfix starting with the second
one encountered. If such scenarios is unavoidable, you may prefer to generate
the documentation pages once to check the resulting anchor names before linking
to it.

Last but not least it is perfectly possible to link to an anchor in another
Markdown page. As such, `[example](../Home.md#installation)` will directly jump
to the `Installation` chapter of the `Home.html` page:
[example](../Home.md#installation).

### Image, audio and video

When linking to a media resource, either through
[Markdown syntax's for images](https://spec.commonmark.org/0.30/#images) or
through embedded HTML elements, README will automatically copy the resouce so it
is also accessible from the output directory.

For example, I can insert an image by writing something like
`![README logo](../../assets/img/logo.png "README")`, which will copy the image
so it is visible in the HTML page.

Likewise, media elements like `<video src="../../assets/video/my_video.mp4" />`
can be embedded in you markdown as HTML. The resource will also be copied by
README into the output directory.

README only copies local resources. You can also refer to online resources in
your markdown files, in which case the resulting HTML will also refer to those
same online resources without copying them locally.

## File and directories location

The location of the various directories containing documentation pages is
important, as the file architecture will be reused by README to organize the
generated HTML pages.

All documentation pages should be put in a common root directory in your
project. To take an example, let's say that our root directory is `./doc` (from
the root of our project).

In that root directory, you want to put subdirectories corresponding to the
"Categories" you'll have. Categories are subsets of your documentations which
you do not want to group together (for example in this documentation, categories
are "Getting Started" and "API"). You do not need to name the directory the same
way you want the category to be called in the resulting HTML documentation, this
"display name" will be configurable in
[the Configuration step](./Configuration.md).

Inside that second level of directories (the "Category" ones), you can either
put directly your Markdown documentation pages, or directories themselves
containing Markdown documentation pages if you want to create multiple linked
pages in a "page groups" (in the documentation you're reading right now the
"Step by step guide" is a page group for example). Once again, the name of those
files and directories aren't important as the name used for display in links
will be configured elsewhere.

Likewise, the order in which those files may be listed (alphabetically or
otherwise) is unimportant. You'll set-up configuration files in the next steps
setting a clear ordering of those pages.

Thus, taking in example the README documentation you're reading right now,
here's how files have been organized (may be out-of-date):

```
doc                                  # Root directory
│
├── .docConfig.json                  # Global configuration (we'll see that later)
│
├── Getting_Started                  # "Getting Started" Category
│   ├── .docConfig.json              # Local configuration (we'll see that later)
│   ├── Steps                        # Page group
│   │   ├── .docConfig.json          # Local configuration
│   │   ├── Configuration.md
│   │   ├── Documentation_Files.md   # The page you're reading right now
│   │   ├── Page_Ordering.md
│   │   ├── Run.md
│   │   └── Serve.md
│   ├── Home.md                      # The "README Overview" previous page
│   └── HTML_Page_features.md
│
└── API                              # Another Category, "API"
    ├── .docConfig.json              # Local configuration
    ├── CLI.md
    └── ...
```