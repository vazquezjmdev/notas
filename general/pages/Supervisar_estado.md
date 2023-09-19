- Buenas practicas
	- Supervisar la presencia de un puerto de escucha.
	- Supervisar la presencia de un archivo.
	- Realizar una conexión HTTP.
	- Conectarse a una base de datos.
	- Acceder a una página de
	  diagnóstico.
- Monitoreo de un contenedor
	- readiness
		- iniciado
		- listas las dependencias
		- fallo se elimina del trafico pero no se borra
	- liveness
		- se puede utilizar
		- tiene suficiente memoria
		- responde a tiempo
		- fallo se detiene y es sustituido por uno nuevo
	- otra al iniciar es el startpProbe
	- Pruebas
		- liveness
			- tiene que ser independiente. solo sobre el contendor actual
				- la memoria
				- no por ejemplo la conexion a una db
			- readiness
				- verifica que la aplicacion funciona correctamente
			- statupProbe
				- dejar tiempo necesario para las pruebas
	- Estructura de los campos de supervision
		- deployment --> spec --> template --> spec --> contenedors
			- startupProbe, readinessProbe y livenessProbe
		- #+BEGIN_EXAMPLE
		   exec: comando para ejecutar en el contenedor.
		   failureThreshold: número de errores antes de considerar que hay un 
		   problema (predeterminado = 3).
		    httpGet: estructura que define la prueba HTTP que hay que realizar.
		    initialDelaySeconds: tiempo inicial antes de iniciar las pruebas.
		    periodSeconds: tiempo de espera en segundos entre cada prueba 
		    (por defecto, 10 segundos).
		    successThreshold: número de pruebas consecutivas para 
		    considerar que un contenedor está OK (por defecto, 1).
		    tcpSocket: verificación de la presencia de un puerto de escucha.
		    timeoutSeconds: tiempo en segundos que debe durar una prueba 
		    (por defecto, 1).
		  #+END_EXAMPLE
		- #+BEGIN_EXAMPLE
		  apiVersion: apps/v1 
		  kind: Deployment 
		  metadata: 
		     labels: 
		       app: mailhog 
		     name: mailhog 
		  spec: 
		     replicas: 1 
		     selector: 
		       matchLabels: 
		         app: mailhog 
		     template: 
		       metadata: 
		         labels: 
		           app: mailhog 
		       spec: 
		         contenedors: 
		       -   image: mailhog/mailhog 
		           name: mailhog 
		           readinessProbe: 
		             tcpSocket: 
		               port: 1025 
		           livenessProbe: 
		             tcpSocket: 
		               port: 8025
		  #+END_EXAMPLE
		-
-
-