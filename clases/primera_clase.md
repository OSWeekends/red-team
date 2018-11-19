# CAPITULO 1. TERMINAL

**apt-get install terminator**
Usar el software Terminator = nos permite dividir la terminal de una manera muy práctica

### MANEJO BASICO TERMINAL

**Ifconfig** = muestra los datos de red, ip, mascara, broadcast...

**pwd** = ruta donde nos encontramos

**cd “directorio”** = nos mueve a ese directorio

**cd ..** = nos mueve al directorio anterior

**ls** = nos muestra los archivos y directorios donde nos encontramos

**ls -all** = muestra más detalles de los archivos y directorios, como permisos, tamaño, fecha de creación, etc...

**ls -all *.txt** = filtraría los txt

**grep -i “filtro”** = nos muestra la línea con la palabra a filtrar

**echo “información que queramos introducir” > nombrearchivo.txt** = crea un archivo .txt con esa información

**cat** = para leer un fichero

**nano** = para editar un fichero

**rm** = borrar archivo

**mkdir “directorio”** = crear directorio

**history** = para ver todos los comandos que hemos usado 

**rm -R “directorio”** = elimina un directorio

**cp “archivo para copiar” “nombre del archivo copiado”** = copiar archivos



### GESTION DE PROCESOS, PERMISOS Y BUSQUEDAS

#### PROCESOS

**ps** = para ver los procesos que están corriendo en el sistema (entorno de usuario)
**ps -all** = todos los procesos 
**“nombre del CMD” &** = dejar el proceso en segundo plano
**kill -9 “PID”** = para matar un proceso, el -9 es para forzar el cierre del proceso
top = ver los procesos y su consumo
**killall -9 “proceso”** = para matar varios procesos 
**bg** = para ver lo que tenemos en background
**fg** = para para volver al proceso que está en el background
**Cntrol+C** = termina el programa **Cntrol+Z** = lo mata  Cntrol+D = lo deja tal cual (background)

#### PERMISOS

**r = read 4   w = write 2   x = execute 1**

  - Los archivos están formados por 9 bits 3 grupos de tres, ejemplo: -rwx rwx rwx = 777
  
  - El primer grupo de 3 pertenece a los permisos del usuario actual, el segundo al grupo, y el tercero a otros usuarios del sistema.

**sudo su** = nos convierte en usuarios root con sus privilegios
**chmod 777 “archivo”** = para darle todos los permisos 
**chmod +rwx “archivo”** = daría los permisos “r w x” a los 3 grupos usuario, grupo y otros usuarios (777)

#### BUSQUEDAS

**grep -r “búsqueda” /** = nos buscaría todo lo que contuviese la palabra desde el directorio raíz
**locate “palabra a buscar”** = busca en la terminal la palabra
**updatedb** = actualizar la db
**whereis “palabra a buscar”** = busca la ruta

### RED E INSTALACION DE SOFWARE

**useradd -m “nombre usuario”** = crea un usuario nuevo
**passwd “nombre password”** = modifica el password
**usermode -a -G sudo “usuario”** = le da permisos de root

#### RED

**ping** = probar conexión entre dos ips

**netstat -ano** = indica que puertos y servicios están abiertos

**service ssh start** = inicia el servicio ssh

**service ssh status** = nos muestra el estado del servicio

**service ssh stop** = nos para el servicio ssh

**ssh “nombreusuario@IP”** = para conectarnos a un servicio ssh

**exit** = para salir de un servicio ssh

**service** = muestra todos los servicios que podemos iniciar (como el ssh anteriormente)

**service “servicio” start** = iniciar servicio

**service “servicio” stop** = parar servicio

**service “servicio” status** = ver el estado del servicio

#### INSTALACION DE SOFTWARE

**apt-get install “repositorio”** = instalaría el repositorio elegido

**dpkg -i “archivo.deb”** = para instalar archivos .deb

**./config | make | makeinstall** = para archivos ya descargados



### INFORMACION DEL SISTEMA 

**date** = fecha

**cal** = calendario

**uptime** = tiempo que lleva el sistema habilitado

**w** = que usuarios están ahora conectados al sistema

**whoami** = para saber que usuario somos

**finger “usuario”** = información del usuario

**uname -a** = información del sistema

**cat /proc/cpuinfo** = nos dará información del equipo (CPU)

**cat /proc/meminfo** = nos dará información de la memoria

**free** = uso de la memoria

**df** = memoria disponible

**man “comando”** = nos dará información del comando , como lanzarlo, como usarlo, etc. . .


### SCRIPS

#### DOMINIOS Y SUBDOMINIOS

**wget “url”** = descarga el código fuente de esa url

**grep “href=” “url”.html** = buscaría dentro de ese HTML los href
**| cut -d”/” -f3** = nos mostraría añadiendo a lo anterior lo que se encuentre entre el símbolo 
indicado

**| grep “\.”** = para filtrar aun filtrando el punto

**| sort -u** = nos ordena los dominios por orden y no nos replica los repetidos

**\> “nombre del archivo”.txt** = nos guardaría la terminal en un txt

### HOST

**Host “dominio”** = nos da la ip de ese dominio

**For dom in $(cat “nombre del archivo”.txt); do host $dom; done** = este scrip nos daría el comando host de cada dominio que estuviese en el txt que sacamos anteriormente 

**| grep “has address”** = nos filtraría los que en su línea tuviesen “has address”

**| cut -d “ “ -f4** = nos mostraría a partir del espacio 4º (en este caso solo las ips)

**; done** = nos iría mostrando el proceso