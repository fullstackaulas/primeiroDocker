# Usa uma imagem do PHP com FPM
FROM php:8.2-fpm

# Instala extensões necessárias para Laravel
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    unzip \
    git \
    curl \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql

# Instala o Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Define o diretório de trabalho
WORKDIR /var/www/html

# Copia os arquivos do Laravel
COPY . .

# Instala as dependências do Laravel
RUN composer install --no-dev --optimize-autoloader

# Define permissões
RUN chown -R www-data:www-data /var/www/html

# Expõe a porta do Laravel
EXPOSE 8000

# Inicia o servidor do Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]
