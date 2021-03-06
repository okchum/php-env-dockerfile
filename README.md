# php-env-dockerfile

Some collections about how to custom your own perfect php image with official image.

## Official PHP images

[Official PHP on DockerHub](https://hub.docker.com/r/library/php/)


#### [PHP Repositories for Alpine](https://github.com/codecasts/php-alpine) - Codecasts (Recommended)

Codecasts implemented docker-php-ext-* commands well - which might be managed easily. Here below is an example from its readme.

```dockerfile
# Versions 3.8 and 3.7 are current stable supported versions.
FROM alpine:3.9

# trust this project public key to trust the packages.
ADD https://dl.bintray.com/php-alpine/key/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub

## you may join the multiple run lines here to make it a single layer

# make sure you can use HTTPS
RUN apk --update add ca-certificates

# add the repository, make sure you replace the correct versions if you want.
RUN echo "https://dl.bintray.com/php-alpine/v3.9/php-7.3" >> /etc/apk/repositories

# install php and some extensions
RUN apk add --update php
RUN apk add --update php-mbstring
RUN apk add --update php-you-extension-name-here
```

#### Available Packages

This is the complete available packages list:

| Package Name          | Type            |
| -                     | -               |
| `php`                 | PHP Core        |
| `php-common`          | PHP Core        |
| `php-fpm`             | PHP Core        |
| `php-cgi`             | PHP Core        |
| `php-apache2`         | PHP Core        |
| `php-doc`             | PHP Core        |
| `php-dev`             | PHP Core        |
|  -                    |                 |
| `php-sodium`          | Core Extension  |
| `php-bcmath`          | Core Extension  |
| `php-bz2`             | Core Extension  |
| `php-calendar`        | Core Extension  |
| `php-ctype`           | Core Extension  |
| `php-curl`            | Core Extension  |
| `php-dba`             | Core Extension  |
| `php-dom`             | Core Extension  |
| `php-embed`           | Core Extension  |
| `php-enchant`         | Core Extension  |
| `php-exif`            | Core Extension  |
| `php-ftp`             | Core Extension  |
| `php-gd`              | Core Extension  |
| `php-gettext`         | Core Extension  |
| `php-gmp`             | Core Extension  |
| `php-iconv`           | Core Extension  |
| `php-imap`            | Core Extension  |
| `php-intl`            | Core Extension  |
| `php-json`            | Core Extension  |
| `php-ldap`            | Core Extension  |
| `php-litespeed`       | Core Extension  |
| `php-mbstring`        | Core Extension  |
| `php-mcrypt`          | Core Extension  |
| `php-mysqli`          | Core Extension  |
| `php-mysqlnd`         | Core Extension  |
| `php-odbc`            | Core Extension  |
| `php-opcache`         | Core Extension  |
| `php-openssl`         | Core Extension  |
| `php-pcntl`           | Core Extension  |
| `php-pdo`             | Core Extension  |
| `php-pdo_dblib`       | Core Extension  |
| `php-pdo_mysql`       | Core Extension  |
| `php-pdo_pgsql`       | Core Extension  |
| `php-pdo_sqlite`      | Core Extension  |
| `php-pear`            | Core Extension  |
| `php-pgsql`           | Core Extension  |
| `php-phar`            | Core Extension  |
| `php-phpdbg`          | Core Extension  |
| `php-posix`           | Core Extension  |
| `php-pspell`          | Core Extension  |
| `php-session`         | Core Extension  |
| `php-shmop`           | Core Extension  |
| `php-snmp`            | Core Extension  |
| `php-soap`            | Core Extension  |
| `php-sockets`         | Core Extension  |
| `php-sqlite3`         | Core Extension  |
| `php-sysvmsg`         | Core Extension  |
| `php-sysvsem`         | Core Extension  |
| `php-tidy`            | Core Extension  |
| `php-wddx`            | Core Extension  |
| `php-xml`             | Core Extension  |
| `php-xmlreader`       | Core Extension  |
| `php-xmlrpc`          | Core Extension  |
| `php-xsl`             | Core Extension  |
| `php-zip`             | Core Extension  |
| `php-zlib`            | Core Extension  |
|  -                    |                 |
| `php-amqp`            | Extra Extension |
| `php-apcu`            | Extra Extension |
| `php-ast`             | Extra Extension |
| `php-ds`              | Extra Extension |
| `php-imagick`         | Extra Extension |
| `php-mailparse`       | Extra Extension |
| `php-memcached`       | Extra Extension |
| `php-mongodb`         | Extra Extension |
| `php-msgpack`         | Extra Extension |
| `php-psr`             | Extra Extension |
| `php-phalcon`         | Extra Extension |
| `php-redis`           | Extra Extension |
| `php-ssh2`            | Extra Extension |
| `php-swoole`          | Extra Extension |
| `php-timecop`         | Extra Extension |
| `php-libsodium`       | Extra Extension |
| `php-scalar_objects`  | Extra Extension |
| `php-secp256k1`       | Extra Extension |
| `php-xdebug`          | Extra Extension |
|  -                    |                 |
| `argon2`              | Extra Package   |
| `argon2-dev`          | Extra Package   |
| `libargon2`           | Extra Package   |
| `secp256k1`           | Extra Package   |


#### docker-php-ext-install/docker-php-ext-configure

Possible values for ext-name:

```
bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp hash iconv imap interbase intl json ldap mbstring mcrypt mysqli oci8 odbc opcache pcntl pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell readline recode reflection session shmop simplexml snmp soap sockets spl standard sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zip
```

Normally add text below in your docker file

```RUN docker-php-ext-install <your-ext-name1> <your-ext-name2>```

Like

```RUN docker-php-ext-install mysqli pdo pdo_mysql```




## Composer 

##### Alpine

```
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 
```

## IONCUBE

1. Check PHP info.

- PHP Version (It will decide which loader you have to choose on ionCube folder)
- extension_dir (For instance, `/usr/local/lib/php/extensions/no-debug-non-zts-20160303`)
- Scan this dir for additional .ini files (In this case, it's `/usr/local/etc/php/conf.d/`)

2. Download IONCUBE.

```
wget http://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz && tar xvfz ioncube_loaders_lin_x86-64.tar.gz && rm -rf ioncube_loaders_lin_x86-64.tar.gz
```

3. Update `zend_extension` on `ioncube.ini` file by using the value you checked.

4. Update 3 places on `Dockerfile` file with your value.
