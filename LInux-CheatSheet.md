# Linux CheatSheet

Una referencia rápida y visual para comandos esenciales de Linux. Cada sección muestra los comandos, ejemplos y descripciones para que puedas consultarlos fácilmente cuando los necesites.

---

## 📁 Estructura de Directorios

| Ruta         | Contenido                                                                 |
|--------------|--------------------------------------------------------------------------|
| `/`          | Directorio raíz del sistema.                                             |
| `/home`      | Directorios personales de los usuarios.                                  |
| `/etc`       | Archivos de configuración del sistema y servicios.                       |
| `/var`       | Archivos de datos variables, como logs, bases de datos y correos.        |
| `/bin`       | Binarios esenciales del sistema para todos los usuarios.                 |
| `/sbin`      | Binarios del sistema para el administrador (root).                       |
| `/usr`       | Programas y archivos de aplicaciones de solo lectura.                    |
| `/tmp`       | Archivos temporales que se borran al reiniciar.                          |
| `/opt`       | Software opcional de terceros.                                           |
| `/dev`       | Archivos de dispositivos del sistema (discos, impresoras, etc.).         |
| `/media`     | Punto de montaje para medios removibles (USB, CD).                       |

---

## 🗂️ Comandos Fundamentales de Linux

| Comando | Ejemplo | Descripción |
|---------|---------|-------------|
| `ls`    | `ls -l /var/log` | Lista archivos. `-l` para detalles, `-a` para ocultos, `-R` recursivo. |
| `cd`    | `cd ~/Documents` | Cambia de directorio. `cd ..` sube un nivel, `cd ~` va al directorio personal. |
| `pwd`   | `pwd` | Muestra la ruta del directorio actual. |
| `mkdir` | `mkdir -p backups/daily` | Crea directorios. `-p` crea directorios padres si no existen. |
| `rm`    | `rm -rf my_project/` | Borra archivos (`rm`) o directorios (`rm -r`). `-f` fuerza la eliminación. |
| `cp`    | `cp -r /etc/ssh/ .` | Copia archivos o directorios. `-r` para carpetas. |
| `mv`    | `mv old_name.txt new_name.md` | Mueve o renombra un archivo o directorio. |
| `touch` | `touch new_script.sh` | Crea un archivo vacío o actualiza su fecha y hora. |
| `cat`   | `cat /etc/os-release` | Muestra el contenido de un archivo. |
| `grep`  | `grep "error" /var/log/syslog` | Busca patrones de texto en archivos. |
| `head`  | `head -n 5 access.log` | Muestra las primeras 5 líneas de un archivo. |
| `tail`  | `tail -f /var/log/apache2/error.log` | Muestra las últimas líneas. `-f` monitorea en tiempo real. |
| `wc`    | `wc -l file.txt` | Cuenta palabras, líneas y caracteres. `-l` cuenta líneas, `-w` palabras y `-c` caracteres. |
| `sort`  | `sort file.txt` | Ordena las líneas de un archivo de texto. |
| `uniq`  | `uniq file.txt` | Filtra líneas duplicadas adyacentes. `-d` muestra solo las líneas duplicadas. |
| `diff`  | `diff file1.txt file2.txt` | Compara dos archivos línea por línea. `-q` muestra si son diferentes, `-u` muestra las diferencias en un formato unificado. |
| `awk`   | `awk '{print $1}' data.txt` | Lenguaje de procesamiento de texto. Este ejemplo imprime la primera columna de cada línea. |
| `sed`   | `sed 's/old_word/new_word/g' file.txt` | Editor de streams. Reemplaza todas las apariciones de "old_word" por "new_word". |
| `tr`    | `echo "hello.world" \| tr '.' '-'` | Sustituye caracteres. Reemplaza el punto por un guion. |

---

## 📄 Comandos de Archivos y Directorios

