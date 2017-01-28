---
title:  "Blog setup (Jekyll + Gem-based themes + Github Pages + Travis-CI)"
date:   2017-01-31 18:00:00 +0000
categories: blog
tags: jekyll travis-ci github-pages
---

> TL;DR. GitHub Pages doesn't currently support 3rd party theme gems. You can workaround this, by building Jekyll in your local machine or in a CI service like Travis-CI and push to Github the generated files inside `_site`. :rocket:
>
> WARNING: This is not supposed to be a step by step tutorial, but my experience and some hints on how you can archive the same thing.

### The initial idea

When I was setting up this blog, I wanted to use [Github Pages](https://pages.github.com/) and [Jekyll](http://jekyllrb.com).

I follow some tutorials, forked a few [different](https://github.com/Huxpro/huxpro.github.io) [themes](https://biomadeira.github.io/jasper/), but it felt a hack to fork a repository, keep it update with original, making local changes which could result in future conflicts, bah :unamused:
That's something that I didn't want to do for a simple blog... I want to apply the [KISS principle](https://en.wikipedia.org/wiki/KISS_principle).

Then I find out that since version 3.2, Jekyll start supporting [Gem-based themes](http://jekyllrb.com/docs/themes/), which seems what I was looking for, but after a quick search I find out this:

> Note: Not all Jekyll themes are supported. For a list of Jekyll themes that are supported by GitHub Pages, see [https://pages.github.com/themes](https://pages.github.com/themes).
>
> -- <cite>[Adding a Jekyll theme to your GitHub Pages site](https://help.github.com/articles/adding-a-jekyll-theme-to-your-github-pages-site/)</cite>

[Github Pages](https://pages.github.com/) only support a small number of [themes](https://pages.github.com/themes/), which made me return to the original plan of forking a repository.

### A better way

After a while, when I was trying a new [theme](https://github.com/mmistakes/minimal-mistakes) I found this [github issue](https://github.com/mmistakes/minimal-mistakes/issues/662).

> <cite>Question:</cite> Use with GH pages without requiring fork?
>
> <cite>Answer:</cite> ... The problem is GitHub Pages doesn't currently support 3rd party theme gems. Similar to how they don't allow Jekyll plugins (except for a few that have been whitelisted). So instead of pushing commits to GH and having it build your site, you need to build it locally and push the contents of your _site folder.
> ... A lot of people use CI services like Travis to build their site and deploy to GH.
>
> -- <cite>[Question: Use with GH pages without requiring fork? · Issue #662 · mmistakes/minimal-mistakes](https://github.com/mmistakes/minimal-mistakes/issues/662)<cite>

This was exactly what I was trying to archive!
Basically if I perform the Jekyll build outside of github, like on my local machine or [Travis-CI](https://travis-ci.org/), I could still use Jekyll Gem-based themes, and push to github only the generated file inside `_site`.

I already tried the [Jasper theme](https://biomadeira.github.io/jasper/) with [Travis-CI](https://travis-ci.org/) so maybe that wouldn't be that hard.

I followed this [guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) especially the sections [Ruby Gem Method](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#ruby-gem-method) and [Setup Your Site](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#setup-your-site).

The most important files to get started are:
-   [`_config.yml`](https://github.com/4brunu/4brunu.github.io/blob/source/_config.yml) for blog configuration (modified from [https://github.com/mmistakes/minimal-mistakes](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml))
-   [`.travis.yml`](https://github.com/4brunu/4brunu.github.io/blob/source/.travis.yml) for Travis-CI configuration (modified from [https://github.com/biomadeira/jasper/blob/master/.travis.yml](https://github.com/biomadeira/jasper/blob/master/.travis.yml))
-   [`Rakefile`](https://github.com/4brunu/4brunu.github.io/blob/source/Rakefile) which is invoked by Travis-CI to build Jekyll and push the `_site` directory to [`master branch`](https://github.com/4brunu/4brunu.github.io/tree/master) (modified from [https://github.com/biomadeira/jasper/blob/master/Rakefile](https://github.com/biomadeira/jasper/blob/master/Rakefile))
-   [`gemfile`](https://github.com/4brunu/4brunu.github.io/blob/source/Gemfile) where I put my dependencies like [Github Pages or Jekyll](https://github.com/4brunu/4brunu.github.io/blob/source/Gemfile#L3-L4), [Gem-based Theme](https://github.com/4brunu/4brunu.github.io/blob/source/Gemfile#L8), and some [build dependencies](https://github.com/4brunu/4brunu.github.io/blob/source/Gemfile#L7)

And after some tweaking and failed build's, I got it working! :smile: :tada: :rocket:

### Conclusion

In general I'm satisfied with the setup, Travis-CI does all the heavy lifting for me, it builds the site in every commit, although I would like that the build times were faster, currently they are around two and half minutes.

If you have any suggestion to improve, or any issue trying to reproduce what I describe, please let me know.
