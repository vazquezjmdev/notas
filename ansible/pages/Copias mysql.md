- Un playbook de Ansible para realizar copias de seguridad de una base de datos MySQL podría verse de la siguiente manera. Este playbook asume que tienes Ansible instalado en tu sistema y que ya tienes configuradas las credenciales de acceso a tu servidor MySQL. Asegúrate de personalizar las variables y los nombres de los archivos de copia de seguridad según tus necesidades:
- #+BEGIN_EXAMPLE
  ---
  - name: Crear copia de seguridad de MySQL
    hosts: tu_servidor_mysql
    gather_facts: no
  
    tasks:
      - name: Crear directorio de copias de seguridad
        file:
          path: /ruta/a/tu/directorio_de_copias
          state: directory
        become: yes
  
      - name: Obtener la fecha actual
        command: date +"%Y%m%d%H%M%S"
        register: fecha_actual
        changed_when: false
        become: yes
  
      - name: Crear copia de seguridad de la base de datos MySQL
        command: mysqldump -u usuario_mysql -p{{ tu_password_mysql }} nombre_de_la_base_de_datos > /ruta/a/tu/directorio_de_copias/backup_{{ fecha_actual.stdout }}.sql
        become: yes
  
      - name: Comprimir la copia de seguridad
        command: gzip /ruta/a/tu/directorio_de_copias/backup_{{ fecha_actual.stdout }}.sql
        become: yes
  
      - name: Eliminar copias de seguridad antiguas
        find:
          paths: /ruta/a/tu/directorio_de_copias
          age: 1d
          recurse: yes
          match: "*.sql.gz"
        register: copias_antiguas
        become: yes
  
      - name: Borrar copias de seguridad antiguas
        file:
          path: "{{ item.path }}"
          state: absent
        with_items: "{{ copias_antiguas.files }}"
        when: copias_antiguas.matched > 7
        become: yes
  #+END_EXAMPLE
- Asegúrate de personalizar las siguientes partes del playbook:
- `tu_servidor_mysql`: Cambia esto al nombre o la IP de tu servidor MySQL.
- `usuario_mysql` y `tu_password_mysql`: Sustituye estos valores por las credenciales de acceso a tu servidor MySQL.
- `nombre_de_la_base_de_datos`: Reemplaza esto por el nombre de la base de datos de la que deseas realizar copias de seguridad.
- `/ruta/a/tu/directorio_de_copias`: Sustituye esta ruta por la ubicación donde deseas almacenar las copias de seguridad.
- `7` en la tarea "Borrar copias de seguridad antiguas" se utiliza para mantener las últimas 7 copias de seguridad y eliminar las antiguas. Puedes ajustar este valor según tus necesidades.
- Este playbook crea una copia de seguridad de la base de datos MySQL, la comprime y elimina copias de seguridad antiguas para mantener un número determinado de copias de seguridad recientes. Asegúrate de tener las dependencias necesarias, como `mysqldump` y `gzip`, instaladas en tu servidor. Además, ten en cuenta las consideraciones de seguridad al manejar las contraseñas de MySQL en tu playbook.
-
- Si deseas realizar copias de seguridad en varios servidores MySQL con direcciones IP diferentes, puedes modificar el playbook anterior para que funcione en un entorno con varios hosts. Para hacerlo, puedes utilizar un archivo de inventario de Ansible que enumere los servidores MySQL y sus respectivas direcciones IP. Aquí tienes una versión actualizada del playbook:
  
  ```yaml
  ---
  - name: Crear copias de seguridad de MySQL
    hosts: servidores_mysql
    gather_facts: no
  
    tasks:
      - name: Crear directorio de copias de seguridad
        file:
          path: /ruta/a/tu/directorio_de_copias
          state: directory
        become: yes
  
      - name: Obtener la fecha actual
        command: date +"%Y%m%d%H%M%S"
        register: fecha_actual
        changed_when: false
        become: yes
  
      - name: Crear copias de seguridad de las bases de datos MySQL
        command: mysqldump -u usuario_mysql -p{{ tu_password_mysql }} {{ item.database }} > /ruta/a/tu/directorio_de_copias/backup_{{ fecha_actual.stdout }}_{{ item.host }}.sql
        with_items: "{{ bases_de_datos }}"
        become: yes
  
      - name: Comprimir las copias de seguridad
        command: gzip /ruta/a/tu/directorio_de_copias/backup_{{ fecha_actual.stdout }}_{{ item.host }}.sql
        with_items: "{{ bases_de_datos }}"
        become: yes
  
      - name: Eliminar copias de seguridad antiguas
        find:
          paths: /ruta/a/tu/directorio_de_copias
          age: 1d
          recurse: yes
          match: "*.sql.gz"
        register: copias_antiguas
        become: yes
  
      - name: Borrar copias de seguridad antiguas
        file:
          path: "{{ item.path }}"
          state: absent
        with_items: "{{ copias_antiguas.files }}"
        when: copias_antiguas.matched > 7
        become: yes
  
  # Define los servidores MySQL y sus bases de datos aquí
  vars:
    bases_de_datos:
      - { host: 192.168.1.1, database: nombre_de_la_base_de_datos_1 }
      - { host: 192.168.1.2, database: nombre_de_la_base_de_datos_2 }
      # Agrega más servidores y bases de datos según sea necesario
  ```
  
  En este playbook, hemos definido un grupo de hosts llamado `servidores_mysql`, y cada servidor MySQL y su respectiva base de datos se especifican en la variable `bases_de_datos`. Puedes agregar tantos servidores y bases de datos como necesites en esta variable.
  
  Asegúrate de actualizar las direcciones IP, nombres de bases de datos, usuarios y contraseñas de MySQL en la variable `bases_de_datos` de acuerdo con tu entorno. Además, personaliza la ruta de almacenamiento de copias de seguridad y la cantidad de copias a mantener, según tus necesidades.
