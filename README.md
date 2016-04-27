# ghost-on-docker

![Ghost](https://raw.githubusercontent.com/alexellis/ghost-on-docker/master/static/ghost_small.png)

Recipes for building and running Ghost blogging platform on Docker

> Find out more about [Ghost](https://ghost.org) here

Ghost is an elegant and minimal blogging platform that focus on simplicity. One of its most attractive features is its Markdown editor. It's also fully hackable running on Node.js with the [Handlebars](http://handlebarsjs.com) view-engine.

*This project is work-in-progress but all the blog images are fully working*

### Getting started

You can pull the ARMv7 image (for PI2/3) straight from the Docker Hub `docker pull alexellis2/ghost-on-arm:armv7` or build it yourself using the Dockerfiles as listed.

> Please support the project by giving it a **Star**.

### Dockerfiles

These are all based upon Node 4.x, pick the architecture for your computer/server. If you are using a regular PC it will be the first option marked x86_x64. Each image has been pushed to the Docker hub, the `npm` modules alone for Ghost take up around 500MB, but the download will be faster than a fresh build if you use a Raspberry PI.

* Regular PC/Laptop - x86_x64
 * [Dockerfile](https://github.com/alexellis/ghost-on-docker/blob/master/x86_64/Dockerfile)
  * Based upon Alpine Linux
  * Very fast build time and requests/per second compared to a Raspberry PI.

* ARMv7 (Raspberry PI 2 / 3)
 * [Dockerfile](https://github.com/alexellis/ghost-on-docker/blob/master/ARMv7/Dockerfile)
 * Building SQLite npm module on PI 2 takes about 7 minutes
 * semver and other required modules will take quite some time
 * Once up and running can handle 12-16 requests per second
 * Nginx is beneficial as a cache (dramatically improving requests/per second), but not absolutely necessary.

* ARMv6 (Raspberry PI A/B/B+/Zero)
 * [Dockerfile](https://github.com/alexellis/ghost-on-docker/blob/master/ARMv6/Dockerfile)
 * Note: ARMv6, especially models with < 512mb RAM will require a swapfile for building the *SQLite* npm module. [Creating SWAP file](https://wiki.archlinux.org/index.php/swap)
 * Building SQLite npm module on PI Zero takes about 16 minutes
 * Once up and running performs 2-3 requests per second, use of Nginx or another cache is highly recommended.

### Questions/comments?

Head over to my blog and post a comment/question, or if you've found a bug raise an issue on Github.

[Self-hosting on a Raspberry PI](http://blog.alexellis.io/self-hosting-on-a-pi/)
