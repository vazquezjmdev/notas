- docker stats
- docker info
-
- Memoria
	- -m o --memory
	- --memory-swap
	- --memory-swappiness (1-100)
	- --memory-reservation
	- --kernel-memory (ojo )
	- --oom-kill-disable -ojo para fijar un contonedor que sea el ultimo en eliminar
- stress -m 2 --vm-bytes 100m --vm-keep
- stress -m 2 --vm-bytes 100m --vm-keep
- CPU
	- cpu scheduler css
	- --cpus="1.5" -> cpu y media para este container
		- --cpu-period=10000
		- --cpu-quoata
	- --cpuset-cpus 0-3 que cpu usa
	- --cpu-shares (unidades igual que vmware)
	-
- Almacenamiento
	- docker info
	- lsblk
	- copia de /var/lib/docker
	- sudo cp -r /var/lib/docker /var/lib/docker.viejo
	- sudo zpool create -f zpol-docker -m /var/lib/docker /dev/sdb
	- sudo rm -rf /var/lib/docker
	- informar drv
		- /etc/docker/daemon.json
			- informar en ese fichero
			  #+BEGIN_EXAMPLE
			  {
			  "storage-driver": "zfs"
			  }
			  #+END_EXAMPLE
	-
	-
	-
-