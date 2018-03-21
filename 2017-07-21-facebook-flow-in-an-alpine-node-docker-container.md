Running Facebook's Flow in an Alpine Node Container

Create Dockerfile and npmrc template

Creating the Dockerfile was more chalanging than expected. To make flow work in Alpine we need `glibc`. To get glibc from GitHub we need `wget` with SSL support (and ca-certs).

All in all this Dockerfile works:

```
FROM node:8-alpine

# Install bash (required by scripts/*) and GNU wget
RUN apk update \
  && apk add \
    bash \
    wget \
    ca-certificates

# Install glibc comaptibility for alpine (required by flow)
RUN wget \
    --quiet \
    --output-document=/etc/apk/keys/sgerrand.rsa.pub \
    https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub \
  && wget \
    --quiet \
    https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-2.25-r0.apk \
  && apk add glibc-2.25-r0.apk

# Slim the image by removing APK cache
RUN rm -rf /var/cache/apk/*

USER node
# This build time argument should be passed by build script.
# See common.sh, jenkins-build.sh and .npmrc files
ARG npm_token

WORKDIR                               /home/node
COPY package.json                     ./
COPY package-lock.json                ./
COPY .flowconfig                      ./.flowconfig
COPY npmrc.template                   ./.npmrc
COPY src                              ./src
COPY scripts                          ./scripts

RUN npm install

RUN rm ./.npmrc

CMD npm start
```

Sources:

  - https://github.com/facebook/flow/issues/3649#issuecomment-308070179
  - https://github.com/google/cadvisor/issues/1131#issuecomment-229108215
