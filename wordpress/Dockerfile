FROM debian:12-slim

LABEL maintainer="ray@agimon.com"
LABEL org.opencontainers.image.source="https://github.com/Agimon-LLC/homelab-images"

# Update + install base dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates curl tar unzip supervisor \
    nginx php8.2-fpm php8.2-mysql php8.2-gd php8.2-xml php8.2-curl \
    php8.2-zip php8.2-mbstring php8.2-intl php8.2-soap \
    php8.2-bcmath php8.2-imagick php8.2-cli \
 && update-ca-certificates \
 && rm -rf /var/lib/apt/lists/*

# Download and install WordPress
RUN curl -fsSL -o /tmp/wordpress.tar.gz https://wordpress.org/latest.tar.gz \
 && tar -xzf /tmp/wordpress.tar.gz -C /var/www/html --strip-components=1 \
 && rm /tmp/wordpress.tar.gz

# Permissions
RUN chown -R www-data:www-data /var/www/html

# Copy configs
COPY nginx.conf /etc/nginx/sites-available/default
COPY php-fpm.conf /etc/php/8.2/fpm/php-fpm.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80
CMD ["/usr/bin/supervisord", "-n"]
