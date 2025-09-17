# Gestión de Red en Linux

La gestión de red en Linux se basa en un conjunto de comandos y archivos de configuración que permiten al usuario diagnosticar problemas de conectividad, configurar interfaces de red y gestionar el enrutamiento. A diferencia de los sistemas operativos de escritorio, la mayoría de la configuración se realiza a través de la línea de comandos, lo que ofrece un control más preciso sobre la red.

---

## Comandos de Diagnóstico

### `ping`

El comando `ping` se utiliza para probar la conectividad a un host, ya sea por IP o nombre de dominio. Envía paquetes ICMP (Internet Control Message Protocol) y mide el tiempo que tardan en recibir una respuesta. Es una herramienta esencial para verificar si un servidor está en línea y su latencia.

- **Función:** Diagnosticar la conexión y el tiempo de respuesta de un host.

#### Uso Básico

```bash
ping www.google.com
```

#### Banderas Clave

- `-c <número>`: Envía un número específico de paquetes y luego se detiene.
- `-i <segundos>`: Establece el intervalo entre cada envío de paquetes.
- `-4` o `-6`: Obliga a usar IPv4 o IPv6, respectivamente.
- `-I <interfaz>`: Especifica la interfaz de red desde la cual se enviarán los paquetes.

#### Ejemplo de Uso

```bash
ping -c 3 www.google.com
```

---

### `traceroute`

El comando `traceroute` te permite seguir la ruta que toman los paquetes para llegar a un destino. Es útil para identificar cuellos de botella o puntos de fallo en la red.

- **Función:** Mapea los "saltos" (routers) entre tu equipo y un destino.

#### Uso Básico

```bash
traceroute www.google.com
```

#### Salida de Ejemplo

Cada línea representa un salto, mostrando la IP, el nombre del host (si está disponible) y el tiempo que tarda el paquete en llegar a ese punto.

---

### `nslookup`

`nslookup` es una herramienta para realizar consultas a los servidores DNS y obtener información sobre nombres de dominio e IPs.

- **Función:** Resuelve nombres de dominio a direcciones IP (y viceversa).

#### Uso Básico

```bash
nslookup as.com
```

#### Salida de Ejemplo

Muestra las direcciones IP asociadas con el nombre de dominio.

---

## Comandos de Configuración Temporal (`ip`)

El comando `ip` es la herramienta moderna y preferida para configurar las interfaces de red, las tablas de enrutamiento y las direcciones IP.

- **Ver el estado de las interfaces de red:**

    ```bash
    ip link show
    ```

- **Ver las direcciones IP asignadas a cada interfaz:**

    ```bash
    ip address show
    ```

- **Activar o desactivar una interfaz de red:**

    ```bash
    sudo ip link set dev eth1 down
    sudo ip link set dev eth1 up
    ```

- **Mostrar la tabla de enrutamiento del sistema:**

    ```bash
    ip route
    ```

- **Agregar una nueva entrada de enrutamiento:**

    ```bash
    sudo ip route add 172.16.0.42 dev eth1
    ```

- **Eliminar una entrada de enrutamiento:**

    ```bash
    sudo ip route del 172.16.0.42 dev eth1
    ```

> **Nota Importante:** Los cambios realizados con el comando `ip` son temporales y se perderán al reiniciar el sistema.

---

## Configuración Persistente y el Directorio `/etc/network`

Para que los cambios en la configuración de red persistan después de un reinicio, debes modificar los archivos de configuración en el sistema. Aunque las distribuciones modernas como Ubuntu utilizan Netplan, la configuración tradicional se encuentra en `/etc/network/interfaces`.

### El Archivo `interfaces`

Este archivo es el corazón de la configuración de red en sistemas basados en Debian. Aquí se define la configuración de cada interfaz de red.

#### Configurar una IP Estática

Para asignar una dirección IP fija a una interfaz, edita el archivo `interfaces` y define la configuración de forma manual.

1. Abre el archivo con un editor de texto (requiere permisos de superusuario):

    ```bash
    sudo nano /etc/network/interfaces
    ```

2. Define la interfaz `eth0` como estática y añade los siguientes parámetros:

    ```bash
    # La interfaz de loopback
    auto lo
    iface lo inet loopback

    # Configuración de la interfaz eth0
    auto eth0
    iface eth0 inet static
        address 192.168.1.100
        netmask 255.255.255.0
        gateway 192.168.1.1
        dns-nameservers 8.8.8.8 8.8.4.4
    ```

3. Guarda los cambios y cierra el editor.

4. Reinicia el servicio de red para aplicar la nueva configuración:

    ```bash
    sudo systemctl restart networking
    ```

    O reinicia la interfaz directamente:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

Ahora la interfaz `eth0` tendrá una dirección IP estática que no cambiará.

---