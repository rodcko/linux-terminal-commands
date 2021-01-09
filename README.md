# COMANDOS TERMINAL LINUX

Diferentes comandos de la terminal de Linux, si sabes alguno que no esta aca ¡dejalo en un pull request! :) 

## Organizacion de archivos
- `ls` lista los archivos
- `ls -a` lista los archivos ocultos
- `..` directorio padre

```sh
.
```
directorio al puntero actual

/* ORGANIZACION DE ARCHIVOS */
ls: lista los archivos
ls -a: lista archivos ocultos
..: directorio padre
.: directorio al puntero actual
pwd: identificar el directorio
cd: cambiar de directorio (parametro el directorio que quiero moverme)
cd ~: me lleva al home
cd -: ultimo directorio visitado
mkdir: crear un directorio (parametro del directorio a crear)
ls -l: ver si si son directorio o archivos
cp: copiar un archivo (cp nombrearchivo.extension nuevodirectorio/)
rm: borrar un archivo
mv: mover un archivo (mv ../archivoamover.extension .)
rmdir: eliminar un directorio (rmdir nombredirectorio) * primero borrar los archivos dentro de directorio, para poder borrar el directorio

/* MANEJO DE ARCHIVOS DE TEXTO Y UTILIDADES INTERACTIVAS */7
vim (i: para escribir, esc para salir del modo edicion, :q para salir de vim, :x salir y guardar cambios)
nano

/* UTILIDADES BATCH Y BATCH AVANZADAS */
cat: mostrar el contenido completo de un archivo
head: ver solo las primeras lineas del archivo
head -n 5 archivo.txt mostramos solo 5 lineas del archivo
tail: me muestra las ultimas lineas (lo contrario de head)
grep: busqueda por expresiones regulares
grep expresionabuscar archivo.sql
grep -i expresionabuscarnoimportantomayusominus archivo.sql
grep -i "frasequeterminaren$" archivo.sql
sed: tratamiento de flujos de caracteres
sed 's/palabraareemplazardentrodelarchivo/palabranueva/g' archivo.extension (s: sustitucion, g: global)
* no modifica el archivo, solo crea un nuevo flujo con la modificación, pero el archivo sigue teniendo lo que tenia
sed '$d' archivo.extension borra la ultima linea
awk: tratamiento de texto delimitado
awk -F ';' '{ print $1 }' text.txt indica que el delimitador de las columnas es el ; y que imprima solo la primer columna
touch: permite crear archivos
touch archivo.txt

