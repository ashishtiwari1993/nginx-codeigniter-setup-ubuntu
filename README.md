# nginx-ci-conf

Step1: Download CodeIgniter latest version from here https://codeigniter.com/download .

Step2: Extract CodeIgniter and place it here '/var/www/html/ci' .

Step3: Go to 'cd /etc/nginx/sites-available/' . 

Step4: Create file with your domain name like 'yourdomain.com' and copy below content. Replace your domain name.

	server {
		listen 80;
		listen [::]:80;


		root /var/www/html/ci;

		autoindex on;
		index index.php index.html index.htm index.nginx-debian.html;

		server_name yourdomain.com;

		location / {
			# First attempt to serve request as file, then
			# as directory, then fall back to displaying a 404.
			try_files $uri $uri/ /index.php;
		}

		location ~ \.php$ {
			include snippets/fastcgi-php.conf;
			fastcgi_pass unix:/run/php/php7.0-fpm.sock;
		}

		location ~ /\.ht {
			deny all;
		}
	}

Step5: Restart your Nginx server with 'systemctl restart nginx.service' and hit 'yourdomain.com' in browser. You should able to see codeIgniter index page.
 
