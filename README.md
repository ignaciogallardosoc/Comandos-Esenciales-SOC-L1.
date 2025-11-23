Comandos Esenciales de Linux para Ciberseguridad (SOC)
# 1. Identidad y estado del Sistema

Estos son los primeros comandos que usa cualquier analista al Iniciar Sesión.

## 1.1 whoami

**Descripción:** Muestra el nombre de usuario actual que inició en el sistema.

**Ejemplo Usado:** `whoami`

**Salida Esperada:** ignaciogallardosoc

**Uso en Ciberseguridad:** Confirma desde qué cuenta se está operando. Ayuda a detectar escalamiento de privilegios o sesiones sospechosas.

## 1.2 pwd

**Descripción:** Indica dónde estamos, ruta completa actual.

**Ejemplo Usado:** `pwd`

**Salida Esperada:** /home/ignaciogallardosoc

**Uso en Ciberseguridad:** Se utiliza para confirmar nuestra ubicación en el sistema cuando analizamos rutas de logs o auditamos directorios sensibles (/etc, /var/log).

## 1.3 hostname

**Descripción:** Muestra el nombre del dispositivo o servidor donde estás trabajando.

**Ejemplo Usado:** `hostname`

**Salida Esperada:** ubuntu-vm

**Uso en Ciberseguridad:** Ayuda a identificar la máquina cuando estás conectado a múltiples hosts en una red corporativa.

## 1.4 uname -a

**Descripción:** Muestra información completa del sistema operativo: kernel, arquitectura, versión, etc.

**Ejemplo Usado:** `uname -a`

**Salida Esperada:** Linux ubuntu 5.15.0-72-generic

**Uso en Ciberseguridad:** Permite identificar vulnerabilidades ligadas a versiones del kernel y del sistema.

## 1.5 date

**Descripción:** Muestra fecha y hora actuales del sistema.

**Ejemplo Usado:** `date`

**Salida Esperada:** Sat nov 23 12:45:01-11 2025

**Uso en Ciberseguridad:** Clave para correlacionar eventos, logs y ataques según línea de tiempo.

## 1.6 uptime

**Descripción:** Muestra cuánto tiempo lleva encendido el sistema y su carga promedio.

**Ejemplo Usado:** `uptime`

**Salida Esperada:** 12:47:15 up 3:21, 2 users, load average: 0.24, 0.31, 0.11

**Uso en Ciberseguridad:** Permite detectar reinicios sospechosos o caídas relacionadas con incidentes.

## 1.7 who

**Descripción:** Muestra qué usuarios están actualmente logeados en el sistema.

**Ejemplo Usado:** `who`

**Salida Esperada:** ignaciogallardosoc tty1 2025-11-23 10:02

**Uso en Ciberseguridad:** Detecta sesiones activas que podrían no corresponder a usuarios legítimos.

## 1.8 id

**Descripción:** Muestra los UID, GID y grupos del usuario actual.

**Ejemplo Usado:** `id`

**Salida Esperada:** uid=1000(ignaciogallardosoc) gid=1000 groups=1000,27,4,24...

**Uso en Ciberseguridad:** Ayuda a identificar privilegios del usuario y validar controles de acceso.

## 1.9 df -h

**Descripción:** Muestra el espacio disponible en los discos del sistema en formato legible.

**Ejemplo Usado:** `df -h`

**Salida Esperada:** Listados de particiones con su espacio usado/libre. Ejemplo: /dev/sda1 40G 18G 22G 45% /

**Uso en Ciberseguridad:** Ayuda a detectar llenado de disco malicioso, ataques de DoS por almacenamiento o logs excesivos.

## 1.10 free -h

**Descripción:** Muestra el uso de memoria RAM y swap en formato legible.

**Ejemplo Usado:** `free -h`

**Salida Esperada:** Mem: 3.8G used, 1.2G free Swap: 2.0G used, 0 free

**Uso en Ciberseguridad:** Permite identificar procesos sospechosos que consumen demasiada memoria (malware, cryptominers).


# 2. Navegación del Sistema

Este bloque es fundamental para moverte como un analista de SOC dentro de Linux.

## 2.1 ls

**Descripción:** Lista los archivos y directorios del directorio actual.

**Ejemplo Usado:** `ls`

**Salida Esperada:** Nombres y carpetas de archivos.

**Uso en Ciberseguridad:** Revisar rápidamente qué archivos existen en rutas críticas como /etc/, /home/, /var/log/.

## 2.2 ls -la

