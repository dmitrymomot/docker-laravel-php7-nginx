# Lightweight PHP-FPM & Nginx Docker Image for Laravel
Based on [https://github.com/devgeniem/docker-wordpress](https://github.com/devgeniem/docker-wordpress) and removed WP specific items. 


[![License](https://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)


Mount your laravel project into:
```
/var/www/laravel
```

### Override project path
You can use `OVERRIDE_PROJECT_ROOT` variable to change project path with symlink.
Container creates a symlink from /var/www/project into `$OVERRIDE_PROJECT_ROOT` which allows us to use custom path.

## User permissions
You can use `WP_GID` and `WP_UID` env to change web user and group.

If these are not set container will look for owner:group from files mounted in `/var/www/laravel/public/`.

If these files are owned by root user or root group the container will automatically use 100:101 as permissions instead. This is so that we won't never run nginx and php-fpm as root.

### Email variables

```
SMTP_HOST
```

This variable changes the host where container tries to send mail from. By default this is docker host `172.17.0.1`.

```
SMTP_PORT
```

This variable changes the port where container tries to connect in order to send mail. By default this is `25`.

```
SMTP_TLS
```

If this is provided use username in authenticating to mail server. Default: null
```
SMTP_USER
```

If this is provided use password in authenticating to mail server. Default: null
```
SMTP_PASSWORD
```

If this is `on` mail will use username/password authentication in connections to smtp server.
This will automatically activate if you use `SMTP_USER` and `SMTP_PASSWORD`. Default: `off`
```
SMTP_AUTH
```

See more about these variables in [msmtp docs](http://msmtp.sourceforge.net/doc/msmtp.html#Authentication).

### PHP and Nginx Variables
You can change following env to change php configs:

```
# Variables and default values
PHP_MEMORY_LIMIT=128M
NGINX_MAX_BODY_SIZE=64M
NGINX_FASTCGI_TIMEOUT=30
```

## What's inside container:
### For running Laravel
- php7
- php-fpm7
- nginx

### For sending emails with smtp server
- msmtp
