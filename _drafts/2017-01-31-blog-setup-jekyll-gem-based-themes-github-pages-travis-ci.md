---
title:  "Blog setup (Jekyll + Gem-based themes + Github Pages + Travis-CI)"
date:   2017-01-31 18:00:00 +0000
categories: blog jekyll travis-ci github-pages
---

When I was setting up this blog, I wanted to use Github Pages with Jekyll.
I follow some tutorials, forked a few [different](https://github.com/Huxpro/huxpro.github.io) [themes](https://biomadeira.github.io/jasper/), but it felt a hack to fork a repository, keep it update with original, making changes, resolving merge conflicts, bahhh :S, that was something that I didn't want to do, for a simple blog.

Then I find out that since version 3.2, Jekyll start supporting [Gem-based themes](http://jekyllrb.com/docs/themes/), which seems what I was looking for! But after a quick search I find out that [Github Pages](https://pages.github.com/) only support a small number of [themes](https://pages.github.com/themes/), which made me return to the original plan of forking a repository.

After a while, when I was trying a new [theme](https://github.com/mmistakes/minimal-mistakes) I found this [github issue](https://github.com/mmistakes/minimal-mistakes/issues/662) which was exactly what I was trying to archive!
Basically if I perform the Jekyll build outside of github, like on my local machine or [Travis-CI](https://travis-ci.org/), I could still use Jekyll Gem-based themes, and push to github only the generated file inside `_site`.

I already tried the [Jasper theme](https://biomadeira.github.io/jasper/) with [Travis-CI](https://travis-ci.org/) so maybe that wouldn't be that hard.

I followed this [guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) especially the sections using the [Ruby Gem Method](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#ruby-gem-method).

The most important files to get started are:
-   [`_config.yml`](https://github.com/4brunu/4brunu.github.io/blob/source/_config.yml) for blog configuration (modified from [https://github.com/mmistakes/minimal-mistakes](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml))
-   [`.travis.yml`](https://github.com/4brunu/4brunu.github.io/blob/source/.travis.yml) for Travis-CI configuration (modified from [https://github.com/biomadeira/jasper/blob/master/.travis.yml](https://github.com/biomadeira/jasper/blob/master/.travis.yml))
-   [`Rakefile`](https://github.com/4brunu/4brunu.github.io/blob/source/Rakefile) which is invoked by Travis-CI to build the Jekyll `_site` and pushes it to [`master branch`](https://github.com/4brunu/4brunu.github.io/tree/master) (modified from [https://github.com/biomadeira/jasper/blob/master/Rakefile](https://github.com/biomadeira/jasper/blob/master/Rakefile))
-   [`gemfile`](https://github.com/4brunu/4brunu.github.io/blob/source/Gemfile) where I put my dependencies like [Github Pages or Jekyll](https://github.com/4brunu/4brunu.github.io/blob/source/Gemfile#L3-L4), [Gem-based Theme](https://github.com/4brunu/4brunu.github.io/blob/source/Gemfile#L8), and some [build dependencies](https://github.com/4brunu/4brunu.github.io/blob/source/Gemfile#L7)

And after some tweaking and failed build's, it worked! :D

In general I'm satisfied with the setup, Travis-CI does all the heavy lifting for me, it builds the site in every commit, although I would like that the build times were faster, currently they are around 2 and half minutes.

If you have any suggestion to improve, please let me know.
