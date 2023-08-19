FROM mcr.microsoft.com/vscode/devcontainers/php:0-8

# Install PHP extensions
RUN docker-php-ext-install pdo pdo_mysql

# Install and configure MariaDB
RUN apt-get update && apt-get install -y mariadb-server mariadb-client
RUN echo "mysql-server mysql-server/root_password password YOUR_ROOT_PASSWORD" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password YOUR_ROOT_PASSWORD" | debconf-set-selections

# Install phpMyAdmin
RUN apt-get install -y phpmyadmin
RUN phpenmod mysqli

# Set up web directory
WORKDIR /workspace/web
COPY index.php .

# Expose MySQL and phpMyAdmin ports
EXPOSE 3306 80

# Start services (MariaDB, Apache, and PHP)
CMD ["bash", "-c", "service mysql start && service apache2 start && php -S 0.0.0.0:8080"]
