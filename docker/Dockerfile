FROM wordpress:6.5.2-php8.3-apache
LABEL org.opencontainers.image.authors="soulteary@gmail.com"

# Refs:
#  - https://soulteary.com/2024/04/21/wordpress-sqlite-docker-image-packaging-details.html
#  - https://soulteary.com/2024/04/22/turn-wordpress-into-a-baas-service-a-guide-to-wp-api-calls.html

# WP CLI
# https://github.com/wp-cli/wp-cli/blob/5a91c54f1ced8fac5486181bfd805083b22b7c96/php/WP_CLI/Runner.php#L1073C48-L1073C65
ENV WP_CLI_ALLOW_ROOT=1
RUN apt update && apt install -y less && apt clean
RUN curl -L -o "wp-cli.phar" https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp

# WP REST API
RUN echo "# Enable WP REST API, by @soulteary" >> /usr/src/wordpress/wp-config-docker.php
RUN echo "if ( ! defined( 'REST_REQUEST' ) ) { define('REST_REQUEST', true); }" >> /usr/src/wordpress/wp-config-docker.php
