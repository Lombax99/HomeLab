
Installed on linux machine following this tutorial: https://www.youtube.com/watch?v=fpr37FJSgrw

To have a TLS certificate for a Domain Name that point to a lan address i decided to use Nginx and let's encrypt to do it since certbot cannot.

To do that i need to move nexcloud (apache2) to a different port so that nginx can have the 80 and 443.

1) Edit Apache port configuration:
```shell
sudo nano /etc/apache2/ports.conf
```

change to `Listen 8080`

2) Edit the VirtualHost for Nextcloud: