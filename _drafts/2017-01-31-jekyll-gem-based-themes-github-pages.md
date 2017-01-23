---
title:  "Jekyll + Gem-based themes + Github Pages"
date:   2017-01-31 18:00:00 +0000
categories: blog jekyll travis-ci
---

When I was setting up this blog, I wanted to use Github Pages with Jekyll.
I follow some tutorials, forked a few [different](https://github.com/Huxpro/huxpro.github.io) [themes](https://biomadeira.github.io/jasper/), but it felt a hack to fork a repository, keep it update with original, making changes, resolving merge conflicts, bahhh :S, that was something that I didn't want to do, for a simple blog.

Then I find out that since version 3.2, Jekyll start supporting [Gem-based themes](http://jekyllrb.com/docs/themes/), which seems what I was looking for! But after a quick search I find out that [Github Pages](https://pages.github.com/) only support a small number of [themes](https://pages.github.com/themes/), which made me return to the original plan of forking a repository.

After a while, when I was trying a new [theme](https://github.com/mmistakes/minimal-mistakes) I found this [github issue](https://github.com/mmistakes/minimal-mistakes/issues/662) which was exactly what I was trying to archive!
Basically if I perform the Jekyll build outside of github, like on my local machine or [Travis-CI](https://travis-ci.org/), I could still use Jekyll Gem-based themes, and push to github only the generated file inside `_site`.

I already tried the [Jasper theme](https://biomadeira.github.io/jasper/) with [Travis-CI](https://travis-ci.org/) so maybe that wouldn't be that hard.

I started with the most basic setup:
- modified [`_config.yml`]() from [](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml)
- [`.travis.yml`](https://github.com/biomadeira/jasper/blob/master/.travis.yml) from [biomadeira/jasper]() 
- modified [Rakefile]() from  https://github.com/biomadeira/jasper/blob/master/Rakefile
- basic [gemfile]()
