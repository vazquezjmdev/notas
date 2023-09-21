- Repaso
	- -o wide ->ampliado
	- describe
	- kubectl get deployment mailhog -o yaml
	  kubectl edit deployment mailhog
	- export EDITOR=vi
	- watch kubectl get pods
	  kubectl logs -c nombre contenedor
	- kubectl port-forward mailhog-5dbc9c86c4-gsbk6 8025
	  kubectl port-forward deployment/mailhog 8025
	-
- ### Esqueleto para un despliegue
	- kubectl create deployment mailhog --image mailhog/mailhog --dry-run=client -o yaml
- ### Aplicar
	- kubectl apply -f mailhog-deployment.yaml
- ### Eliminar
	- kubectl delete -f mailhog-deployment.yaml
- ### Idempotencia
	- en el campo metadatos, eliminación del subcampo creationTimestamp,
	- en el campo spec, eliminación de los subcampos strategy y ressources,
	- eliminación del campo status.
- ### Crear un servicio
	- kubectl expose deployment/mailhog --dry-run=client--port 1025,8025 -o yaml
	- limpieza
		- Al igual que para el despliegue, la reentrada
		  no se gestiona correctamente si dejamos el campo createTimestamp. El campo status tampoco es necesario y, por
		  lo tanto, se eliminará.
	- ### Mecanismo de selector y etiquetas
		- kubectl get pods -l app=mailhog
- ### Agrupar elementos
	- kubectl apply -f ./mailhog
	- kubectl get -f ./mailhog
	-
- ## Estructura de los objetos
	- kubectl explain
		- service
		- pod
		- deployment