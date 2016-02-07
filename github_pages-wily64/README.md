# About

Docker recipe used in my Docker [tl,dr tutorial](https://alexconst.github.io/2016/02/02/docker-basics/).



Dockerfile recipe for GitHub Pages Jekyll with a twist. It uses the `ENTRYPOINT` option to bind the container to an executable.

NOTE: this is just a simple test and you actually don't want to use Jekyll on your system like this. Check my Vagrant development environment [recipe](https://github.com/alexconst/vagrant_recipes/) instead.

# Instructions

Build the image:
```bash
image_name_tag="alexconst/jekyll:v1"
docker build -t "${image_name_tag}" .
# check it
docker images
```


Spin a new container from our image:
```bash
contport="4000"
hostport="4000"
contmnt="/shared/"
hostmnt="/home/username/home/downloads/share_docker/"
# Before you spin an image, make sure you have a directory named `blog` in the host shared folder.
# NOTE: only run the `new` command if you have nothing there
# create a new site:
docker run -t -i --rm=true -v "${hostmnt}:${contmnt}" -p "${hostport}:${contport}"  "${image_name_tag}" new .
# build the site:
docker run -t -i --rm=true -v "${hostmnt}:${contmnt}" -p "${hostport}:${contport}"  "${image_name_tag}" build
# serve the site:
docker run -t -i --rm=true -v "${hostmnt}:${contmnt}" -p "${hostport}:${contport}"  "${image_name_tag}" serve
```

