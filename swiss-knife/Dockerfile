FROM mhart/alpine-node:8.7.0

MAINTAINER Ivan Berdinsky

COPY docker-entrypoint.sh /usr/local/bin/

ADD package.json /srv

RUN chmod +x /usr/local/bin/docker-entrypoint.sh && \
  set -ex &&\
  cd /srv &&\
  apk add --no-cache git make g++ python autoconf automake nasm libjpeg-turbo-dev zlib-dev &&\
  npm install &&\
  apk del --no-cache --purge make g++ python autoconf automake nasm libjpeg-turbo-dev zlib-dev &&\
  ln -s /srv/node_modules/.bin/gulp /usr/bin/gulp &&\
  rm -rf /root/.npm /root/.config /tmp/npm* /tmp/phantomjs


WORKDIR /work
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["npm", "run", "gulp"]
