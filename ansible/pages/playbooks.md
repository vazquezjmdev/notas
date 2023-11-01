- #+BEGIN_EXAMPLE
  - host: web
     remote_user: ansible
     vars:
         http_port: 80
         items: [1,2,3,4]
     task:
     -  name: install nginx {{  http_port  }}
         apt:
              name: nginx
              state:  present
  
  #+END_EXAMPLE
- se ejecuta con ansible-paybook nginx.yaml
	- -C  -> para hacer simulaciones
	- -b -k -> pide la contraseña para ejecutar comandos con permisos administrativos altos
- #+BEGIN_EXAMPLE
  - host: web
     remote_user: ansible
     vars:
         http_port: 80
         items: [1,2,3,4]
     task:
     -  name: install nginx {{  http_port  }}
         apt:
              name: nginx
              state:  present
  
  #+END_EXAMPLE
- exampe.txt.j2
	-