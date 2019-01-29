# PHP chroot bind

This utility can automatically mount resources into jailed chroots.

## Setup

Create `/etc/php-chroot-bind.conf` ([See example](php-chroot-bind.conf.example))

Copy php-chroot-bind to /usr/bin/php-chroot-bind

And set permission

```bash
sudo chmod +x /usr/bin/php-chroot-bind
```

## Usage

### Get a list with the active binds for each chroot.

```bash
sudo php-chroot-bind status
```

_The - in front of a bind path indicates that it is not bound to the chroot. To activate the binds run the script with parameter bind. This will create the necessary mountpounts and mount the bind paths read only to the chroot._

### To activate the binds

```bash
sudo php-chroot-bind bind
```

### Autobindind

The process of creating mountpoints, binding and unbinding can be configured to happen automatically during boot using systemd. To activate this run php-chroot-bind systemd create and reload systemd.

```bash
sudo php-chroot-bind systemd create
sudo systemctl daemon-reload
```

The unit files installed will handle the readonly binding as well as creating propper mountpoints if necessary.

To test, first unbind all active binds and remove created mountpoints.

```bash
php-chroot-bind unbind clean -do
```

Full docuementation goes to:

https://www.vennedey.net/resources/3-Secure-webspaces-with-NGINX-PHP-FPM-chroots-and-Lets-Encrypt#chroot_binds