| Comando | Ejemplo | Descripción |
|---------|---------|-------------|
| `man`   | `man ls` | Muestra el manual de ayuda de un comando. |
| `pwd`   | `pwd` | Muestra la ruta completa del directorio actual. |
| `cd`    | `cd /var/log` | Cambia de directorio. `cd ..` sube un nivel. |
| `ls`    | `ls -la` | Lista el contenido de un directorio. `-l` para detalles, `-a` para archivos ocultos. |
| `mkdir` | `mkdir -p docs/reports` | Crea directorios. `-p` crea directorios anidados. |
| `rmdir` | `rmdir empty_folder` | Elimina directorios vacíos. |
| `touch` | `touch new_file.txt` | Crea un archivo vacío o actualiza su fecha. |
| `cp`    | `cp -r data/ backup/` | Copia archivos o directorios. `-r` para copiar carpetas completas. |
| `mv`    | `mv old_file.txt new_file.txt` | Mueve o renombra archivos y directorios. |
| `rm`    | `rm -rf temp/` | Elimina archivos o directorios. `-r` recursivo, `-f` forzado. |

---

## 📦 Gestión de Paquetes (Ubuntu/Debian)

| Comando | Ejemplo | Descripción |
|---------|---------|-------------|
| `apt update`  | `apt update` | Sincroniza la lista de paquetes con los repositorios. |
| `apt upgrade` | `apt upgrade` | Actualiza todos los paquetes instalados. |
| `apt install` | `apt install nginx` | Instala uno o más paquetes. |
| `apt remove`  | `apt remove nginx` | Elimina un paquete, conservando la configuración. |
| `apt purge`   | `apt purge nginx` | Elimina un paquete y sus archivos de configuración. |
| `apt search`  | `apt search "mail server"` | Busca paquetes en los repositorios. |
| `apt show`    | `apt show nginx` | Muestra información detallada de un paquete. |

---

## 🔀 Redirección y Pipelines (Bash)

| Concepto                | Ejemplo                                   | Descripción |
|-------------------------|-------------------------------------------|-------------|
| Redirección (`>`)       | `echo "Hola" > saludo.txt`                | Sobrescribe la salida en un archivo. |
| Añadir (`>>`)           | `echo "Adiós" >> saludo.txt`              | Agrega la salida al final de un archivo. |
| Redirigir Errores (`2>`) | `find /root 2> errores.log`              | Redirige la salida de error a un archivo. |
| Todo a un archivo (`&>`) | `ls / &> all_output.txt`                 | Redirige la salida estándar y la de errores. |
| Pipelines (`|`)         | `ps aux | grep nginx`                     | Envía la salida de un comando a la entrada de otro. |
| Brace Expansion         | `mkdir folder-{a,b}`                      | Crea `folder-a` y `folder-b`. |
| Expansión Aritmética    | `echo $((10+5))`                          | Realiza operaciones matemáticas. |
| Globbing (`*` y `?`)    | `ls *.txt` <br> `ls file-?.txt`           | Coincide con cualquier caracter (`*`) o un solo caracter (`?`). |

---

## 👤 Gestión de Usuarios y Permisos

| Comando | Ejemplo | Descripción |
|---------|---------|-------------|
| `useradd` | `useradd -m -s /bin/bash juan` | Crea un nuevo usuario. `-m` crea el directorio home, `-s` asigna el shell. |
| `passwd`  | `passwd juan` | Asigna o cambia la contraseña de un usuario. |
| `usermod` | `usermod -aG sudo juan` | Modifica un usuario. `-aG` lo agrega a un grupo sin eliminarlo de los demás. |
| `userdel` | `userdel -r juan` | Elimina un usuario. `-r` borra también su directorio home. |
| `chmod`   | `chmod 700 private.sh` <br> `chmod +x script.sh` | Cambia permisos de archivos (notación octal o relativa). |
| `chown`   | `chown alicia:devs /data` | Cambia el propietario (chown) o el grupo (chgrp) de un archivo o directorio. `-R` para recursivo. |
| `sudoers` | `visudo` | Edita el archivo de configuración de sudo para asignar permisos. |

---

## 📊 Monitoreo y Procesos

| Comando | Ejemplo | Descripción |
|---------|---------|-------------|
| `ps`      | `ps aux` | Muestra los procesos en ejecución. |
| `top`     | `top` | Monitorea los procesos en tiempo real (uso de CPU, memoria). |
| `kill`    | `kill 12345` | Envía una señal para terminar un proceso por su ID de proceso (PID). |
| `killall` | `killall firefox` | Termina todos los procesos con un nombre específico. |
| `jobs`    | `jobs` | Muestra los trabajos en segundo plano en la sesión actual. |
| `bg`      | `sleep 300 & bg` | Envía un proceso al segundo plano. |
| `fg`      | `fg` | Trae un proceso en segundo plano al primer plano. |

