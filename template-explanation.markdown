---
layout: default
title: "Template Explanation"
num: 1
---

##A template for OTS workshops##
This template was created for OpenTechSchool Brussels. It is meant to ease the creation of materials for the workshop, have a brand presence, and have a coherency between materials.

This template will evolve and get more and more features as feelings of them being required grow. If you already think of something to add, be sure to drop us a message.

##How to create a course from this template##

Everything was done so that you would have to modify as less files as possible. This template uses Jekyll as a back bone. You can publish it whenever jekyll is installed. If you're making the course for OTS, think of hosting that on a github page, many workshops are already there.

First, you'll need to copy past the whole folder of this template. Then you'll only have to modify a few files (`_config.yml`, `_data/authors/yml` and `index.markdown`.) and add the ones representing your course's pages.

#####Configuration: `_config.yml`#####
In this file we descrive configuration parameteres that are on the website scale. Nothing much to be done here, you'll only need to modify two elements:  
`-` The title (the string after `title:`). Put the title you chose for your course.  
`-` The base URL (the string after `baseurl:`) Put the base URL where your website is meant to be accessed.

#####Adding authors: `_data/authors/yml`#####
In this file we add informations about the authors of the workshop. Just modify the information of the current author, and copy past it to add as many authors as you wish.  
All the authors' information is shown in the about page.

#####Welcoming page: `index.markdown`#####
This is your home page. Write there a welcoming message, description of your website, pasta cooking recipy... This is the first thing your students will see, make it nice!

#####Your pages#####
So, now the most important part, the course itself! In order to add pages, just create at the root of your website (where this file is) files with a `.markdown` extension. [Mardown](http://daringfireball.net/projects/markdown/) is a way to write future HTML files in a very straight forward manner, that one can learn in a matter of minutes.
Lucky you, you'll only have to worry about the raw content of your page. We have a layout that already add the header, footer, styling, menu on the side, and parse your files to add them to the menu and many other little details. In order to use that, you need to specify in each of your files a header:

```
---
layout: default
title: "Template Explanation"
num: 1
---
```

Alwas keep the layout by default (unless you want to create a new one). In title, you have the title of you webpage. And for num, you have the index of your page (defining the order they are presented in the menu on the side), starting with 1. Always be carefull to have them in consecutive order. If you have 5 pages and one index is 8, it won't be displayed in the menu. We're trying to find a better way to handle that, but until then, be careful! If you want, you go look the source of this file on the github repository.

If you prefere, you can also add straight `.html` files. Be sure to still keep the headers (layout, title & num).

If you're not sure how & what to write in either HTML or Markdown: we are built on Jekyll, and using redCarpet. If this doesn't help you much or if you have any issue creating your course material based, be sure to send me a message: [roman@opentechschool.org](mailto:roman@opentechschool.org).