/* COMUNICACION ENTRE PROCESOS */
mysql -h ip -u root -p123 < archivo.sql: conectarse al servidor
ls > archivos.txt (almacena todo lo que esta en un archivo, redireccionar la salida)
ls -l >> archivo.txt (el nuevo resultado lo agrega al final del archivo con la doble >)
ls -l | more (para ver mas archivos)
cat archivo.txt | wc -l (work count, para contar cuantos caracteres tiene un archivo)
head -n 15 archivo30lineas.txt > primeras15.txt (obtener 15 primeras linea de un archivo y y guardarlo en otro archivo)
date >> code.js (imprime la fecha al final de un archivo

/* ADMINISTRACION DE PROCESOS EN BACKGROUND Y FOREGROUND */
Si colocamos el ' al final de un comando, se ejecuta el proceso pero nos devuelve el control de la terminar (segundo plano/background)
Ctrl+z puedes mandar un proceso al background
ps: lista los procesos que se estan ejecutando
ps ax: da mas informacion de los procesos
ps ax | grep init: solo muestra las lineas que tengan init
top: muestra en tiempo real como los procesos estan cambiando (con q salimos del dashboard)
**foreground: primer plano
kill -9 numerodeproceso: mata el proceso (a un proceso en si) mandando una señal
killall: mata a todos (si no escuchan las señales) solo se coloca el nombre del archivo, no el id

/* PERMISOS SOBRE ARCHVOS: EL SISTEMA DE PERMISOS OCTAL */
alterar permisos:
chmod(cambia el modo del archivo)
chown(quien es el dueño del archivo)
chgrp(quien es el grupo de usuarios que puede acceder al archivo)
chmod o-w code.js (que le quite el permiso a otros usuarios para escribir)
chmod +x code.js (que tanto al dueño, grupos y otros usuarios se les de el permiso de ejecutar)
**notacion binaria: 777 (primera posicion owner, segunda grupos, tercera otros)
sudo nos permite ser superusuario por un momento

/* SISTEMA DE MANEJO DE PAQUETES */
Paquetes binarios: apt (debian, ubuntu), zypper (algunas otras), rpm (universal)
apt install lynx: ejemplo
Paquetes de lenguajes: pip, composer, npm
Otros: conda, homebrew

/* HERRAMIENTAS DE COMPRENSION Y COMBINACION DE ARCHIVOS */
ls code.js -lh (da mas detalles de cuanto pesa el archivo y fecha en que se hizo)
gzip code.js (comprimimos el archivo)
gzip -d code.js (descomprimir el archivo)
tar cf backup.tar backup/* (agrupa los archivos en un archivo backup.tar, todos los que esten dentor de la carpeta backup/)
tar tf backup.tar (vemos el contenido del archivo, solo agrupa, no comprime)
tar xf backup.tar (lo visualiza)
tar czf backup.tgz backup/* (agrupa y comprime los archivos)

/* HERRAMIENTAS DE BÚSQUEDA DE ARCHIVOS */
locate: hace una busqueda en todo el sistema de archivos
whereis: para buscar comandos
find: busca en un arbol de directorios, dependiendo los criterios que le ingreses
find . -user rodcko -perm 644 (buscar todos los archivos que le pertenecen a rodcko y con ciertos permisos)
find . -type f -mtime +7 -exec cp {} ./backup/ \; (buscar un tipo de archivo file y que haya sido modificado hace 7 dias, y seran copiados a un directorio backup) * comando poderoso para hacer backups

/* HERRAMIENTA PARA INTERACTUAR A TRAVES DE HTTP */
curl: hacer pedidos directamente, es decir pedidos crudos
wget: realiza descargas desde servidores http (recursivo)
curl https://platzi.com (nos devuelve todo el texto)
curl -v https://platzi.com | more
curl -v https://platzi.com > /dev/null: solo ve la comunicacion de encabezados http
wget https://www.url.com: nos descarga el archivo

/* ACCESO SEGURO A OTRAS COMPUTADORAS */
ssh: terminal segura 
ssh usuario
cat .ssh/ (ver la configuracion ssh)
ls .ssh/ -l (ver llaves publicas y privadas)
echo "Probando" | mail -s "Probando para Platzi" rodcko@live.com (enviar correos desde la terminal, hay que tener ciertas cosas configuradas)

/* VARIABLES DE ENTORNO */
Es una definicion global a la que todos los procesos tienen acceso, para tomar info de lo que esta pasando alrededor de, se conoce como $PATH, todos los procesos podrán acceder a ellas, tanto para leerlas como modificarlas, los tipos de asignación son:
Para un comando: VAR=valor comando
Para toda la sesión: export VAR=valor

/* COMO Y PARA QUE ESCRIBIR SCRIPTS EN BASH */
Scripting bash, codigo de programacion
source .bashrc: para ejecutar el comando

/* PROGRAMACION DE TAREAS */
at: at now +2 minutes (ejecutar algo dentro de 2min) y luego colocamos el comando
cron; utiliza la crontab (tareas programadas)
crontab -e: nos permite ver las tareas programadas y agregar nuevas, se ingresa a un archivo donde nos indica el minuto que lo queremos ejecutar, dias y que comando, luego salimos guardando los cambios en el archivo y listo

------------
- Curso de Introducción a la Terminal y Línea de Comandos: https://platzi.com/clases/terminal/
- Usuario de Platzi: https://platzi.com/p/rodcko2417/
