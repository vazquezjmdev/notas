- Compose solo para local y desarollo
- kb get nodes
- .kube/
	- kb config current-context
	- kb get-contexts
	- kb config use-context
	- azure
		- az aks get-credential ....
- kb  run hello-world --image helloword
- kb delete pod name_pod
- kb get namespaces
- kb get pods -n kube-system
- kb run name --image --restart Never -> si cae no se reinicia cosa configurada por defecto
- kb describe pod patata -> ver lo que pasa
- kb logs name_pod -f  --tail=2 -> log de contenedores del pod (-c container)
- kb  port-forward nginx 8.8.8.8 ->80
- kb run bb -it --image busybox ->ayuda tipico para colocarnos
	- vget ..
- kb set image cambia que imagen el pod y se reinica el contenedor
- estados de un pod
	- desalojado
	- finalizado con error
	- pending pendiente de ejecuta
	- running
	- succeded contendor ejecutado
	- failes (cascado)
- kb get pods columna estado -> mezcla estado del pod con el contendor (ver running y el contendor se esta reiniciando)
- la ip es anivel pod
- En kb el contenedor no tiene ip
- localhost
	- dk es el contnedor
	- kb  es el pod
- kb exect -it nginx --/bin/sh -> entro a un contenedor
-
-
-
-
-
-
	-
	-
	-