**Install Nginx**: Ensure Nginx is installed and running.
```
sudo apt update
sudo apt install nginx

```

**Configure the Domain**: Create a new configuration file for your domain.
```
sudo nano /etc/nginx/sites-available/asr-al-arqam.com

```
**Add the Basic Configuration**: Add the following configuration to the file:
```
server {
    listen 80;
    server_name asr-al-arqam.com www.asr-al-arqam.com;

    location / {
        root /var/www/html;
        index index.html index.htm;
    }

    # Redirect all HTTP requests to HTTPS
    location /.well-known/acme-challenge/ {
        allow all;
        root /var/www/html;
    }
}

```

**Enable the Site Configuration**: Link the configuration file to `sites-enabled` and test the configuration.
```
sudo ln -s /etc/nginx/sites-available/asr-al-arqam.com /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx

```

**Obtain an SSL Certificate**: Use Certbot to obtain an SSL certificate from Let's Encrypt. Install Certbot:
```
sudo apt install certbot python3-certbot-nginx

```
Obtain the SSL certificate:
```
sudo apt install certbot python3-certbot-nginx

```
**Configure Nginx to Use SSL**: Certbot will automatically configure Nginx to use the obtained SSL certificate. Ensure the configuration includes the following:

```
server {
    listen 80;
    server_name asr-al-arqam.com www.asr-al-arqam.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name asr-al-arqam.com www.asr-al-arqam.com;

    ssl_certificate /etc/letsencrypt/live/asr-al-arqam.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/asr-al-arqam.com/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    location / {
        root /var/www/html;
        index index.html index.htm;
    }
}

```

```
sudo nginx -t
sudo systemctl restart nginx

```

Since the `index.html` file does not exist in the `/var/www/html` directory, you need to create it. Here's how you can do that, along with ensuring proper permissions and configuration:
```
sudo mkdir -p /var/www/html
echo '<html><body><h1>Welcome to asr-al-arqam.com!</h1></body></html>' | sudo tee /var/www/html/index.html

```
**Set Proper Permissions**:
```
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html

```
**Verify and Reload Nginx Configuration**:
```
sudo nginx -t
sudo systemctl reload nginx

```

```
# Redirect all HTTP requests to HTTPS
server {
    listen 80;
    server_name asr-al-arqam.com www.asr-al-arqam.com;

    location /.well-known/acme-challenge/ {
        root /var/www/html;
        allow all;
    }

    location / {
        return 301 https://$host$request_uri;
    }
}

# HTTPS server block
server {
    listen 443 ssl;
    server_name asr-al-arqam.com www.asr-al-arqam.com;

    root /var/www/html;
    index index.html index.htm;

    ssl_certificate /etc/letsencrypt/live/asr-al-arqam.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/asr-al-arqam.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

    location / {
        try_files $uri $uri/ =404;
    }

    location /.well-known/acme-challenge/ {
        root /var/www/html;
        allow all;
    }
}

```