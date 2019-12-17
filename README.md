# Reproducible Research Oxford website

[![Netlify Status](https://api.netlify.com/api/v1/badges/2bedcda0-338d-4e19-9f1c-10a829c58b4b/deploy-status)](https://app.netlify.com/sites/hopeful-archimedes-2f00a3/deploys)

This site will enable people to ascertain quickly which initiatives are happening in Oxford to improve reproducibility in research, and to identify the key people behind those initiatives. 

# Working with the project

The project uses the static site generator Jekyll with the minimal-mistakes theme. The contents of this repository define the site which is to be built. Your computer will build its own version of the site when you test it, located in a new **_site** directory. 

Because most files are configuration or layout files, most contributors will want to ignore those files. As a general rule, most files should not be edited unless you know what you're doing (feel free to ask if you want to learn!). 

## Setting up

To work with the project you'll need a local setup capable of building and serving the Jekyll site. Following the [installation instructions](https://jekyllrb.com/docs/installation/) should get you started. Once you've done that, you can open a Ruby command prompt, `cd this_repo_clone_directory` and then `bundle exec jekyll serve` to build the site and start a webserver on your computer. You can then view the local version of the site by going to http://localhost:4000/. 

When you make changes to the Jekyll files you'll notice that Ruby automatically rebuilds the site and you can see your local changes by refreshing the page.

## Content files

Content files which contribute to the contents of the site can and should be edited! These are:
* The main page file, **_pages/main.md** (mostly now written in HTML)
* The first few lines of **_pages/people.md** and **_pages/initatives.md**, which introduce those collections before listing their contents
* The **_pages/get-involved.md** and **_pages/resources.md** files, which contain markdown defining those pages

## Collections

Collections are Jekyll's way of organising arbitrary content bundles, and they're used here to group initiatives and people. Files in the **_initiatives/** and **_team/** directories contain the entries for these collections, respectively. These files can be edited, and others created as necessary. Newly created files in these folders will be automatically added to the relevant pages.

### Images

The collection files usually have images associated with them. These are stored in the **assets/images/initiatives/** and **assets/images/team_members/** directories and referred to without the directory structure prefix in the YAML.

## File languages

There are six main languages used in the project. They are, in order of simplest to most complicated:
* [Markdown](https://gist.github.com/roachhd/779fa77e9b90fe945b0c)
    - a text markup language allowing simple formatting
    - Looks like: `[link text](link-url)`
* [YAML](https://idratherbewriting.com/documentation-theme-jekyll/mydoc_yaml_tutorial.html)
    - a configuration markup language used for defining Jekyll variables
    - You'll find this at the very top of most files, in between `---` separators.
    - Looks like: `key: value` pairs
* [HTML](https://www.w3schools.com/html/default.asp)
    - the markup language in which websites are written
    - Looks like: `<h1>Some title</h1>`
* [CSS](https://www.w3schools.com/css/default.asp)
    - a language for specifying the look of website components. 
    - In the project this is mostly generated second-hand using SCSS
    - You generally won't find this inside other files, except perhaps in HTML files inside `<style></style>` tags.
* [Liquid](https://shopify.github.io/liquid/)
    - a language which allows access to Jekyll's information at build time
    - Looks like: `{{ doc.collection }}` and `{% if doc.collection == "team" %}` tags.
* [JavaScript](https://www.w3schools.com/js/default.asp)
    - the client-side programming language which powers websites
    - You'll see this included via HTML inside `<script></script>` tags.
    
It's also possible to write custom plugins for Jekyll using [Ruby](http://rubylearning.com/satishtalim/first_ruby_program.html) itself, although the project doesn't currently use this.

## Advanced editing

The configuration and layout files can be edited, with appropriate caution. The customised layout files can certainly be improved on! Note that editing certain files, such as the master **_config.yml** file, will not trigger an update to the site, and the server will have to be restarted and the whole site rebuilt to see these changes.
