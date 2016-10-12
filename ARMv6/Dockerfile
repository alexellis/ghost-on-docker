FROM alexellis2/nodejs-armv6:4.4

USER root
RUN mkdir -p /var/www/ghost 
WORKDIR /var/www/ghost/

RUN apt-get -qy update && \
    apt-get -qy install --no-install-recommends \
     curl ca-certificates unzip && \
     curl -sSLO https://github.com/TryGhost/Ghost/releases/download/0.11.2/Ghost-0.11.2.zip && \
     rm -rf /var/lib/apt/lists/* && \
     unzip Ghost-0.11.2.zip

RUN useradd ghost -m -G www-data -s /bin/bash
RUN chown ghost:www-data .
RUN chown ghost:www-data -R *
RUN npm install -g pm2

USER ghost
WORKDIR /var/www/ghost
RUN /bin/bash -c "time (npm install sqlite3)"
RUN npm install

ENV NODE_ENV production

RUN chown ghost:www-data -R /var/www/ghost/
USER ghost
RUN sed -e s/127.0.0.1/0.0.0.0/g ./config.example.js > ./config.js

EXPOSE 2368
EXPOSE 2369

CMD ["pm2", "start", "index.js", "--name", "blog", "--no-daemon"]
