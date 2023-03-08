ARG VERSION_PHP=${VERSION_PHP}

FROM php:${VERSION_PHP} as base

RUN apt-get update && apt-get install -y \
    libpq-dev

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pgsql pdo_pgsql pdo_mysql mysqli

ARG DOCKER_UID=${DOCKER_UID}
ARG DOCKER_GID=${DOCKER_GID}
ARG DOCKER_USER=${DOCKER_USER}

RUN groupadd -g ${DOCKER_GID} ${DOCKER_USER}
RUN useradd -u ${DOCKER_UID} -ms /bin/bash -g ${DOCKER_GID} ${DOCKER_USER}

USER ${DOCKER_USER}


FROM base as development

COPY DockerFiles/Php/conf/zz-docker.conf /usr/local/etc/php-fpm.d/zz-docker.conf


FROM base as production

COPY DockerFiles/Php/conf/zz-docker.conf /usr/local/etc/php-fpm.d/zz-docker.conf