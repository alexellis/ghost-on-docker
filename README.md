# ghost-on-docker

![Ghost](https://raw.githubusercontent.com/alexellis/ghost-on-docker/master/static/ghost_small.png)

Pair Docker and Ghost for the perfect platform to run your blog!

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
  * Very fast build time and high amount of requests/per second compared to a Raspberry PI, my Core i5 NUC with 16GB RAM running a single container gave around 85-90 requests/per second.

  Example usage:

  ```
  $ docker run --name blog -d -p 80:2368 alexellis2/ghost-on-docker:latest
  ```
  Or use the recently added [Docker Compose file](https://github.com/alexellis/ghost-on-docker/blob/master/x86_64/docker-compose.yml) for even less fuss:
  
  ```
  $ docker-compose up -d
  ```

* ARMv7 (Raspberry PI 2 / 3)
 * [Dockerfile](https://github.com/alexellis/ghost-on-docker/blob/master/ARMv7/Dockerfile)
 * Building SQLite npm module on PI 2 takes about 7 minutes
 * semver and other required modules will take quite some time
 * Once up and running can handle 12-16 requests per second
 * Nginx is beneficial as a cache (dramatically improving requests/per second), but not absolutely necessary.

 Example usage:

 ```
 $ docker run --name blog -d -p 80:2368 alexellis2/ghost-on-docker:armv7
 ```

* ARMv6 (Raspberry PI A/B/B+/Zero)
 * [Dockerfile](https://github.com/alexellis/ghost-on-docker/blob/master/ARMv6/Dockerfile)
 * Note: ARMv6, especially models with < 512mb RAM will require a swapfile for building the *SQLite* npm module. [Creating SWAP file](https://wiki.archlinux.org/index.php/swap)
 * Building SQLite npm module on PI Zero takes about 16 minutes
 * Once up and running performs 2-3 requests per second, use of Nginx or another cache is highly recommended.

  Example usage:

  ```
  $ docker run --name blog -d -p 80:2368 alexellis2/ghost-on-docker:armv6
  ```

### Benchmarking

One of the simplest ways you can benchmark your blog is to use Apache Bench. It has a very simple CLI, here's an example load:

On the Docker host:

```
$ docker run --name blog -d -p 80:2368 alexellis2/ghost-on-docker:latest
5c71cdf984fefc7b508e8ee0f0d82c389ee492a339f7df23be95a61e83340156
```

From another PC:

```
$ ab -c 4 -n 1000 http://192.168.0.240/
```

* `-c 4` means 4 concurrent requests, simulating three users hitting the page at exactly the same time
* `-n 1000` means 1000 requests, so each of the 4 users will hit the page a portion of that time. i.e. 250 requests each.

You can play with the numbers to see how the blog performs under different conditions, you could also try typing in `docker stats` to see what kind of load the Docker container is creating.

### Coming soon

* *docker-compose.yml* file
 * adding volume support to add persistence of your posts (current available through built-in admin page)
 * ramp-up performance with a purpose-built Nginx Docker container to sit in front of your blog and take the load off.
* Full instructions for Raspberry PI Model B 2/3
 * set up Arch Linux, Docker and Ghost

### Questions/comments?

Head over to [my blog](http://blog.alexellis.io/ghost-on-docker-5mins/) and post a comment/question, or if you've found a bug raise an issue on Github.

### See also:

#### Just want to learn Docker?

Start learning today with a dozen progressive labs with my [Hands-on Docker tutorial](http://blog.alexellis.io/handsondocker/)

#### How I self-host my blog for free

> [Self-hosting on a Raspberry PI](http://blog.alexellis.io/self-hosting-on-a-pi/)

> [How I use dynamic DNS for alexellis.io](http://blog.alexellis.io/alexellis-io/)
