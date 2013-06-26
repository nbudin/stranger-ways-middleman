# stranger-ways.com

Copyright &copy; 2011-2013 Stranger Ways, all rights reserved.

stranger-ways.com is a [Jekyll](https://github.com/mojombo/jekyll) site.  It's statically compiled to HTML, then uploaded to Amazon S3 and served from there using the CloudFront content distribution network.  This should mean it's lightning-fast and basically impossible to hack using the usual means (because nothing is running server-side).

## Installing Jekyll and its friends

You'll need a recent version of [Ruby](http://ruby-lang.org) because that's what Jekyll is written in.  I recommend 1.9.3 or above.  Once that's installed, you'll need [Bundler](http://gembundler.com).  To install it, run this command:

`gem install bundler`

You'll also need [ImageMagick](http://www.imagemagick.org) because we use that for resizing images for thumbnails.  If you're on Linux, your distribution probably packages it.  Make sure to get the -dev or -devel package as well so you get the libraries.  On Mac OS X, use Homebrew or some such.  On Windows, I dunno, I can't help you.

Finally, from inside the stranger-ways.com directory:

`bundle install`

That should get Jekyll and all the other dependencies installed.

## Compiling, testing, deploying

To compile the site into static HTML files:

`jekyll`

To run a local web server on http://localhost:4000 that is serving a test copy of the site:

`jekyll --server`

To deploy the site to Amazon S3 (note that you'll need the S3 keys in your environment variables; they're not checked in here so ask Nat):

```
jekyll
jekyll-s3
```

## Jekyll basics

A Jekyll page more or less looks like this:

```
---
title: My awesome page
layout: page
other_stuff: blah
---

Hello!  This is an **awesome** page.  It has the other stuff {{ page.other_stuff }} on it.

* one
* two
* three
```

Basically there is some frontmatter (the stuff between the three dashes) which is written in YAML format.  All pages should have at least a title and a layout.  Layout refers to one of the files in the `_layouts` directory; title gets put in the page's HTML title tag as well as in a h1 on top of the content.  You can also specify whatever other variables you want there.

The content below it is parsed according to the file's extension.  In this case, the page is written in Markdown, so it'd have a .md file extension.  You could also write it in Textile or just straight-up HTML.  There are probably other things we could write pages in by adding plugins but that's what comes with Jekyll.

You can also use [Liquid](http://www.liquidmarkup.org) syntax inside the pages for parsed content.  In this case I'm substituting in the value of the `other_stuff` variable.  More useful things to do are to include the content of other files, loop through arrays, put in the current date, stuff like that.  Note that all this happens at compile time, not when the page is viewed.

## Posts

Posts are like pages, but they live in the `_posts` directory.  They have to have a name that begins with a YYYY-MM-DD formatted year.  They are essentially blog posts, and get treated as such.

Traditionally we've mostly used the blog posts in Wordpress for announcing shows.  We've got a category just for that.  If you add these lines to the YAML frontmatter in a post, it'll show up in the Shows tab of the site:

```
categories:
  - Shows
```

There could be other post categories too but we haven't really used those as yet.

## Plugins

Plugins live in the `_plugins` directory.  We currently have two of them:

* `bundler.rb` just loads up Bundler when Jekyll starts, so Jekyll will have access to all the gems in our Gemfile and nothing else.
* `gallery_generator.rb` is [a third-party plugin from ggreer](https://github.com/ggreer/jekyll-gallery-generator).  It looks for images inside the `photos` directory and generates image gallery pages for them.

We could add more plugins; one of the nice things about Jekyll is that it's pretty easy to hook into and extend.

## Configuration

There are a few config files at the top of the repo.  `_config.yml` is the main Jekyll config and it tells Jekyll a few things about how the site should be compiled.  `_jekyll_s3.yml` configures the deployment to Amazon.  `.tm_properties` is a property file for if you use TextMate (like I do).  `Gemfile` and `Gemfile.lock` are for Bundler; they specify which Ruby gems should be loaded when compiling the site.
