- Trabajar solo con claves
- Eliminar el acceso sin llaves
	- nano /etc/ssh/sshd_config
		- PasswordAuthentication no
- bloquear el acceso de root
	- nano /etc/ssh/sshd_config
		- PermitRootLogin yes/no
- sudo systemctl reload ssh.service
- sudo su -> para ser root
-
- firewall ubuntu
	- sudo ufw app list
	- sudo ufw allow "OpenSSH"
	- sudo ufw status verbose
	- sudo ufw enable
	- [[Ataques brutos]]
	- Bloqueo al acceso .git .htaccess
		- ficheros /etc/nginx/sites-avaliable
			- location ~ /\.ht {
			          deny all;
			          }
			- location ~ /\.git {
			          deny all;
			          }
		- Fichero a fichero
	- Ocultando la firma de nginx
		- /etc/nginx/nginx.conf
			- server_tokens off;
	- Eliminar ataques
		- #+BEGIN_EXAMPLE
		  #avoid iframes
		  add_header X-Frame-options SAMEORIGINS;
		  
		  #avoid mime
		  add_header X-Content-Type-Options nosniff;
		  
		  #avoid XSS
		  
		  add_header X-XSS-Protection "1; mode=block";
		  
		  # Refferrer policy
		  add_header Referrer-Policy "strict-origin-when-cross-origin";
		  
		  #+END_EXAMPLE
		- en los ficheros de configuracion
			-
		-
		-