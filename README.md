# ghost-on-docker

Recipe for building and running Ghost blogging platform on Docker

*This project is work-in-progress*

### Getting started

You can pull the ARMv7 image (for PI2/3) straight from the Docker Hub `docker pull alexellis2/ghost-on-arm:armv7` or build it yourself using the Dockerfiles as listed.

### Dockerfiles

* ARMv7 (Raspberry PI 2 / 3) 
 * [Dockerfile](https://github.com/alexellis/ghost-on-docker/blob/master/ARMv7/Dockerfile)
 * Building SQLite npm module on PI 2 takes about 7 minutes
 * semver and other required modules will take quite some time
* ARMv6 (Raspberry PI A/B/B+/Zero)
 * [Dockerfile](https://github.com/alexellis/ghost-on-docker/blob/master/ARMv6/Dockerfile)
 * Note: ARMv6, especially models with < 512mb RAM will require a swapfile for building the *SQLite* npm module. [Creating SWAP file](https://wiki.archlinux.org/index.php/swap)
 * Building SQLite npm module on PI Zero takes about 16 minutes

### Questions/comments?

Head over to my blog and post a comment/question.

[Self-hosting on a Raspberry PI](http://blog.alexellis.io/self-hosting-on-a-pi/)