---

## 💾 Espacio en Disco y Archivos

| Comando | Ejemplo | Descripción |
|---------|---------|-------------|
| `df`     | `df -h` | Muestra el espacio libre y usado de las particiones. `-h` para formato legible. |
| `du`     | `du -sh /home/user` | Muestra el tamaño de un directorio. `-s` suma el tamaño, `-h` lo hace legible. |
| `fdisk`  | `fdisk -l` | Muestra las particiones y discos físicos del sistema. |
| `mount`  | `mount /dev/sdb1 /mnt/usb` | Monta un sistema de archivos. |
| `umount` | `umount /mnt/usb` | Desmonta un sistema de archivos. |
| `tar`    | `tar -czvf archive.tar.gz /data` | Comprime archivos en un solo archivo `.tar.gz`. `-x` para extraer. |
| `find`   | `find /var -name "*.log"` | Busca archivos y directorios por nombre o tipo. |

---

## 🌐 Red y Conexiones Remotas

| Comando | Ejemplo | Descripción |
|---------|---------|-------------|
| `ifconfig` | `ifconfig` | Muestra y configura interfaces de red (obsoleto, `ip` es preferido). |
| `ip`       | `ip a` | Muestra las direcciones IP de las interfaces de red. |
| `ping`     | `ping -c 5 google.com` | Prueba la conectividad a un host. `-c` especifica la cantidad de paquetes. |
| `traceroute` | `traceroute google.com` | Rastrea la ruta de los paquetes a un host, mostrando cada salto. |
| `netstat`  | `netstat -tunlp` | Muestra conexiones de red. `-t` TCP, `-u` UDP, `-n` numérico, `-l` en escucha, `-p` procesos. |
| `ssh`      | `ssh user@hostname` | Inicia una sesión remota segura. `-p` para un puerto diferente. |
| `scp`      | `scp file.txt user@host:~/` | Copia archivos de forma segura entre hosts. |
| `wget`     | `wget https://example.com/file.zip` | Descarga archivos desde la web. |

---

## 🖥️ Información del Sistema

| Comando | Ejemplo | Descripción |
|---------|---------|-------------|
| `uname`       | `uname -a` | Muestra información detallada del sistema y el kernel. |
| `hostname`    | `hostname` | Muestra el nombre del equipo. `-I` muestra la dirección IP local. |
| `uptime`      | `uptime` | Muestra cuánto tiempo lleva el sistema encendido. |
| `date`        | `date` | Muestra la fecha y hora actuales. |
| `who`         | `who` | Muestra los usuarios conectados actualmente. |
| `dmesg`       | `dmesg` | Muestra los mensajes del kernel. |
| `lshw`        | `sudo lshw -short` | Muestra información detallada de hardware. |
| `lsb_release` | `lsb_release -a` | Muestra información de la distribución. |

---

## 🛠️ Gestión de Servicios y Tareas Programadas

| Comando | Ejemplo | Descripción |
|---------|---------|-------------|
| `systemctl`         | `systemctl start apache2` | Inicia, detiene, reinicia o verifica el estado de un servicio. |
| `systemctl enable`  | `systemctl enable apache2` | Configura un servicio para que se inicie al arrancar el sistema. |
| `crontab`           | `crontab -e` | Edita las tareas programadas (cronjobs) para el usuario actual. |
| `crontab -l`        | `crontab -l` | Muestra las tareas programadas existentes. |

---

## ⚙️ Configuraciones Avanzadas

| Servicio | Archivo de Configuración | Descripción |
|----------|-------------------------|-------------|
| SSH      | `/etc/ssh/sshd_config`  | Configura el servidor SSH (puerto, usuarios permitidos, etc.). |
| Cron     | `/etc/crontab` <br> `/etc/cron.d/` | Archivos de tareas programadas del sistema. |
| Samba    | `/etc/samba/smb.conf`   | Configura el servicio de compartición de archivos para Windows. |
| FTP (vsftpd) | `/etc/vsftpd.conf`  | Configura el servidor FTP. |
| MySQL    | `my.cnf`                | Configuración del servidor de base de datos MySQL/MariaDB. |

---

> **Consejo:** Usa la búsqueda de tu editor (`Ctrl+F`) para encontrar rápidamente el comando que necesitas.
