- kubectl port-forward
- ```
  minikube addons enable ingress
  ```
- kubectl -n ingress-nginx get pods -l app.kubernetes.io/name
- #+BEGIN_EXAMPLE
  apiVersion: networking.k8s.io/v1 
  kind: Ingress 
  metadata: 
    name: mailhog 
  spec: 
    rules: 
    - http: 
        paths: 
        - path: / 
          pathType: Prefix 
          backend: 
            service: 
              name: mailhog 
              port: 
                number: 8025 
  
  #+END_EXAMPLE
-
- ## Trampas para multiples rutas
	- #+BEGIN_EXAMPLE
	  Cuando tiene una dirección IP de este tipo, es posible pasar una dirección formada por la dirección IP, seguida del nombre de dominio nip.io. En el caso de la dirección IP 192.168.122.67, este dominio será 192.168.122.67.nip.io.
	  
	  El funcionamiento de nip.io es el siguiente: durante una consulta de DNS, este último va a recuperar la dirección IP anterior nip.io y la devolverá.
	  
	  Este mecanismo se aplica a la dirección raíz (192.168.122.67.nip.io), así como a todos los subdominios (mailhog.192.168.122.67.nip.io, por ejemplo).
	  #+END_EXAMPLE
-
-