**Descripción:** Lista los archivos con información detallada: permisos, dueño, tamaño, fechas y ocultos.

**Ejemplo Usado:** `ls -la`

**Salida Esperada:** Columnas de permisos (drwxr-xr-x), propietario, tamaño, fecha, nombre.

**Uso en Ciberseguridad:** Analizar permisos incorrectos, archivos ocultos, modificaciones sospechosas.

## 2.3 cd

**Descripción:** Cambia al directorio especificado.

**Ejemplo Usado:** `cd /home`

**Salida Esperada:** Cambias a la carpeta /home.

**Uso en Ciberseguridad:** Moverte durante rutas clave del sistema durante una investigación.

## 2.4 cd ..

**Descripción:** Sube un nivel en el árbol de directorios.

**Ejemplo Usado:** `cd ..`

**Salida Esperada:** Regresas a la carpeta padre.

**Uso en Ciberseguridad:** Navegar jerarquías de logs o configuraciones sin perderte.

## 2.5 cd /

**Descripción:** Te mueve al directorio raíz del sistema.

**Ejemplo Usado:** `cd /`

**Salida Esperada:** Ruta: /.

**Uso en Ciberseguridad:** Explorar todo el filesystem desde el nivel más alto.

## 2.6 tree

*(Si no lo tienes instalado: sudo apt install tree)*

**Descripción:** Muestra la estructura de directorios en forma de árbol.

**Ejemplo Usado:** `tree`

**Salida Esperada:** Una representación jerárquica del contenido (visual).

**Uso en Ciberseguridad:** Muy útil para visualizar dónde se ocultan archivos, scripts o subdirectorios sospechosos.

## 2.7 ls -lh

**Descripción:** Lista los archivos con tamaños en formato legible (KB, MB, GB).

**Ejemplo Usado:** `ls -lh`

**Salida Esperada:** Los tamaños aparecerán como "12K", "4.3M", etc.

**Uso en Ciberseguridad:** Detectar archivos inusualmente grandes (Ej: dumps de memoria, archivos exfiltrados).

## 2.8 ls -R

**Descripción:** Muestra todos los archivos de forma recursiva incluyendo subdirectorios.

**Ejemplo Usado:** `ls -R`

**Salida Esperada:** Listados extendidos de carpetas internas.

**Uso en Ciberseguridad:** Ver estructuras completas y descubrir archivos escondidos en profundidad.


# 3. Manipulación de Archivos y Directorios

## 3.1 touch

**Descripción:** Crea un archivo vacío o actualiza la fecha de modificación de uno existente.

**Ejemplo Usado:** `touch notas.txt`

**Salida Esperada:** Se crea el archivo "notas.txt" (no muestra texto en pantalla).

**Uso en Ciberseguridad:** Crea archivos temporales para análisis, pruebas de permisos o preparar estructuras de trabajo.

## 3.2 mkdir

**Descripción:** Crea un directorio (carpeta).

**Ejemplo Usado:** `mkdir logs`

**Salida Esperada:** Se crea la carpeta "logs".

**Uso en Ciberseguridad:** Organizar carpetas para guardar informes, evidencias o archivos analizados.

## 3.3 mkdir -p

**Descripción:** Crea una ruta completa de directorios aunque no existan los niveles anteriores.

**Ejemplo Usado:** `mkdir -p proyectos/SOCTEAM/2025`

**Salida Esperada:** Creación de toda la ruta sin errores.

**Uso en Ciberseguridad:** Levantar lecturas de análisis o repositorios de evidencia sin preocuparte por carpetas faltantes.

## 3.4 rm

**Descripción:** Elimina archivos específicos.

**Ejemplo Usado:** `rm notas.txt`

**Salida Esperada:** El archivo se elimina (No deja ningún mensaje).

**Uso en Ciberseguridad:** Eliminar restos de archivos temporales después de análisis o scripts de prueba.

## 3.5 rm -r

**Descripción:** Elimina directorios completos (con todo su contenido).

**Ejemplo Usado:** `rm -r proyecto_prueba`

**Salida Esperada:** Todos los archivos y subcarpetas dentro de "proyecto_prueba" se eliminan.

**Uso en Ciberseguridad:** Limpiar los entornos de análisis, borrar carpetas contaminadas o pruebas de malware.

## 3.6 cp

**Descripción:** Copia un archivo a otra ubicación.

**Ejemplo Usado:** `cp evidencia.txt respaldo.txt`

**Salida Esperada:** Se crea una copia llamada "respaldo.txt".

