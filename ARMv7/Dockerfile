FROM alexellis2/node4.x-arm:latest

USER root
WORKDIR /var/www/
RUN mkdir -p ghost
RUN apt-get update && apt-get -qy install wget unzip
RUN wget https://ghost.org/zip/ghost-0.7.9.zip
RUN unzip ghost-0.7.9.zip -d ghost
RUN useradd ghost -m -G www-data -s /bin/bash
RUN chown ghost:www-data .
RUN chown ghost:www-data ghost
RUN chown ghost:www-data -R ghost/*
RUN npm install -g pm2

USER ghost
WORKDIR /var/www/ghost
RUN /bin/bash -c "time (npm install sqlite3)"
RUN npm install

EXPOSE 2368
EXPOSE 2369
RUN ls && pwd

ENV NODE_ENV production

RUN sed -e s/127.0.0.1/0.0.0.0/g ./config.example.js > ./config.js
CMD ["pm2", "start", "index.js", "--name", "blog", "--no-daemon"]

