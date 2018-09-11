FROM jenkinsci/jnlp-slave:alpine

MAINTAINER Link <sumeet.chaudhari@bettercloud.com>
USER root

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 8.11.4-r0
ENV DOCKER_VERSION 18.06.1-r0

RUN apk add --no-cache gnupg git jq curl nodejs=$NODE_VERSION npm python rsync
RUN npm install -g yarn npm@6.0.0 crypto-js@3.1.9-1
RUN npm install cypress@3.0.3
RUN apk add docker=$DOCKER_VERSION ; dockerd -v; docker -v

# Install Docker binary
#RUN curl -fsSLO https://get.docker.com/builds/Linux/x86_64/docker-${DOCKER_VERSION}.tgz \
#    && tar --strip-components=1 -xvzf docker-${DOCKER_VERSION}.tgz -C /usr/bin

COPY ./nodejs/wait-for-it /usr/local/bin/