FROM alexellis2/nodejs-armhf:6.9.2

USER root
WORKDIR /root/

RUN mkdir -p /var/www/ghost 
WORKDIR /var/www/ghost/

RUN apt-get -qy update && \
    apt-get -qy install --no-install-recommends \
     curl ca-certificates unzip && \
     curl -sSLO https://github.com/TryGhost/Ghost/releases/download/0.11.8/Ghost-0.11.8.zip && \
     rm -rf /var/lib/apt/lists/* && \
     unzip Ghost-0.11.8.zip

RUN useradd ghost -m -G www-data -s /bin/bash
RUN chown ghost:www-data .
RUN chown ghost:www-data -R *
RUN npm install -g pm2

USER ghost
WORKDIR /var/www/ghost
#RUN npm install sqlite3
RUN npm install

EXPOSE 2368
EXPOSE 2369
RUN ls && pwd

ENV NODE_ENV production

RUN sed -e s/127.0.0.1/0.0.0.0/g ./config.example.js > ./config.js

VOLUME ["/var/www/ghost/content/apps"]
VOLUME ["/var/www/ghost/content/data"]
VOLUME ["/var/www/ghost/content/images"]

CMD ["pm2", "start", "index.js", "--name", "blog", "--no-daemon"]
