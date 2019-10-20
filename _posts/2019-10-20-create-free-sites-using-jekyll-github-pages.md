---
layout: post
title: Build websites using Jekyll and Github Pages.
---


Today, I will guide you on how to build a website or blog using Jekyll and Github Pages for free!

We will use the following tools:

- **Jekyll**: [Jekyll](http://jekyllrb.com) is a static site generator, an open-source tool for creating simple yet powerful websites of all shapes and sizes.
- **Github Pages**: [Github Pages](https://pages.github.com/) is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub and publishes a website. 
- **A Markdown Editor**: [StackEdit](https://stackedit.io/editor) is an online markdown editor. Or you may choose any other tool as per your preferences.



Setup Jekyll:
-------------

- Choose a free Jekyll theme from [https://jekyllthemes.io/free](https://jekyllthemes.io/free) or any other theme store.
- Download theme files on your local computer.
- Install [ruby](https://www.ruby-lang.org/en/documentation/installation/) and [Jekyll](https://jekyllrb.com/docs/installation/).
- Run `jekyll serve --watch`


Setup Github Pages:
-------------------


- Create a [new repository](https://help.github.com/en/articles/create-a-repo) on your Github account and put your theme on Github([check this out](https://help.github.com/en/articles/adding-an-existing-project-to-github-using-the-command-line)).
- Go to **Settings** tab of your theme repository and navigate to Github Pages section. 
- Select *master* from the source drop-down menu and page will be re-loaded automatically.
- Navigate to Github Pages section again and check your website URL here.
- Your website is up and ready.
- Additionally, you can use a custom domain to serve your site. Add your custom domain name(e.g. "ydrall.ml") in "Custom Domain" input and press "Save" button.


 

Add A New Post/Article:
-------------

Adding a new post is a very simple 4 step process:

- Navigate to _posts folder and add a new file named in format yyyy-mm-dd-title-of-the-post.md, eg. 2019-10-18-build-site-using-jekyll-github-pages.
- Add suitable meta-data at the top of file, e.g.

<pre>---
layout: post
title: Build websites using Jekyll and Github Pages.
---</pre>

- Open [StackEdit Editor](https://stackedit.io/editorStart) and start writing your content in [markdown language](https://www.markdownguide.org/getting-started).
- Once completed, copy content form editor to your file and push changes to Github. That's it. Your post will be available on your site within a minute.

