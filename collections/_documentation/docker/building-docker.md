---
title: Build your image
description: How to use our stages and build your own Kimai docker image
canonical: /documentation/building-docker.html
---

The same docker file is used to build all the tagged images and is configured by combination of build arguments and targets.

## Clone the repo

Before you do anything else you will need to clone this repo and open a terminal in that folder:

```bash
git clone {{ site.kimai_v2_docker }}.git
cd kimai
```

## Targets

The docker file has many staging targets but two functional builds are `prod` and `dev` which correspond to the prod and development environments as outlined in the Kimai documentation.  The default is `prod`

```bash
docker build --target=prod .
docker build --target=dev .
```

## Build Arguments

### BASE

* `BASE=apache`
* `BASE=fpm`

Selects which PHP wrapper to use.  The Apache Debian version bundles an Apache server, and the mod-php wrapper based on a debian buster image.
The fpm-alpine version provides the fast CGI version of PHP based on an alpine image.

The Apache/Debian image is bigger (~940mb) but does not require a second container to provide http services.
Use this image for development, tests or evaluation.

The FPM image is smaller (~640mb) but requires a web server to provide the http services.
Use this image in production and see the [Docker Compose]({% link _documentation/docker/docker-compose.md %}) page for setting up a http server.

### KIMAI

This allows over releases of Kimai to be built.  You can specify anything that would be passed to a git clone command.

* A tag or release, e.g. `KIMAI={{ site.kimai_v2_version }}`
* A branch name, e.g. `KIMAI=main`

### TZ

The PHP timezone for the php build.  Defaults to Europe/Berlin.

* `TZ=Europe/London`

## Examples

Build a dev image of Kimai that uses the apache bundled web server:

```bash
docker build --target=dev --build-arg KIMAI={{ site.kimai_v2_version }} --build-arg BASE=apache .
```

Build a prod, FPM image of Kimai, localised for the UK

```bash
docker build --target=prod --build-arg KIMAI={{ site.kimai_v2_version }} --build-arg BASE=fpm --build-arg TZ=Europe/London .
```

## Extending the image

If the base image(s) that are here do not contain an extension you need then you can base you own image from the ones built here.

To keep the final image size down we recommend building the php extension in an intermediate image and then copying that extension into the new image.

e.g. to add xml/xls support to the apache/debian production image

```dockerfile
FROM php:8.1-apache-buster AS php-base
RUN apt-get update
RUN apt-get install -y libxslt-dev libxml2-dev libssl-dev
RUN docker-php-ext-install -j$(nproc) xsl xml xmlrpc xmlwriter simplexml

FROM kimai/kimai2:apache
COPY --from=php-base /usr/local/etc/php/conf.d/docker-php-ext-xsl.ini /usr/local/etc/php/conf.d/docker-php-ext-xsl.ini
COPY --from=php-base /usr/local/lib/php/extensions/no-debug-non-zts-20190902/xsl.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902/xsl.so
```

Attention: the above is only an example.
