# Gestión de Paquetes en Linux

En Linux, la gestión de software es clave para mantener el sistema actualizado y seguro. A diferencia de Windows o macOS, donde descargas programas desde la web, en Linux se usan **gestores de paquetes**. Estos automatizan la instalación, actualización y eliminación de programas, resolviendo automáticamente las dependencias necesarias.

## Tipos de paquetes

- **.deb**: Para distribuciones basadas en Debian (como Ubuntu y Mint).
- **.rpm**: Para distribuciones basadas en Red Hat (como Fedora, CentOS, openSUSE).
- **.tar.gz** o **.tar.xz**: Contienen código fuente que debe ser compilado manualmente.

## Gestores de paquetes más comunes

- **apt** y **dpkg**: Debian, Ubuntu y derivados.
- **yum** y **dnf**: Red Hat, Fedora, CentOS.
- **pacman**: Arch Linux.
- **zypper**: openSUSE y SUSE.

Los gestores de paquetes se conectan a **repositorios**, servidores que almacenan gran cantidad de software.

---

# Uso básico de apt en Ubuntu y Debian

Los siguientes comandos se ejecutan con permisos de superusuario (`sudo`).

### 1. Actualizar la lista de paquetes

Sincroniza la información de los paquetes disponibles.

```sh
sudo apt update
```

### 2. Instalar paquetes

Instala uno o varios programas y sus dependencias.

```sh
sudo apt install <paquete1> <paquete2>
```
Ejemplo:
```sh
sudo apt install apache2
```

**Opciones útiles:**
- `-y`: Responde "sí" automáticamente a las preguntas.
- `-s`: Simula la instalación, sin hacer cambios reales.

### 3. Actualizar todos los paquetes instalados

Actualiza todos los programas a la última versión disponible.

```sh
sudo apt upgrade
```

Para ver qué paquetes se pueden actualizar:
```sh
apt list --upgradable
```

### 4. Eliminar paquetes

Elimina un programa, pero deja sus archivos de configuración.

```sh
sudo apt remove <paquete>
```
Ejemplo:
```sh
sudo apt remove apache2
```

### 5. Eliminar completamente un paquete (incluyendo configuración)

```sh
sudo apt purge <paquete>
```
Ejemplo:
```sh
sudo apt purge apache2
```

### 6. Eliminar dependencias que ya no se usan

```sh
sudo apt autoremove
```

### 7. Buscar paquetes

Busca programas en los repositorios.

```sh
apt search <palabra_clave>
```
Ejemplo:
```sh
apt search mail server
```

### 8. Ver información de un paquete

Muestra detalles como descripción, versión y dependencias.

```sh
apt show <paquete>
```
Ejemplo:
```sh
apt show apache2
```

---

# Uso de dpkg

`dpkg` gestiona archivos `.deb` descargados localmente.

- **Listar paquetes instalados:**
    ```sh
    dpkg -l
    ```
    Si una línea empieza con "ii", el paquete está instalado correctamente.

- **Instalar un paquete local:**
    ```sh
    sudo dpkg -i <archivo_paquete.deb>
    ```