JSPWiki Markdown support
------------------------

Markdown Parser/Renderer for JSPWiki, based on Flexmark + a custom JSPWiki extension. 

Currently it supports:
* Normal Markdown
* Wiki links (internal, external, interwiki, edit, etc.)
* Variables
* Almost all plugins (more on this below)
* Inline images
* Footnotes
* ACLs
* Metadata
* WYSIWYG edition

Prerequisites
-------------
* at least Java 7
* latest snapshot (> 2.10.3-git-42)

Installation
------------
* download / git clone this repo and `mvn clean install` jspwiki-markdown module
* add the jspwiki-markdown as a dependency to jspwiki-war so the resulting war contains all the needed dependencies 
* add / change to your jspwiki*-properties file the following lines
```
jspwiki.renderingManager.markupParser=org.apache.wiki.parser.markdown.MarkdownParser
jspwiki.renderingManager.renderer=org.apache.wiki.render.markdown.MarkdownRenderer
jspwiki.renderingManager.renderer.wysiwyg=org.apache.wiki.render.markdown.MarkdownRenderer
```
* compile your customized JSPWiki war and you're done!

Demoing
-------
* download / git clone this repo and `mvn clean install` all the modules
* go inside jspwiki-markdown-war and run `mvn tomcat7:run-war`
* Markdown powered available at http://localhost:8080/jspwiki-markdown-war after a few moments
* jspwiki-markdown-pages contains a couple of sample wikipages

Gotchas / Yet to be done
------------------------
* Plain editor toolbar support
* Initial set of WikiPages for markdown / markup migration tool?
* %%css constructs. A new extension for this should be made, there is no support for this.
* plugins implementing HeadingListener (that is, TableOfContents) are not supported
** this interface is fired by `JSPWikiMarkupParser` every time it finds a header (more precisely, for every heading, JSPWikiMarkupParser generates a "#" link
with the section reference and then registers a HeadingListener).
** The way flexmarks parses and renders markdown, doesn't allow to generate the TOC this way. 
** Right now, TableOfContents plugin is translated to flexmark's own TOC extension, surrounded with some divs.
** There are two proper ways of adding support for this:
*** add enough css so that both html render more or less the same. Parameters parsing should be implemented anyways.
*** add a new Flexmark extension for TOC, probably forking+adapting the existing TOC extension.
* jspwiki-markdown-war contains caching turned off. If turned on, on WYSIWYG editors, whole page is rendered, including plugins, variable names, etc. I suspect this has to do more with JSPWiki itself, caching too early, but still have to get a good look at it
* thorough end-to-end testing