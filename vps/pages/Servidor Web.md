- sudo apt install nginx
- /etc/nginx
- sites-available\
	- cp default sagibus.eu
		- root /var/www/sagibus.com;
		- server_name sagibus.eu;
	- sudo ln /etc/nginx/sites-available/sagibus.eu /etc/nginx/sites-enabled/
- sudo nginx -t
	-
- Habilitar gzip
	- en nginx.conf
		- #+BEGIN_EXAMPLE
		  gzip on;
		  
		          gzip_vary on;
		          #gzip_proxied any;
		          gzip_comp_level 6;
		          gzip_buffers 16 8k;
		          gzip_http_version 1.1;
		          gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
		  
		  #+END_EXAMPLE
- DOS
	- /etc/nginx/snippets/dos-protection.conf
		- #+BEGIN_EXAMPLE
		  ##
		  # DoS and DDoS Protection Settings
		  ##
		  
		  #Define limit connection zone called conn_limit_per_ip with memory size 15m based on the un$
		  limit_conn_zone $binary_remote_addr zone=conn_limit_per_ip:15m;
		  
		  #Define limit request to 40/sec in zone called req_limit_per_ip memory size 15m based on IP
		  limit_req_zone $binary_remote_addr zone=req_limit_per_ip:15m rate=40r/s;
		  
		  #Using the zone called conn_limit_per_ip with max 40 connections per IP
		  limit_conn conn_limit_per_ip 40;
		  
		  #Using the zone req_limit_per_ip with an exceed queue of size 40 without delay for the 40 a$
		  limit_req zone=req_limit_per_ip burst=40 nodelay;
		  
		  #Do not wait for the client body or headers more than 5s (avoid slowloris attack)
		  client_body_timeout 5s;
		  client_header_timeout 5s;
		  send_timeout 5;
		  
		  #Establishing body and headers max size to avoid overloading the server I/O
		  client_body_buffer_size 256k;
		  client_header_buffer_size 2k;
		  client_max_body_size 3m;
		  large_client_header_buffers 2 2k;
		  #+END_EXAMPLE
- Evitar secuestros en sitios nginx
	- en \sagibus.eu en sitio por default y ojo con server_name
		- Añadimos
		- #+BEGIN_EXAMPLE
		  server {
		          listen 80 default_server;
		          listen [::]:80 default_server;
		          server_name _;
		  
		          return 301 http://sagibus.eu;
		          #para si el sitio por defecto fuera la www
		          #return 301 http://www.sagibus.eu;
		  #+END_EXAMPLE
		- y
			- #+BEGIN_EXAMPLE
			          server_name sagibus.eu;
			  
			          #server_name www.sagibus.eu;
			  
			  #+END_EXAMPLE