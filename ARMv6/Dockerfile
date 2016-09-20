FROM alexellis2/nodejs-armv6:4.4

USER root
WORKDIR /var/www/
RUN mkdir -p ghost

RUN apt-get -qy update && \
    apt-get -qy install --no-install-recommends \
      curl ca-certificates && \
    curl -sSLO https://github.com/TryGhost/Ghost/archive/0.10.0.tar.gz && \
    tar -xvf ./0.10.0.tar.gz -C ./ghost --strip-components=1 && \
    rm *.tar.gz && \
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
USER root
RUN apt-get update && apt-get -qy install --no-install-recommends git
WORKDIR /var/www/ghost
RUN chown ghost:www-data -R ./*
RUN git init
RUN npm i -g grunt-cli
USER ghost
RUN grunt init --force
RUN sed -e s/127.0.0.1/0.0.0.0/g ./config.example.js > ./config.js
CMD ["pm2", "start", "index.js", "--name", "blog", "--no-daemon"]

