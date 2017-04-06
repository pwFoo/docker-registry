# Self-Hosted Docker Registry

## Introduction

This is a Docker Registry that has token authentication all under the same domain. It was built for a specific use case, however with the configuration files being exposed it can be changed to meet other needs.

## Requirements

Installing the two pieces of software below will be all that you need to

* [Docker](https://www.docker.com/community-edition#/download)
* [Docker Compose](https://docs.docker.com/compose/install/)

## Getting started

First you'll need to generate certs for the token auth for docker registry (any values can be put into the cert)
```bash
cd auth_server/ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.pem
```

Next, bring up all the containers
```bash
docker-composer up -d
```

## Things to be aware of

Some images generated by older versions of Docker may fail when pushing to this registry. Try rebuilding the affected layers. [The github issue about this error](https://github.com/docker/distribution/issues/1709) has more information about what to do.

Caddy is configured to auto-request [Let's Encrypt](https://letsencrypt.org/) TLS certificates, however it is possible to include your own if you already have some.

## Thanks

This wouldn't be possible without the work of others

* [Docker](https://www.docker.com/)
* [Caddy](https://caddyserver.com)
* [Docker Registry 2 authentication server](https://github.com/cesanta/docker_auth)
