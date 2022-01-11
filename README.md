JSPWiki Markdown support
------------------------

Example of Markdown Parser/Renderer integration in JSPWiki. 


Prerequisites
-------------
* at least Java 8
* latest snapshot (> 2.11.1-git-02)

Demoing
-------
* download / git clone this repo and `mvn clean install` all the modules
* go inside jspwiki-markdown-war and run `mvn tomcat7:run-war`
* Markdown powered available at http://localhost:8080/jspwiki-markdown-war after a few moments
* jspwiki-markdown-pages contains a couple of sample wikipages
