FROM node:6.11.1-alpine

ENV NPM_CONFIG_LOGLEVEL warn


USER root
WORKDIR /root/

WORKDIR /var/www/
RUN npm install -g ghost-cli

RUN addgroup www-data
RUN adduser ghost -G www-data -S /bin/bash
RUN chown ghost:www-data .

USER ghost
WORKDIR /var/www/
RUN mkdir -p ghost
WORKDIR /var/www/ghost

RUN ghost install local --no-start

EXPOSE 2368
EXPOSE 2369

ENV NODE_ENV production
RUN sed -ie s/127.0.0.1/0.0.0.0/g config.development.json

CMD ["ghost", "run", "--development", "--ip", "0.0.0.0"]
