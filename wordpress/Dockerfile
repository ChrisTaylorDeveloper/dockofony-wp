ARG WP_IMAGE_TAG=CHANGEME
FROM wordpress:${WP_IMAGE_TAG}

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        git \
        zip \
        unzip \
    && rm -rf /var/lib/apt/lists/*sdf

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ARG XDEBUG=false
RUN if [ "${XDEBUG}" = true ]; then \
        pecl install xdebug && docker-php-ext-enable xdebug; \
        { \
            echo "[xdebug]"; \
            echo "xdebug.mode=develop,debug,coverage"; \
            echo "xdebug.discover_client_host = true"; \
            echo "xdebug.client_host=172.17.0.1"; \
            echo "xdebug.client_port = 9003"; \
            echo "xdebug.max_nesting_level = 512"; \
            echo "xdebug.start_with_request=yes"; \
            echo "xdebug.log=/var/log/xdebug.log"; \
        } >> "$PHP_INI_DIR"/conf.d/xdebug.ini; \
        touch /var/log/xdebug.log && chmod 777 /var/log/xdebug.log \
    ;fi
