# 🐧 Comandos Básicos de la Shell

> Referencia rápida de comandos esenciales para trabajar en la terminal Linux/Unix.

---

## 📁 Navegación

| Comando | Descripción |
|---------|-------------|
| `pwd` | Muestra el directorio actual |
| `ls` | Lista archivos y directorios |
| `cd` | Cambia de directorio |
| `cd ..` | Sube un nivel |

```bash
pwd                  # /home/usuario
ls                   # lista básica
ls -l                # lista detallada (permisos, tamaño, fecha)
ls -la               # incluye archivos ocultos
ls -lh               # tamaños legibles (KB, MB)
ls -lt               # ordenado por fecha de modificación

cd /etc              # ruta absoluta
cd documentos        # ruta relativa
cd ~                 # va al home del usuario
cd -                 # vuelve al directorio anterior
cd ../..             # sube dos niveles
```

---

## 👀 Visualización de archivos

| Comando | Descripción |
|---------|-------------|
| `tree` | Muestra estructura en árbol |
| `cat` | Muestra contenido completo |
| `less` | Muestra contenido paginado |
| `head` | Muestra las primeras líneas |
| `tail` | Muestra las últimas líneas |

```bash
tree -L 1            # árbol nivel 1
tree -L 2 --dirsfirst  # nivel 2, directorios primero
tree -a              # incluye archivos ocultos

cat archivo.txt      # muestra todo el contenido
cat -n archivo.txt   # con números de línea

less archivo.txt     # navegación con flechas, q para salir
less +G archivo.txt  # abre al final del archivo

head archivo.txt         # primeras 10 líneas (default)
head -n 20 archivo.txt   # primeras 20 líneas

tail archivo.txt         # últimas 10 líneas
tail -n 20 archivo.txt   # últimas 20 líneas
tail -f /var/log/syslog  # sigue el archivo en tiempo real (logs)
```

---

## 📄 Manejo de archivos y directorios

| Comando | Descripción |
|---------|-------------|
| `touch` | Crea un archivo vacío |
| `mkdir` | Crea un directorio |
| `cp` | Copia archivos/directorios |
| `mv` | Mueve o renombra |
| `rm` | Elimina archivos/directorios |

```bash
touch archivo.txt            # crea archivo vacío
touch archivo.{txt,md,sh}    # crea varios a la vez

mkdir carpeta                # crea directorio
mkdir -p proyectos/src/utils # crea estructura completa

cp archivo.txt copia.txt         # copia archivo
cp -r carpeta/ destino/          # copia directorio (recursivo)
cp -rp carpeta/ destino/         # copia preservando permisos

mv archivo.txt nuevo_nombre.txt  # renombra
mv archivo.txt ~/documentos/     # mueve

rm archivo.txt               # elimina archivo
rm -r carpeta/               # elimina directorio y contenido
rm -i archivo.txt            # pide confirmación antes de borrar
```

> ⚠️ `rm` no tiene papelera de reciclaje. Usá `-i` para confirmar antes de borrar.

---

## 🔍 Búsqueda

| Comando | Descripción |
|---------|-------------|
| `find` | Busca archivos por nombre, tipo, fecha |
| `grep` | Busca texto dentro de archivos |
| `which` | Muestra la ruta de un comando |
| `locate` | Búsqueda rápida en base de datos |

```bash
find . -name "*.txt"             # busca .txt desde aquí
find /home -name "config*"       # busca por nombre
find . -type d                   # solo directorios
find . -type f -mtime -7         # modificados en los últimos 7 días
find . -size +1M                 # archivos mayores a 1MB

grep "error" archivo.log         # busca "error" en un archivo
grep -r "TODO" ./src/            # búsqueda recursiva
grep -i "error" archivo.log      # case-insensitive
grep -n "error" archivo.log      # muestra número de línea
grep -v "debug" archivo.log      # líneas que NO contienen "debug"
grep -c "error" archivo.log      # cuenta coincidencias

which python3                    # /usr/bin/python3
which bash                       # /bin/bash
```

---

## 📝 Edición rápida

| Comando | Descripción |
|---------|-------------|
| `nano` | Editor simple en terminal |
| `echo` | Imprime texto o escribe en archivo |
| `>` | Redirige salida (sobreescribe) |
| `>>` | Redirige salida (agrega al final) |

```bash
nano archivo.txt             # abre editor (Ctrl+O guardar, Ctrl+X salir)

echo "Hola mundo"            # imprime en pantalla
echo "texto" > archivo.txt   # escribe en archivo (sobreescribe)
echo "más texto" >> archivo.txt  # agrega al final del archivo

# Crear archivo con contenido rápido
cat > notas.txt << EOF
Línea 1
Línea 2
EOF
```

---

## ⚙️ Sistema y procesos

| Comando | Descripción |
|---------|-------------|
| `ps` | Lista procesos activos |
| `top` / `htop` | Monitor de procesos en tiempo real |
| `kill` | Termina un proceso |
| `df` | Espacio en disco |
| `du` | Uso de disco por directorio |
| `free` | Memoria RAM disponible |
| `uname` | Info del sistema |

```bash
ps aux                       # todos los procesos
ps aux | grep python         # filtrar procesos de python

top                          # monitor interactivo (q para salir)
htop                         # versión mejorada (si está instalado)

kill 1234                    # termina proceso con PID 1234
kill -9 1234                 # fuerza terminación

df -h                        # espacio en disco legible
du -sh carpeta/              # tamaño de una carpeta
du -sh *                     # tamaño de todo en el directorio actual

free -h                      # memoria RAM y swap

uname -a                     # info completa del sistema
uname -r                     # versión del kernel
```

