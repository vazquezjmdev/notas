- ps
	- ```
	  ps -u eni -o pid,state,command
	  ```
- vmstat
- mpstat cpus
- free
- Vaciar cachee
- ```
  sync ; echo 3 > /proc/sys/vm/drop_caches
  ```
-
- Los siguientes comandos son útiles
  para el swap:
	- mkswap: «formatear» la partición de intercambio.
	- swapon: activar el swap.
	- swapoff: desactivar el swap.
	- cat /proc/swaps: detallar la ocupación por partición swap.
- df /
	- -Th /
	- -i /
- du /etc
- iostat
- lsof -i
	- -ni tcp:25
	- -ni @192.168.0.1:25
	- -i -a -p 1234
	- -u 1000
	-
-
-
-
	-
	-
-