# Étape 1 : Utiliser l'image PHP officielle
FROM php:8.2-cli AS dev

# Définir le dossier de travail
WORKDIR /app

# Installer les dépendances système nécessaires
RUN apt-get update \
    && apt-get install -y \
        git \
        unzip \
        libicu-dev \
        libzip-dev \
        libpng-dev \
        libssl-dev \
        pkg-config \
        libcurl4-openssl-dev \
        curl

# Installer l'extension MongoDB pour PHP
RUN pecl install mongodb \
    && docker-php-ext-enable mongodb

# Installer d'autres extensions PHP utiles à Symfony
RUN docker-php-ext-install intl zip

# Installer Composer (récupéré depuis l'image officielle Composer)
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copier le code source du projet
COPY . .

# Installer les dépendances PHP avec Composer
RUN composer install

# Exposer le port pour le serveur Symfony (ou PHP built-in)
EXPOSE 8000

# Commande par défaut pour lancer le serveur Symfony
CMD ["php", "-S", "0.0.0.0:8000", "-t", "public"]