**Uso en Ciberseguridad:** Copiar evidencia sin modificar los archivos originales antes del análisis.

## 3.7 cp -r

**Descripción:** Copia carpetas completas con todos sus archivos.

**Ejemplo Usado:** `cp -r /var/log ./logs_backup`

**Salida Esperada:** Copia todo el directorio /var/log dentro de "logs_backup".

**Uso en Ciberseguridad:** Resguardar logs antes de analizarlos para evitar alteraciones.

## 3.8 mv

**Descripción:** Mueve un archivo o directorio a otra ubicación, o cambia su nombre.

**Ejemplo Usado:** `mv notas.txt notas_antiguas.txt`

**Salida Esperada:** El archivo cambia de nombre.

**Uso en Ciberseguridad:** Mover archivos sospechosos a cuarentena o reorganizar información recolectada.

## 3.9 cat

**Descripción:** Muestra el contenido completo de un archivo en pantalla.

**Ejemplo Usado:** `cat /var/log/auth.log`

**Salida Esperada:** Ver el contenido del archivo auth.log línea por línea.

**Uso en Ciberseguridad:** Lectura rápida de logs o configuraciones para detectar anomalías.

## 3.10 less

**Descripción:** Permite visualizar archivos largos de manera paginada, con scroll.

**Ejemplo Usado:** `less /var/log/syslog`

**Salida Esperada:** Se abre un archivo en un visor; se navega con flechas.

**Uso en Ciberseguridad:** Lectura eficiente de logs extensos sin saturar la pantalla.


# 4. Búsqueda, Lectura de Logs y Análisis Avanzado

## 4.1 head

**Descripción:** Muestra las primeras 10 líneas de un archivo.

**Ejemplo Usado:** `head /var/log/syslog`

**Salida Esperada:** Primeras 10 líneas del archivo.

**Uso en Ciberseguridad:** Revisar encabezados de logs o archivos recién generados para entender su formato rápido.

## 4.2 head -n 20

**Descripción:** Muestra una cantidad de líneas desde el inicio.

**Ejemplo Usado:** `head -n 20 /var/log/auth.log`

**Salida Esperada:** Primeras 20 líneas del documento.

**Uso en Ciberseguridad:** Examinar cambios iniciales en logs tras un reinicio o intento de acceso.

## 4.3 tail

**Descripción:** Muestra las últimas 10 líneas de un archivo.

**Ejemplo Usado:** `tail /var/log/auth.log`

**Salida Esperada:** Últimas 10 líneas del archivo.

**Uso en Ciberseguridad:** Ver actividad reciente, como intentos fallidos de login.

## 4.4 tail -n

**Descripción:** Muestra una cantidad específica de líneas desde el final.

**Ejemplo Usado:** `tail -n 50 /var/log/syslog`

**Salida Esperada:** Últimas 50 líneas del archivo.

**Uso en Ciberseguridad:** Revisar eventos recientes justo después de un ataque o un reinicio.

## 4.5 tail -f

**Descripción:** Muestra nuevas líneas en tiempo real conforme se escriben en el archivo.

**Ejemplo Usado:** `tail -f /var/log/auth.log`

**Salida Esperada:** Actualización en vivo de nuevas entradas.

**Uso en Ciberseguridad:** Monitorear ataques en tiempo real (Fuerza Bruta SSH, accesos anómalos, cambios sospechosos).

## 4.6 nano

**Descripción:** Editor de texto simple para crear y modificar archivos directamente en la terminal.

**Ejemplo Usado:** `nano notas.txt`

**Salida Esperada:** Se abre el editor dentro de la terminal.

**Uso en Ciberseguridad:** Editar configuraciones, scripts, notas de análisis y archivos de respuesta a incidentes.

## 4.7 grep

**Descripción:** Busca texto dentro de un archivo.

**Ejemplo Usado:** `grep "Failed" /var/log/auth.log`

**Salida Esperada:** Coincidencias de líneas que contengan "Failed".

**Uso en Ciberseguridad:** Filtrar intentos fallidos de autenticación o patrones sospechosos en logs.

## 4.8 grep -i

**Descripción:** Busca texto ignorando mayúsculas o minúsculas.

**Ejemplo Usado:** `grep -i "Failed" /var/log/syslog`

**Salida Esperada:** Coincidencias sin importar MAYÚS.

**Uso en Ciberseguridad:** Buscar eventos cuyos formatos varían según el sistema.

## 4.9 grep -R

**Descripción:** Busca texto dentro de todos los archivos de un directorio de manera recursiva.

