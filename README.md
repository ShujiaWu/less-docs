[![devDependency Status](https://david-dm.org/less/less-docs/dev-status.svg)](https://david-dm.org/less/less-docs#info=devDependencies)

# lesscss.org

> Official website and documentation for Less/Less.js

## 说明

这是我学习 Less 时从 Less Doc 的官方仓库 fork 下来的，并且对文档进行了翻译。

主要原因是在网上没有找到最新中文文档，加上我自己本身如果直接看英文文档也不是特别顺畅（英语水平差伤不起呀o(╥﹏╥)o），所以索性自己根据理解边学边翻译。

目前的进度相对比较缓慢，我会尽最大的努力把它翻译完。

由于本人的水平比较有限，翻译过程中可能出现差错，如有错误欢迎指出。

目前的安排是先将文档全部翻译完成，然后再进行校对。

## Quickstart

Assemble and Grunt are used to build the docs. To get started:

1. Download the docs
2. In the root of the project, run `npm install`
3. Run the `grunt` command to build the docs

If all worked properly, you're ready to begin contributing to the docs!

### Documentation

All documentation content can be found in the `./content` directory. Please read the **contributing** section below if you wish to add documentation.

## The Plan

1. Clean up and organize all of the documentation in the [content](./content) directory, which means
2. Consistent naming conventions for files, consistent coding styles in documents
3. Organize information and favor individual files for sections of content, rather than long documents
4. Last, a new theme.


## Contributing
### Coding Style
> Please help us make the documentation _consistent, readable, and maintainable_ by conforming to these guidelines when contributing:

#### Less, LESS or Less.js?

The name of the project is **Less**. Anywhere in the docs, **Less** means both the language and its official, reference implementation.
The **less.js** form is normally to be used only to specify either of:
* the browser script file name
* the particular GitHub [repository](https://github.com/less/less.js) (where most of the development takes place)

##### Examples:
- *"Less language", "Less library", "Less API", "Less plugin", "Using Less" etc.*
- *"Fork [less/less.js](https://github.com/less/less.js) repository"* (synonyms: *"Less Repository", "Main Repository"* etc.)
- *"Make sure to include your stylesheets before the [less.js](https://github.com/less/less.js/blob/v2.7.2/dist) script"*


#### Capitalization

##### In Titles: Do Capitalize

* Nouns (man, bus, book)
* Adjectives (angry, lovely, small)
* Verbs (run, eat, sleep)
* Adverbs (slowly, quickly, quietly)
* Pronouns (he, she, it)
* Subordinating conjunctions (as, because, that)

##### In Titles: Do Not Capitalize

* Articles: a, an, the
* Coordinating Conjunctions: and, but, or, for, nor, etc.
* Prepositions: on, at, to, from, by, etc.

#### Markdown standards

* Use `#` for titles, not underlines. Underlines are not semantic, aren't as flexible, aren't always highlighted properly in code highlighters
* Always add a space between the `#` and the heading
* Wrap inline code with a **single backtick**,
* wrap blocks of code with **three backticks** (code fences).
* With code blocks, _always use the correct language_ after the first code fence. Although GitHub does not highlight Less, our documentation is more likely to show up in GitHub's and Google's search results when the correct language is used. Examples: please use <code>\`\`\`less</code> for Less, and <code>\`\`\`css</code> for CSS.

#### Less standards

* Two spaces for indentation, never tabs, and always use proper indentation
* Multiple-line formatting (one property and value per line)
* For multiple, comma-separated selectors, place each selector on its own line
* Double quotes only, never single quotes
* Always put a space after a property's colon (e.g., `display: block;` and not `display:block;`)
* End _all_ lines with a semi-colon
* Attribute selectors, like `input[type="text"]` should always wrap the attribute's value in double quotes. This is important to do in your own code as well for consistency and safety (see this [blog post on unquoted attribute values](http://mathiasbynens.be/notes/unquoted-attribute-values) that can lead to XSS attacks)
* When using HTML in your examples, use tags and elements appropriate for an HTML5 doctype (e.g., self-closing tags with _no trailing slash_)
* Separate words in variable and mixin names using dash (e.g., `@long-variable-name` or `.my-favourite-mixin`)

Examples:

**Good**

```css
body {
  padding-top: 80px;
  font-size: 12px;
}
```

**Bad**

```css
body {
padding-top: 80px;
font-size: 12px;
}
```

**Bad**

```css
body { padding-top: 80px; font-size: 12px }
```

Also, please ensure that all documentation files should have globally-unique names, regardless of where they are located in the repository. This makes it easier to use conveniences like file globbing, and it's good practice anyway.

### Feature Requests, Bugs and Pull Requests

* If you would like to request a feature, suggest an improvement, or report a bug, please [submit an Issue](https://github.com/less/less.js/issues?state=open).
* Feature requests are more likely to get attention if you include a clearly described use case.
* If you wish to submit a pull request, please [read this first](https://github.com/less/less.js/blob/master/CONTRIBUTING.md).

## Tools

The documentation site is generated using [Assemble](http://assemble.io). Please visit that project [to report bugs](https://github.com/assemble/assemble/issues?state=open), or to learn more about usage and customization.

## Build the docs

Update the project with the most recent metadata from the Less.js project, such as current version number, description, and so on, and then run Grunt with the following command:

```bash
node data/utils/pkg && grunt
```

## License
Copyright (c) 2017, Alexis Sellier, Less Core Team, Contributors
Documentation released under [Creative Commons](./LICENSE-CC).
Documentation source code released under the [MIT License](./LICENSE-MIT).
Less source code is released under the [Apache 2 License](https://github.com/less/less.js/blob/master/LICENSE).
