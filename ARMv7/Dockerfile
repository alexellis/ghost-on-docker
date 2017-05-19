FROM alexellis2/nodejs-armhf:6.9.2

USER root
WORKDIR /var/www/
RUN mkdir -p ghost
RUN apt-get update && apt-get -qy install wget unzip && \
    wget https://github.com/TryGhost/Ghost/releases/download/0.11.8/Ghost-0.11.8.zip && \
    unzip Ghost-*.zip -d ghost && \
    apt-get -y remove wget unzip && \
    rm -rf /var/lib/apt/lists/*

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

