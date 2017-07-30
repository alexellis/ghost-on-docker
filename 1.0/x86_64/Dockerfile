FROM node:6.11.1-alpine

ENV NPM_CONFIG_LOGLEVEL warn

WORKDIR /var/www/ghost
RUN npm install -g ghost-cli && \
    addgroup www-data && \
    adduser ghost -G www-data -S /bin/bash && \
    chown ghost:www-data -R /var/www/ghost

USER ghost
RUN ghost install local --no-start && \
    sed -ie s/127.0.0.1/0.0.0.0/g config.development.json

EXPOSE 2368
EXPOSE 2369

ENV NODE_ENV production
CMD ["ghost", "run", "--development", "--ip", "0.0.0.0"]
