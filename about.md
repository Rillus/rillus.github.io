---
layout: page
title: About
permalink: /about/
---

Welcome to this experimental site for Riley's notes and musings.

## How this site was built

This has been created using a mix of Obsidian, and Github Pages using Jekyll to compile and theme markdown files and build/deploy.

The theme is [minima](https://github.com/jekyll/minima) by [Jekyll](https://jekyllrb.com/). I've set it up to run locally by doing

``` bash
bundle exec jekyll serve --livereload
```

But prior to that I had to
```bash
gem install jekyll
```

and ensure the path to Ruby was in my PATH variables in  my `.zshrc` file

When I add a new file, I can simply run:
```bash
cd ~/Documents/Obsidian\ Vault/rillus.github.io
git add .
git commit -m "Blog update"
git push origin master
```

Any pushes to `master` branch will trigger a new build.deploy via Github Actions.