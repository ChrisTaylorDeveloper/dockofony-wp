ARG WP_IMAGE_TAG=CHANGEME
FROM wordpress:${WP_IMAGE_TAG}

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        git \
        zip \
        unzip \
    && rm -rf /var/lib/apt/lists/*sdf

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
