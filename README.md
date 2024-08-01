# Poste.io plugin for Dokku 

### What makes this repo different?

While the original Poste.io is meant to be run as an appliance (taking up the whole server and IP), this will run Poste.io as a dokku plugin and have other services running on the same dokku instance besides Poste.io.

In this instance spamd and clamav are disabled by default, roundcube is enabled.

### What is Poste.io?

Poste.io is an full featured email server running in a docker container. Read more at the [poste.io](https://poste.io/) website.
It supports wildcard aliases and has full Gmail support.

### What is Dokku?

[Dokku](http://dokku.viewdocs.io/dokku/) is the smallest PaaS implementation
you've ever seen - _Docker powered mini-Heroku_.

### Requirements
* A working [Dokku host](http://dokku.viewdocs.io/dokku/getting-started/installation/)

# Setup

**Note:** We are going to use the domain `mail.example.com` for demonstration
purposes. Make sure to replace it to your domain name.

## Download plugin
Log onto your Dokku Host as `root` and install plugin:
```bash
dokku plugin:install https://github.com/allanlaal/dokku-plugin-posteio-service.git
```

## Domain name
Next setup domain name for posteio using your normal `dokku` user:

```bash
dokku posteio:set-domain mail.example.com
```

## Start container
To start using Poste.io you need to start his docker container:

``` bash
dokku posteio:start
```

**Note:**
You can disable features by passing these optional parameters to the start command:
- `--disable-clamav` to disable clamAV, it's useful to reduce memory usage if you don't need an antivirus protection.
- `--disable-rspamd` to disable Rspamd, it's useful to reduce memory usage if you don't want a spam filtering system.
- `--disable-roundcube` to disable the Roundcube webmail interface.
also the other way around works:
- `--enable-clamav`
- `--enable-rspamd`
- `--enable-roundcube`

## SSL Certificate

You will need to access Poste.io dashboard certificate page by going to:
```
System Settings > TLS Certificate
```
Or directly by accessing this url:
```
http://mail.example.com/admin/settings/#certificate
```

Now click on issue new certificate or choose existing one, after this tell plugin you enabled SSL by:
```bash
dokku posteio:toggle-ssl
```

## Wrapping up

Your Poste.io instance should now be available and secure on [https://mail.example.com](https://mail.example.com).
