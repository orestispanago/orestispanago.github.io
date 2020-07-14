---
title: "Dockerize Jekyll blog"
date: 2019-07-13
tags: [automation, docker, jekyll]
header:
  image: # "/images/jekyll-on-docker.png"
excerpt: "Set up a docker container for Jekyll static site generator"
---



Jekyll is a popular static site generator written in Ruby. In fact, [this blog](https://github.com/orestispanago/orestispanago.github.io) is made using Jekyll.
Running a Jekyll blog locally or on a VPS requires installing Ruby and its dependencies, installing Jekyll, building the app and then running it.
Docker comes in handy to avoid all that hassle.

![alt text](/images/jekyll-on-docker.png)

Assuming you have cloned a nice repo from github, cd to the parent directory of the project and run:


```bash
docker run --rm -it --volume="$PWD:/srv/jekyll" -p 4000:4000 jekyll/jekyll jekyll serve
```

Edit your markdown files locally and refresh `localhost:4000` to see your changes.
However, building the image every time and discarding it is not that pretty, so using `docker-compose` keeps things tidy and updated once we commit our changes.  
As a bonus I have added `--livereload` command in `docker-compose.yml`.

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
To build the container for the first time, run `docker-compose up` (you may add `-d` flag after the first sucessfull build). Docker automatically names your container as `<projectname>_jekyll_1`.
From now on you can use the container name to start it without rebuilding it.
