# php-env-dockerfile

Some collections about how to custom your own perfect php image with official image.

## Official PHP images

[Official PHP on DockerHub](https://hub.docker.com/r/library/php/)

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