- Si deseas almacenar las copias de seguridad en directorios diferentes para cada servidor MySQL, puedes ajustar el playbook de la siguiente manera:
  
  ```yaml
  ---
  - name: Crear copias de seguridad de MySQL
    hosts: servidores_mysql
    gather_facts: no
  
    tasks:
      - name: Obtener la fecha actual
        command: date +"%Y%m%d%H%M%S"
        register: fecha_actual
        changed_when: false
        become: yes
  
      - name: Crear directorio de copias de seguridad para el servidor
        file:
          path: "/ruta/a/tu/directorio_de_copias/{{ item.host }}"
          state: directory
        with_items: "{{ bases_de_datos }}"
        become: yes
  
      - name: Crear copias de seguridad de las bases de datos MySQL
        command: mysqldump -u usuario_mysql -p{{ tu_password_mysql }} {{ item.database }} > "/ruta/a/tu/directorio_de_copias/{{ item.host }}/backup_{{ fecha_actual.stdout }}.sql"
        with_items: "{{ bases_de_datos }}"
        become: yes
  
      - name: Comprimir las copias de seguridad
        command: gzip "/ruta/a/tu/directorio_de_copias/{{ item.host }}/backup_{{ fecha_actual.stdout }}.sql"
        with_items: "{{ bases_de_datos }}"
        become: yes
  
      - name: Eliminar copias de seguridad antiguas
        find:
          paths: "/ruta/a/tu/directorio_de_copias/{{ item.host }}"
          age: 1d
          recurse: yes
          match: "*.sql.gz"
        register: copias_antiguas
        become: yes
  
      - name: Borrar copias de seguridad antiguas
        file:
          path: "{{ item.path }}"
          state: absent
        with_items: "{{ copias_antiguas.files }}"
        when: copias_antiguas.matched > 7
        become: yes
  
  # Define los servidores MySQL y sus bases de datos aquí
  vars:
    bases_de_datos:
      - { host: 192.168.1.1, database: nombre_de_la_base_de_datos_1 }
      - { host: 192.168.1.2, database: nombre_de_la_base_de_datos_2 }
      # Agrega más servidores y bases de datos según sea necesario
  ```
  
  En este playbook, hemos creado un directorio diferente para cada servidor MySQL dentro de la ruta `/ruta/a/tu/directorio_de_copias`. Las copias de seguridad se almacenan en directorios separados para cada servidor. Asegúrate de personalizar las direcciones IP, nombres de bases de datos, usuarios y contraseñas de MySQL en la variable `bases_de_datos` según tu entorno. Además, puedes ajustar la ruta de almacenamiento de copias de seguridad y la cantidad de copias a mantener según tus necesidades.
-