---

## 🔐 Permisos

| Comando | Descripción |
|---------|-------------|
| `chmod` | Cambia permisos |
| `chown` | Cambia propietario |
| `sudo` | Ejecuta como superusuario |

```bash
chmod +x script.sh           # agrega permiso de ejecución
chmod 755 script.sh          # rwxr-xr-x
chmod 644 archivo.txt        # rw-r--r--
chmod -R 755 carpeta/        # recursivo

chown usuario:grupo archivo.txt
chown -R usuario:grupo carpeta/

sudo apt update              # actualizar paquetes (Debian/Ubuntu)
sudo apt install htop        # instalar un paquete
sudo !!                      # repite el último comando como sudo
```

---

## 🔗 Pipes y redirección

```bash
# Pipe | — encadena la salida de un comando con la entrada del siguiente
ls -la | grep ".txt"         # filtra resultado de ls
cat archivo.log | grep "error" | wc -l  # cuenta errores

# Redirección
comando > salida.txt         # guarda salida en archivo
comando >> salida.txt        # agrega al archivo
comando 2> errores.txt       # guarda solo errores
comando 2>&1 > todo.txt      # guarda salida y errores juntos

# Ejemplos útiles
ls -lt | head -5             # los 5 archivos más recientes
ps aux | grep python | grep -v grep  # procesos python en ejecución
find . -name "*.log" | xargs rm      # borrar todos los .log encontrados
```

---

## 🧰 Utilidades

| Comando | Descripción |
|---------|-------------|
| `clear` | Limpia la terminal |
| `history` | Historial de comandos |
| `man` | Manual de un comando |
| `wc` | Cuenta líneas, palabras, caracteres |
| `sort` | Ordena líneas |
| `uniq` | Elimina duplicados |
| `cut` | Extrae columnas de texto |
| `date` | Fecha y hora actual |

```bash
clear                        # limpia pantalla (o Ctrl+L)

history                      # muestra historial
history | tail -20           # últimos 20 comandos
!200                         # ejecuta el comando número 200 del historial
!!                           # repite el último comando
Ctrl+R                       # búsqueda en historial (interactivo)

man ls                       # manual completo de ls
man grep                     # manual de grep

wc -l archivo.txt            # cuenta líneas
wc -w archivo.txt            # cuenta palabras

sort lista.txt               # ordena alfabéticamente
sort -r lista.txt            # ordena en reversa
sort -n numeros.txt          # ordena numéricamente

sort lista.txt | uniq        # elimina líneas duplicadas
sort lista.txt | uniq -c     # cuenta repeticiones

date                         # fecha y hora actual
date +"%Y-%m-%d"             # formato personalizado: 2024-01-15
```

---

## ⌨️ Atajos de teclado

| Atajo | Acción |
|-------|--------|
| `Ctrl+L` | Limpia la terminal (igual que `clear`) |
| `Ctrl+C` | Cancela el comando actual |
| `Ctrl+Z` | Pausa el proceso (envía a background) |
| `Ctrl+D` | Cierra la sesión / EOF |
| `Ctrl+R` | Busca en el historial |
| `Tab` | Autocompletar |
| `Tab Tab` | Muestra todas las opciones |
| `↑ / ↓` | Navega el historial |
| `Ctrl+A` | Va al inicio de la línea |
| `Ctrl+E` | Va al final de la línea |
| `Ctrl+U` | Borra desde el cursor al inicio |
| `Ctrl+K` | Borra desde el cursor al final |

---

## 🏷️ Alias

```bash
# Ver alias actuales
alias

# Crear alias temporales (solo en la sesión actual)
alias ll='ls -la'
alias ..='cd ..'
alias ...='cd ../..'
alias gs='git status'
alias gp='git push'
alias update='sudo apt update && sudo apt upgrade -y'

# Para hacerlos permanentes, agregalos en ~/.bashrc o ~/.zshrc
echo "alias ll='ls -la'" >> ~/.bashrc
source ~/.bashrc             # recarga la configuración

# Eliminar un alias
unalias ll
```

---

## 📚 Variables de entorno

```bash
echo $HOME               # directorio home: /home/usuario
echo $USER               # nombre de usuario
echo $PATH               # rutas donde se buscan los comandos
echo $SHELL              # shell actual: /bin/bash

env                      # muestra todas las variables de entorno
export MI_VAR="valor"    # crea variable de entorno
echo $MI_VAR             # valor
```

---

## 🗺️ Rutas: absolutas vs relativas

```
Sistema de archivos Linux:
/
├── home/
│   └── usuario/         ← $HOME (~)
│       ├── documentos/
│       └── proyectos/
├── etc/                 ← configuraciones del sistema
├── var/
│   └── log/             ← logs del sistema
└── usr/
    └── bin/             ← comandos del sistema
```

```bash
# Ruta absoluta — empieza desde la raíz /
cd /home/usuario/documentos
cat /etc/hosts

# Ruta relativa — relativa al directorio actual
cd documentos            # si ya estás en /home/usuario
cat ../otro_usuario/archivo.txt

# Atajos de ruta
~    →  /home/usuario      (home del usuario)
.    →  directorio actual
..   →  directorio padre
-    →  directorio anterior (con cd -)
```

---

> 💡 **Tips finales:**
> - Usá `man <comando>` o `<comando> --help` para ver todas las opciones.
> - Usá `Tab` para autocompletar rutas y comandos.
> - Usá `Ctrl+R` para buscar en el historial en vez de reescribir comandos largos.
> - Antes de usar `rm`, verificá con `ls` o `echo` qué archivos serán afectados.

