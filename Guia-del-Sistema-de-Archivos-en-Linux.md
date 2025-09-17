# Sistemas de Archivos en Linux
Anteriormente hemos dicho que en Linux "todo es un archivo". Esto incluye no solo documentos y carpetas, sino también dispositivos de hardware, procesos en ejecución y más. Para organizar y gestionar estos archivos, Linux utiliza un sistema de archivos jerárquico.

## Estructura del Sistema de Archivos
Todos lo archivos parten de una ruta raiz que se representa con una barra inclinada (/). Desde esta raíz, se ramifican varias carpetas y subcarpetas que contienen diferentes tipos de archivos y datos del sistema. 
Ejemplo de rutas :
```bash
/home/usuario/documentos
/etc/configuracion
/var/log/sistema.log
``` 
El caracter especial ~ representa el directorio home del usuario actual. Por ejemplo, si el usuario es "juan", la ruta ~/documentos se refiere a /home/juan/documentos.
Ejemplo de rutas con ~ :

```bash
~/documentos
~/imagenes/foto.jpg
```
Seria lo mismo que :

```bash
/home/juan/documentos
/home/juan/imagenes/foto.jpg
```

## Organizacion del Sistema de Archivos en Linux
- **/**: Raíz del sistema de archivos.
- **/bin**: Contiene los comandos esenciales del sistema que pueden ser utilizados por todos los usuarios, como pueden ser `ls`, `cp`, `mv`, etc.
- **/boot**: Archivos necesarios para el arranque del sistema, incluyendo el kernel, el gestor de arranque (GRUB) y otros archivos relacionados como podria ser la imagen disco RAM.
- **/dev**: Archivos de dispositivos que representan hardware y periféricos del sistema, como discos duros, impresoras y terminales,dichos archivos permiten que al kernel interactuar con el hardware.
- **/etc**: Archivos de configuración del sistema y scripts de inicio. Aquí se encuentran configuraciones para servicios del sistema, redes y usuarios.
- **/home**: Directorios personales de los usuarios. Cada usuario tiene su propia carpeta.
- **/lib**: Bibliotecas compartidas y módulos del kernel necesarios para que los programas y el sistema funcionen correctamente esenciales en los programas y comandos necesitan para funcionar en /bin.
- **/media**: Punto de montaje para dispositivos extraíbles como USB y CD-ROM.
- **/mnt**: Punto de montaje temporal para sistemas de archivos adicionales como son sistemas de archivos en red, dispositivos extraíbles.
- **/opt**: Software adicional y aplicaciones de terceros que no forman parte del sistema base, no estan manejados por el gestor de paquetes del sistema.
- **/proc**: Sistema de archivos virtual que proporciona información sobre los procesos en ejecución y el estado del sistema.
- **/root**: Directorio personal del usuario root (administrador del sistema).
- **/sbin**: Comandos del sistema esenciales que son utilizados principalmente por el usuario root para tareas de administración del sistema.
- **/srv**: Datos específicos de servicios proporcionados por el sistema, como servidores web o FTP.
- **/tmp**: Archivos temporales creados por aplicaciones y el sistema. Estos archivos suelen eliminarse al reiniciar el sistema.
- **/usr**: Archivos de usuario y aplicaciones instaladas. Contiene subdirectorios como /usr/bin (comandos de usuario), /usr/lib (bibliotecas) y /usr/share (datos compartidos).
- **/var**: Archivos variables que cambian con el tiempo, como registros del sistema, colas de impresión y archivos temporales de aplicaciones como /var/log.

# Tipos de sistemas de archivos

- **ext4**: Es el sistema de archivos más común en Linux. Ofrece buen rendimiento, soporte para archivos grandes y es muy estable.Su estabilidad, madurez y buen rendimiento lo hacen ideal para casi cualquier situación. Soporta grandes volúmenes de datos y cuenta con funciones de registro (journaling) que protegen contra la pérdida de datos en caso de un fallo de energía.
  
- **XFS**:  Sistemas que manejan grandes volúmenes de datos o que requieren operaciones de escritura y lectura de archivos masivos, como servidores de bases de datos o de almacenamiento.Se destaca por su alto rendimiento con archivos muy grandes y su capacidad para manejar sistemas de archivos de hasta 8 exabytes.
  
- **Btrfs**: Un sistema de archivos moderno con características avanzadas como instantáneas, compresión y verificación de datos.Sus funciones de instantáneas (snapshots) permiten crear copias de seguridad rápidas y eficientes del estado del sistema, mientras que la compresión y la verificación de datos ayudan a ahorrar espacio y a detectar errores.
  
- **ZFS**: Conocido por su integridad de datos, escalabilidad y características avanzadas como la deduplicación y la compresión.Es ideal para entornos empresariales y de almacenamiento en red, donde la integridad y la gestión eficiente del espacio son cruciales.
  
- **FAT32**: Un sistema de archivos compatible con múltiples sistemas operativos, pero con limitaciones en el tamaño de archivo (máximo 4 GB).
  
- **NTFS**: Utilizado principalmente por Windows, pero Linux puede leer y escribir en particiones NTFS con las herramientas adecuadas.
  
- **exFAT**: Diseñado para dispositivos de almacenamiento flash, es compatible con archivos grandes y es soportado por múltiples sistemas operativos.