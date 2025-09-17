# Introducción a BASH

Bash no es solo un shell; es un lenguaje de scripting completo que te permite automatizar tareas y controlar tu sistema operativo de manera eficiente. Su función principal es actuar como un intermediario entre tus comandos y el kernel de Linux.

---

## Características básicas

### Variables

Para usar el valor de una variable, solo necesitas poner el signo de dólar (`$`) antes de su nombre.

**Ejemplo:**

```bash
user_name="Alice"
echo "Hola, $user_name. ¡Bienvenida!"
```
Salida:
```
Hola, Alice. ¡Bienvenida!
```

---

## Redirección

En Bash, la redirección es una técnica poderosa que manipula el flujo de datos de los comandos. Cada comando tiene una entrada estándar (STDIN), una salida estándar (STDOUT), y una salida de error estándar (STDERR).

**Descriptores de Archivo:**

- `0`: STDIN (entrada del teclado)
- `1`: STDOUT (salida en la pantalla)
- `2`: STDERR (mensajes de error en la pantalla)

### Operadores de Salida (`>` y `>>`)

- El operador `>` redirige la salida estándar a un archivo. Si el archivo existe, su contenido se sobrescribe.

**Ejemplo 1: Sobrescribir un archivo de log**

```bash
echo "Iniciando servicio... $(date)" > service.log
cat service.log
```
Salida:
```
Iniciando servicio... Wed Sep 17 11:50:53 CEST 2025
```
Si vuelves a ejecutar el comando, la fecha y la hora cambiarán, y el contenido anterior se perderá.

- El operador `>>` agrega la salida al final del archivo sin borrar el contenido previo.

**Ejemplo 2: Agregar una nueva entrada a un log**

```bash
echo "Servicio iniciado correctamente." >> service.log
cat service.log
```
Salida:
```
Iniciando servicio... Wed Sep 17 11:50:53 CEST 2025
Servicio iniciado correctamente.
```

### Redirigir Errores (`2>`)

Para capturar los mensajes de error, utiliza el descriptor `2` seguido del operador de redirección.

**Ejemplo 3: Separar la salida de errores**

```bash
# Este comando buscará un directorio que no existe.
find /non_existent_folder 2> error_output.txt
cat error_output.txt
```
Salida:
```
find: ‘/non_existent_folder’: No existe el fichero o el directorio
```

### Enviar STDOUT y STDERR al mismo archivo

Puedes redirigir ambas salidas a un mismo archivo usando `&>`.

**Ejemplo 4: Enviar STDOUT y STDERR al mismo archivo**

```bash
# Buscar en un directorio que existe y en uno que no
ls /etc /non_existent_folder &> mixed_output.txt
cat mixed_output.txt
```
Salida:
```
ls: no se puede acceder a '/non_existent_folder': No existe el fichero o el directorio
/etc:
alternatives   cron.daily   hosts       ltrace.conf  nsswitch.conf  passwd
...
```

---

## Pipelines (`|`)

Una pipeline (o tubería) conecta la salida estándar de un comando a la entrada estándar del siguiente. Esto te permite encadenar comandos para procesar datos paso a paso.

**Ejemplo 5: Buscar procesos y contarlos**

```bash
ps aux | grep "apache2" | wc -l
```
Salida:
```
5
```

- `ps aux`: Lista todos los procesos del sistema.
- `|`: La salida de `ps aux` se envía como entrada al siguiente comando.
- `grep "apache2"`: Filtra las líneas que contienen la palabra "apache2".
- `|`: La salida de `grep` se envía al siguiente comando.
- `wc -l`: Cuenta el número de líneas, dándote el total de procesos de Apache.

---

## Expansiones de Bash

Las expansiones son atajos que Bash utiliza para generar cadenas y nombres de archivos de forma automática, ahorrándote tiempo y escritura.

### Brace Expansion (`{}`)

Genera combinaciones de cadenas a partir de una lista de elementos entre llaves, separados por comas.

**Ejemplo 6: Crear una serie de archivos de respaldo**

```bash
touch report-{v1,v2,v3}.txt
ls
```
Salida:
```
report-v1.txt  report-v2.txt  report-v3.txt
```

**Ejemplo 7: Combinar expansiones**

```bash
echo {img,css,js}/{main,style,script}.*
```
Salida:
```
img/main.* img/style.* img/script.* css/main.* css/style.* css/script.* js/main.* js/style.* js/script.*
```

### Expansión Aritmética (`$(( ))`)

Permite realizar operaciones matemáticas simples directamente en la terminal.

**Ejemplo 8: Realizar un cálculo en línea**

```bash
echo "El total es: $((250 * 2 / 10 + 50))"
```
Salida:
```
El total es: 100
```

### Expansión de Nombres de Archivos (Globbing)

Utiliza caracteres comodín para coincidir con nombres de archivos.

- `*` (asterisco): Coincide con cero o más caracteres.

**Ejemplo 9: Listar todos los archivos que terminan en .log**

```bash
ls /var/log/*.log
```
Salida:
```
auth.log  cron.log  debug.log  syslog
```

- `?` (interrogante): Coincide con un solo carácter.

**Ejemplo 10: Listar archivos con un nombre de un solo carácter**

```bash
touch a b c d e
ls ?
```
Salida:
```
a  b  c  d  e
```

- `[]` (corchetes): Coincide con cualquier carácter dentro de los corchetes.

**Ejemplo 11: Listar archivos que contengan un dígito**

```bash
touch file_1.txt file_2.txt file_A.txt
ls file_[0-9].txt
```
Salida:
```
file_1.txt  file_2.txt
```