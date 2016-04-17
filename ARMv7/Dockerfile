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

USER ghost
WORKDIR /var/www/ghost
RUN npm install -g pm2

RUN npm install

CMD ["node", "index.js"]
