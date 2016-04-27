# ghost-on-docker

Recipe for building and running Ghost blogging platform on Docker

*This project is work-in-progress*

### Dockerfiles

* ARMv7 (Raspberry PI 2 / 3) 
 * [Dockerfile](https://github.com/alexellis/ghost-on-docker/blob/master/ARMv7/Dockerfile)
* ARMv6 (Raspberry PI A/B/B+/Zero)
 * [Dockerfile](https://github.com/alexellis/ghost-on-docker/blob/master/ARMv6/Dockerfile)
 * Note: ARMv6, especially models with < 512mb RAM will require a swapfile for building the *SQLite* npm module. [Creating SWAP file](https://wiki.archlinux.org/index.php/swap)

### Questions/comments?

Head over to my blog and post a comment/question.

[Self-hosting on a Raspberry PI](http://blog.alexellis.io/self-hosting-on-a-pi/)
