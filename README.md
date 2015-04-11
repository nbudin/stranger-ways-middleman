# stranger-ways.com

Copyright &copy; 2011-2015 Stranger Ways, all rights reserved.

stranger-ways.com is a [Middleman](https://middlemanapp.com) site.  It's statically compiled to HTML, then uploaded to Amazon S3 and served from there using the CloudFront content distribution network.  This should mean it's lightning-fast and basically impossible to hack using the usual means (because nothing is running server-side).

## Installing Middleman and its friends

You'll need a recent version of [Ruby](http://ruby-lang.org) because that's what Middleman is written in.  I recommend 2.1 or above.  Once that's installed, you'll need [Bundler](http://gembundler.com).  To install it, run this command:

`gem install bundler`

You'll also need [ImageMagick](http://www.imagemagick.org) because we use that for resizing images for thumbnails.  If you're on Linux, your distribution probably packages it.  Make sure to get the -dev or -devel package as well so you get the libraries.  On Mac OS X, use Homebrew or some such.  On Windows, I dunno, I can't help you.

Finally, from inside the stranger-ways.com directory:

`bundle install`

That should get Middleman and all the other dependencies installed.

## Compiling, testing, deploying

To compile the site into static HTML files:

`bundle exec middleman build`

To run a local web server on http://localhost:4567 that is serving a test copy of the site:

`bundle exec middleman server`

To deploy the site to Amazon S3 (note that you'll need the S3 keys in your environment variables; they're not checked in here so ask Nat):

`bundle exec middleman s3_sync`

## Middleman basics

A Middleman page more or less looks like this:

```markdown
---
title: My awesome page
layout: page
other_stuff: blah
---

Hello!  This is an **awesome** page.  It has the other stuff <%= current_page.data.other_stuff %> on it.

* one
* two
* three
```

Basically there is some frontmatter (the stuff between the three dashes) which is written in YAML format.  All pages should have at least a title and a layout.  Layout refers to one of the files in the `_layouts` directory; title gets put in the page's HTML title tag as well as in a h1 on top of the content.  You can also specify whatever other variables you want there.

The content below it is parsed according to the file's extension.  In this case, the page is written in Markdown, so it'd have a .md file extension.  You could also write it in Textile or just straight-up HTML.  There are probably other things we could write pages in by adding plugins but that's what comes with Middleman.

You can also use [helper methods](https://middlemanapp.com/basics/helper_methods/) inside the pages for parsed content.  In this case I'm substituting in the value of the `other_stuff` variable.  More useful things to do are to include the content of other files, loop through arrays, put in the current date, stuff like that.  Note that all this happens at compile time, not when the page is viewed.

## Posts

Posts are like pages, but they live in the `posts` directory.  They have to have a name that begins with a YYYY-MM-DD formatted year.  They are essentially blog posts, and get treated as such.

Traditionally we've mostly used the blog posts for announcing shows.  We've got a tag just for that.  If you add these lines to the YAML frontmatter in a post, it'll show up in the Shows tab of the site:

```
tags:
  - shows
```

There could be other post tags too but we haven't really used those as yet.

## Configuration

There's a config file at the top of the repo.  `config.rb` is the main Middleman config and it tells Middleman basically everything about how the site should be compiled and deployed.  `.tm_properties` is a property file for if you use TextMate (like I do).  `Gemfile` and `Gemfile.lock` are for Bundler; they specify which Ruby gems should be loaded when compiling the site.
