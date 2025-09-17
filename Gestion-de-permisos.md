# Gestión de Permisos en Linux

En Linux, los permisos de archivos y directorios son un pilar fundamental de la seguridad. Cada archivo tiene un conjunto de permisos que define quién puede leer, escribir y ejecutarlo. Estos permisos se dividen en tres categorías principales: el usuario propietario, el grupo propietario y otros usuarios.

El comando `ls -l` muestra los permisos de un archivo o directorio en la primera columna de su salida. Por ejemplo, en la cadena `-rw-r--r--`:

- El primer carácter (`-`) indica el tipo de archivo: `-` para un archivo, `d` para un directorio o `l` para un enlace simbólico.
- Los siguientes tres grupos de tres caracteres representan los permisos para el propietario, el grupo y otros, respectivamente.

| Permiso | Descripción |
|---------|-------------|
| r       | Permiso de lectura. Permite ver el contenido del archivo o la lista de archivos de un directorio. |
| w       | Permiso de escritura. Permite modificar, guardar o eliminar un archivo. En un directorio, permite crear, renombrar o eliminar archivos. |
| x       | Permiso de ejecución. Permite ejecutar un archivo (si es un script o programa) o acceder a un directorio para usar su contenido. |

---

## Cambio de Permisos (`chmod`)

El comando `chmod` (change mode) se usa para modificar los permisos de archivos y directorios, y puedes hacerlo de dos formas.

### Modo Relativo

Este método es ideal para hacer ajustes específicos a los permisos sin afectar a los demás. Se utiliza una notación con `+` para añadir, `-` para quitar y `=` para establecer.

**Añadir permisos de escritura al grupo:**

```bash
$ ls -l my_report.pdf
-rw-r--r-- 1 alicia developers 1024 Apr  1 10:00 my_report.pdf
$ chmod g+w my_report.pdf
$ ls -l my_report.pdf
-rw-rw-r-- 1 alicia developers 1024 Apr  1 10:00 my_report.pdf
```

**Quitar permiso de escritura a todos:**

```bash
$ chmod a-w my_report.pdf
$ ls -l my_report.pdf
-r--r--r-- 1 alicia developers 1024 Apr  1 10:00 my_report.pdf
```

**Establecer permisos de ejecución solo para el propietario:**

```bash
$ chmod u+x myscript.sh
$ ls -l myscript.sh
--xrw-rw-r-- 1 alicia developers 1024 Apr  1 10:00 myscript.sh
```

---

### Modo Absoluto (Octal)

Este método permite establecer todos los permisos de una sola vez usando números. Cada permiso tiene un valor numérico: `r=4`, `w=2` y `x=1`. Sumas los valores para cada categoría de usuario para obtener un número de tres dígitos.

| Permisos | Binario | Octal |
|----------|---------|-------|
| rwx      | 111     | 7     |
| rw-      | 110     | 6     |
| r-x      | 101     | 5     |
| r--      | 100     | 4     |

**Ejemplo:** Darle al propietario todos los permisos, y al grupo y otros solo lectura y ejecución (`755`).

- Propietario: rwx (4+2+1) = 7
- Grupo: r-x (4+1) = 5
- Otros: r-x (4+1) = 5

```bash
$ chmod 755 public_folder/
$ ls -ld public_folder/
drwxr-xr-x 2 alicia developers 4096 Apr  1 10:00 public_folder/
```

---

## Cambio de Propietario y Grupo

Para cambiar el propietario y el grupo de un archivo o directorio, se usan los comandos `chown` y `chgrp`.

**Cambiar solo el propietario:**

```bash
$ ls -l /var/log/app.log
-rw-r----- 1 root sysadmin 1024 Apr  1 10:00 /var/log/app.log
$ sudo chown www-data /var/log/app.log
$ ls -l /var/log/app.log
-rw-r----- 1 www-data sysadmin 1024 Apr  1 10:00 /var/log/app.log
```

**Cambiar solo el grupo:**

```bash
$ sudo chgrp developers /var/log/app.log
$ ls -l /var/log/app.log
-rw-r----- 1 www-data developers 1024 Apr  1 10:00 /var/log/app.log
```

**Cambiar propietario y grupo al mismo tiempo:**

```bash
$ sudo chown www-data:dev_team /var/log/app.log
$ ls -l /var/log/app.log
-rw-r----- 1 www-data dev_team 1024 Apr  1 10:00 /var/log/app.log
```

Ambos comandos pueden usar la bandera `-R` para aplicar los cambios de manera recursiva a todos los archivos y subdirectorios.

---

## Gestión de Privilegios con sudoers

`sudo` es un comando que permite a un usuario ejecutar otro comando con permisos de superusuario. El archivo `/etc/sudoers` controla qué usuarios pueden usar `sudo` y qué comandos pueden ejecutar. Para editarlo, siempre se usa `visudo`, que valida la sintaxis y previene errores críticos.

**Ejemplo:** Permitir a un usuario ejecutar un comando específico sin contraseña

```bash
# El usuario 'analyst' puede reiniciar el servicio 'apache2' sin necesidad de contraseña.
analyst ALL=(ALL) NOPASSWD: /usr/sbin/service apache2 restart
```