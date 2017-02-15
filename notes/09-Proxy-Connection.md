# Proxy Connection for Tomcat

- For proxy we are using Nginx, so let us install nginx

> While installing nginx I got issue with "libunwind" package. So I've manually downloaded that package and installed it.

```
# wget ftp://195.220.108.108/linux/centos/7.3.1611/os/x86_64/Packages/libunwind-1.1-5.el7_2.2.x86_64.rpm && rpm -ivh libunwind-1.1-5.el7_2.2.x86_64.rpm

# yum install nginx -y
```

- Now for our default configuration files let us have a directory

```
# cd /etc/nginx
# mkdir vhosts.d
```

- Now we need to change the configuration as per our requirement
	- Find the include statement for the config files and add another for our new directory
	- After that remove the server definition under the include statement as we'll have it in our new config

```
# vi nginx.conf

	include /etc/nginx/vhost.d/*.conf;
```

- Now lets go to the ***vhost.d*** directory and create a new config file
	- Copy the sample server definition after deleting the existing server definition in the main config file
	- Paste it in the new config file and modify as per your requirements
	- Else use the below

	```
	server {
        	listen 80;

        	root /opt/tomcat8/webapps/hello/;
        	index index.php index.html index.htm;

        	server_name localhost;

        	location / {
                	try_files $uri $uri/ /index.php;
        	}

        	location ~ \.php$ {
        	        proxy_set_header X-Real-IP $remote_addr;
        	        proxy_set_header X-Forwarded-For $remote_addr;
        	        proxy_set_header Host $host;
        	        proxy_pass http://127.0.0.1:8080;
        	}
	
	        location ~ /\.ht {
	                deny all;
	        }
	}

	```

```
# cd vhost.d/
# vi default.conf

server {
	listen 80;

	root /opt/tomcat8/webapps/hello/;
	index index.php index.html index.htm;

	server_name localhost;

	location / {
		try_files $uri $uri/ /index.php;
	}

	location ~ \.php$ {
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $remote_addr;
		proxy_set_header Host $host;
		proxy_pass http://127.0.0.1:8080;
	}

	location ~ /\.ht {
		deny all;
	}
}
```

- Start ***Nginx***

- Verify that you are able to hit the webapps/hello without any issue.

```
# elinks http://localhost
```
