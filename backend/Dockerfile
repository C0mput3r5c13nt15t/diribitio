FROM php:8.0-apache

RUN apt-get update && apt-get upgrade -y

# Install git
RUN apt-get install -y git

# Update and install ... stuff ?
RUN apt-get update && apt-get install -y \
        libpng-dev \
        zlib1g-dev \
        libxml2-dev \
        libzip-dev \
        libonig-dev \
        zip \
        curl \
        unzip

# Enable php pdo_mysql
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Install php-redis
RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

# Configure apache
COPY apache.conf /etc/apache2/sites-available/inpriparo.conf

# Enable the rewrite module (needed for Laravel)
RUN a2enmod rewrite

# Apply Apache configuration
RUN a2ensite inpriparo.conf
RUN a2dissite 000-default.conf
RUN service apache2 restart

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && php composer-setup.php --install-dir=/usr/local/bin --filename=composer && php -r "unlink('composer-setup.php');"

# Set the working directory
WORKDIR /var/www/

# Clone the GitHub repo
RUN git clone https://github.com/C0mput3r5c13nt15t/Inpriparo.git

# Set the working directory to the root of the application
WORKDIR /var/www/Inpriparo

# Install the necessary dependecies for laravel
RUN composer install --no-dev

# Setup permissions
RUN chmod 777 -R storage/

# Copy the larevel .env file
COPY laravel.env .env

# Generate laravel application key
RUN php artisan key:generate

