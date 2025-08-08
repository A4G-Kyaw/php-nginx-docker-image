# Use official PHP image with FPM
FROM php:8.2-fpm

# Install system dependencies and PHP extensions as needed
RUN apt-get update && apt-get install -y \
    unzip \
    libzip-dev \
    && docker-php-ext-install zip pdo_mysql

# Install Composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set working directory inside container
WORKDIR /var/www/html

# Copy only composer files first, for dependency caching
COPY src/composer.json ./

# Install PHP dependencies
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# Copy rest of application files
COPY . .

# Give proper permissions
RUN chown -R www-data:www-data /var/www/html

