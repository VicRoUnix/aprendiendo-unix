## Comandos de Navegacion y gestion de archivos
### Guía rápida de comandos esenciales de navegación y gestión de archivos en Linux

---

#### 📖 `man`
Consulta el manual de cualquier comando:
```bash
man echo
man ls
```

---

#### 📂 `pwd`
Muestra la ruta completa del directorio actual:
```bash
pwd
# /home/usuario
```

---

#### 📁 `cd`
Navega entre directorios:
```bash
pwd
# /home/usuario
cd /etc
pwd
# /etc
cd ..
pwd
# /
```

---

#### 📄 `ls`
Lista el contenido de un directorio.

**Banderas útiles:**
- `-l`  → Detalles completos
- `-a`  → Incluye archivos ocultos
- `-h`  → Tamaños legibles
- `-p`  → Distingue directorios

**Ejemplos:**
```bash
ls /usr
ls -la
ls -lh
```

---

#### 🗂️ `mkdir`
Crea nuevos directorios.

**Bandera útil:**  
- `-p`  → Crea directorios anidados

**Ejemplo:**
```bash
mkdir myfolder
mkdir -p myfolder/level2/level3
```

---

#### 🗑️ `rmdir`
Elimina directorios vacíos.

**Bandera útil:**  
- `-p`  → Elimina directorios vacíos de forma recursiva

**Ejemplo:**
```bash
rmdir empty_folder
rmdir -p myfolder/level2/level3
```

---

#### 📄 `touch`
Crea archivos vacíos o actualiza la fecha de modificación:
```bash
touch new_file.txt
```

---

#### 📋 `cp`
Copia archivos y directorios.

**Banderas útiles:**
- `-r`  → Copia recursiva (carpetas)
- `-p`  → Conserva permisos y fechas
- `-v`  → Muestra detalles

**Ejemplo:**
```bash
cp my_file.txt /ruta/destino/
cp -r folder1 folder2
cp -pv my_document.txt /home/user/backups/
```

---

#### 🚚 `mv`
Mueve o renombra archivos y directorios:
```bash
mv old_name.txt new_name.txt
mv my_file.txt /ruta/nueva/
```

---

#### ❌ `rm`
Elimina archivos y directorios.

**Banderas útiles:**
- `-r`  → Elimina recursivamente
- `-f`  → Fuerza la eliminación
- `-i`  → Pide confirmación

**Ejemplo:**
```bash
rm my_file.txt
rm -r my_folder
rm -rf /ruta/peligrosa/
rm -i file.txt
```

---

### Comandos para manipular contenido

---

#### 📝 `echo`
Muestra texto en la terminal:
```bash
echo "Hello World!"
# Hello World!
```

---

#### 📖 `cat`
Muestra el contenido de archivos:
```bash
cat /etc/os-release
cat file1.txt file2.txt
```

---

#### 🔍 `find`
Busca archivos y directorios según criterios.

**Banderas útiles:**
- `-name "patrón"`  → Por nombre
- `-type f|d`       → Solo archivos (`f`) o directorios (`d`)
- `-exec ...`       → Ejecuta comandos sobre los resultados

**Ejemplo:**
```bash
find . -name "report.txt"
```

---

#### 🕵️ `grep`
Busca texto dentro de archivos o salidas.

**Banderas útiles:**
- `-i`  → Ignora mayúsculas/minúsculas
- `-n`  → Muestra número de línea
- `-v`  → Invierte la búsqueda
- `-E`  → Expresiones regulares extendidas

**Ejemplo:**
```bash
grep "fail" /var/log/syslog
```

---

#### ⬆️ `head`
Muestra las primeras líneas de un archivo.

**Bandera útil:**  
- `-n <n>`  → Número de líneas

**Ejemplo:**
```bash
head /etc/passwd
head -n 5 /var/log/dmesg
```

---

#### ⬇️ `tail`
Muestra las últimas líneas de un archivo.

**Banderas útiles:**
- `-n <n>`  → Número de líneas
- `-f`      → Sigue el archivo en tiempo real

**Ejemplo:**
```bash
tail /var/log/auth.log
tail -f /var/log/nginx/access.log
```

---

#### 📜 `less`
Visualiza archivos de forma interactiva:
```bash
less large_log_file.txt
```