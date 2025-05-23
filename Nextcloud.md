
Installed on linux machine following this tutorial: https://www.youtube.com/watch?v=fpr37FJSgrw

---

To have a TLS certificate for a Domain Name that point to a lan address i decided to use Nginx and let's encrypt to do it since certbot cannot.

To do that i need to move nexcloud (apache2) to a different port so that nginx can have the 80 and 443.

1) Edit Apache port configuration:
```shell
sudo nano /etc/apache2/ports.conf
```

change to `Listen 8080`

2) Edit the VirtualHost for Nextcloud:
```shell
sudo nano /etc/apache2/sites-available/nc-server.conf
```

change to `<VirtualHost *:8080>`

----

setup nginx with docker compose:

```yaml
services:
  nginx-proxy-manager:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'        # HTTP
      - '81:81'        # Admin UI
      - '443:443'      # HTTPS
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

On nginx admin UI i set up a 



and a Proxy Host

![[Pasted image 20250523163020.png]]
![[Pasted image 20250523163040.png]]
