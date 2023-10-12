- fichero = open('fichero.txt', 'w/r/a')
- fichero.write(texto)
- fichero.close()
- leer todo el fichero
	- fichero = open('fichero.txt','r' )
	      texto = fichero.read()
	      fichero.close()
- Leer en una lista linea -> elemento de la lista
	- fichero = open('fichero.txt','r')
	      lineas= fichero.readlines()
	      fichero.close()
- Añadir una linea
	- fichero = open('fichero.txt','a')
	- fichero.write('\ntercera linea\n')
- Leer una linea segun la posicion de puntero
	- fichero = open('fichero.txt','r')
	- l = fichero.readline()
- Apertura y procesado de fichero
	- with open('fichero.txt','r') as fichero:
	          for linea in fichero:
	              print(linea)
- Manejar el puntero
	- with open('fichero.txt','r') as fichero:
	          fichero.seek(15)
	          posicion10 = fichero.read()
	          print(posicion10)
	- fichero.seek(0) -> principio
	- fichero.read(5) -> los 5 primeros caracteres
	- fichero.seek( len(fichero.readline() ))
- Escribir en el principio del fichero
	- fichero = open('fichero.txt', 'r+')
- Modificar la tercera linea
	- fichero = open('fichero.txt', 'r+')
	- lineas = fichero.readlines()
	- lineas[2] = "linea a modficar\n"
	- fichero.seek(0)
	- fichero.writelines(lineas)
-
	-