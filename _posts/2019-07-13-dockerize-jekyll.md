---
title: "Dockerize Jekyll blog"
date: 2019-07-13
tags: [automation, linux, shell,docker, jekyll]
header:
  image: ""
excerpt: "Automation, Linux, Shell scripting, Docker, Jekyll"
---


Jekyll is a popular static site generator writen in Ruby. In fact, this particular blog is hosted using Jekyll.
Running a blog on Jekyll required installing Ruby and its dependencies, Jekyll, building the app and then running it.
Docker comes in handy to avoid all that hassle.

Assuming you have cloned a nice repo from github, cd to the parent directory of the project and run:


```bash
docker run --rm -it --volume="$PWD:/srv/jekyll" -p 4000:4000 jekyll/jekyll jekyll serve
```

Edit your markdown files locally, refresh `localhost:4000` and you are good to go.
However, building the image every time and discarding it is not that pretty, so using `docker-compose` keeps things tidy and updated once we commit our changes.  
As a bonus I have added `--livereload` command in `docker-compose.yml`

```yml
jekyll:
  image: jekyll/jekyll:3.8
  command: jekyll serve --livereload --drafts
  ports:
    - 4000:4000
    - 35729:35729
  volumes:
    - .:/srv/jekyll
```