**Ejemplo Usado:** `grep -R "password" /etc`

**Salida Esperada:** Listado de archivos y líneas donde aparece el texto.

**Uso en Ciberseguridad:** Encontrar contraseñas expuestas, configuraciones sensibles o rastros de malware.

## 4.10 find

**Descripción:** Busca archivos por nombre, tipo, tamaño o ubicación en todo el sistema.

**Ejemplo Usado:** `find / -name "Oculto"`

**Salida Esperada:** Rutas donde exista un archivo llamado "Oculto".

**Uso en Ciberseguridad:** Localizar archivos sospechosos, scripts ocultos o elementos fuera de lugar en una intrusión.


# 5. Permisos, Procesos, Recursos y Red

## 5.1 ls -l

**Descripción:** Muestra archivos con permisos detallados, dueño y grupo.

**Ejemplo Usado:** `ls -l`

**Salida Esperada:** Líneas como -rw-r--r-- 1 ignaciogallardosoc 532 Nov 23 notas.txt

**Uso en Ciberseguridad:** Identificar permisos indebidos, archivos modificados, acceso anómalo o herencias peligrosas.

## 5.2 chmod

**Descripción:** Modifica los permisos de un archivo o directorio.

**Ejemplo Usado:** `chmod 644 notas.txt`

**Salida Esperada:** El archivo queda con permisos: rw-r---- (según configuración, típicamente lectura/escritura para dueño).

**Uso en Ciberseguridad:** Corregir permisos inseguros, proteger evidencia, bloquear escritura no autorizada.

## 5.3 chmod +x

**Descripción:** Agrega permiso de ejecución a un archivo.

**Ejemplo Usado:** `chmod +x script.sh`

**Salida Esperada:** El archivo script.sh ahora es ejecutable.

**Uso en Ciberseguridad:** Habilitar scripts de análisis, herramientas de monitoreo o automatización.

## 5.4 sudo chown

**Descripción:** Cambia el propietario y grupo de un archivo.

**Ejemplo Usado:** `sudo chown ignacio:ignacio notas.txt`

**Salida Esperada:** Ahora el archivo notas.txt pertenece al usuario especificado.

**Uso en Ciberseguridad:** Arreglar archivos que quedaron con dueños incorrectos tras un ataque o mala configuración.

## 5.5 ps aux

**Descripción:** Lista de TODOS los procesos del sistema (usuarios, root, background).

**Ejemplo Usado:** `ps aux`

**Salida Esperada:** Muestra de procesos con columnas, PID, USER, %CPU, %MEM, COMMAND.

**Uso en Ciberseguridad:** Detectar procesos sospechosos, malware, criptomineros, servicios no autorizados.

## 5.6 top

**Descripción:** Muestra en tiempo real proceso, uso de CPU, RAM y carga.

**Ejemplo Usado:** `top`

**Salida Esperada:** Interfaz dinámica con los procesos más activos.

**Uso en Ciberseguridad:** Identificar consumo anormal de recursos causado por malware o intrusiones.

## 5.7 htop

*(Si no lo tienes: sudo apt install htop)*

**Descripción:** Versión interactiva mejorada de top.

**Ejemplo Usado:** `htop`

**Salida Esperada:** Vista moderna con colores, barras y navegación con teclas.

**Uso en Ciberseguridad:** Filtrar procesos, ver hilos, matar procesos sospechosos fácilmente.

## 5.8 ip a

**Descripción:** Muestra todas las interfaces de red y sus direcciones IP.

**Ejemplo Usado:** `ip a`

**Salida Esperada:** Interfaces como lo, eth0, enp0s3 con IPs y estados.

**Uso en Ciberseguridad:** Identificar la IP del host, interfaces activas o configuraciones alteradas por malware.

## 5.9 ss -tulpn

**Descripción:** Muestra puertos abiertos y servicios que los están usando.

**Ejemplo Usado:** `ss -tulpn`

**Salida Esperada:** Líneas como: LISTEN 0 128 124.155.66.789:22

**Uso en Ciberseguridad:** Detectar puertos abiertos inesperados, backdoors, servicios expuestos.

## 5.10 ping

**Descripción:** Envía paquetes ICMP para verificar conectividad.

**Ejemplo Usado:** `ping google.com`

**Salida Esperada:** Líneas con tiempo de respuesta.

**Uso en Ciberseguridad:** Comprobar disponibilidad de hosts, redes internas, detectar cortes o configuraciones sospechosas.
```
