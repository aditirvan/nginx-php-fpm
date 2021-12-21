# NGINX + PHP FPM

## Install NGINX + PHP FPM
```
sudo apt install nginx php-fpm
```
## Permission
```
sudo chown -R www-data:www-data /var/www/example.com/html/
sudo systemctl reload nginx
```
## NGINX Configuration
```
mkdir -p /var/www/example.com/html/
sudo nano /etc/nginx/sites-available/example.com
```
```
server {
	listen 80;
	root /var/www/test/html;
	index index.php index.html index.htm index.nginx-debian.html;
	server_name example.com www.example.com;
	access_log /var/log/nginx/example.access.log;
	error_log /var/log/nginx/example.error.log;

	location / {
		try_files $uri $uri/ =404;
	}

	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
	}

	location ~ /\.ht {
		deny all;
	}
}
```
```
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
```
```
sudo nginx -t
sudo systemctl restart nginx
```
Adhithia Irvan Rachmawan <adhithia.irvan@gmail.com>
