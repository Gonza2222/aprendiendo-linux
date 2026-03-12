# 🔗 Pipelines, Filtros y Búsquedas en Bash

Una de las características más poderosas de Linux es poder **encadenar comandos** para procesar texto y datos de forma eficiente.

---

## `|` — El Pipe (tubería)

Toma la salida de un comando y la pasa como entrada al siguiente.

```bash
comando1 | comando2 | comando3
```

```bash
ls | sort              # lista los archivos ordenados
cat archivo.txt | wc -l  # cuenta las líneas de un archivo
```

> 💡 Podés encadenar tantos comandos como quieras con `|`.

---

## `sort` — Ordenar líneas

```bash
sort archivo.txt            # ordena alfabéticamente
sort -r archivo.txt         # ordena en orden inverso
sort -n numeros.txt         # ordena numéricamente
sort -u archivo.txt         # ordena y elimina duplicados
sort -k2 archivo.txt        # ordena por la segunda columna
```

### Con pipe
```bash
ls | sort                   # lista archivos ordenados
cat nombres.txt | sort -r   # nombres en orden inverso
```

---

## `uniq` — Eliminar líneas duplicadas

> ⚠️ `uniq` solo detecta duplicados **consecutivos**. Usalo siempre después de `sort`.

```bash
uniq archivo.txt            # elimina duplicados consecutivos
uniq -c archivo.txt         # cuenta cuántas veces aparece cada línea
uniq -d archivo.txt         # muestra solo las líneas duplicadas
uniq -u archivo.txt         # muestra solo las líneas únicas
```

### Con pipe
```bash
sort archivo.txt | uniq           # ordenar y eliminar duplicados
sort archivo.txt | uniq -c        # contar repeticiones
sort archivo.txt | uniq -c | sort -rn  # ordenar por más repetido
```

---

## `wc` — Contar líneas, palabras y caracteres

```bash
wc archivo.txt       # muestra líneas, palabras y caracteres
wc -l archivo.txt    # solo líneas
wc -w archivo.txt    # solo palabras
wc -c archivo.txt    # solo caracteres (bytes)
```

### Con pipe
```bash
ls | wc -l                     # cuántos archivos hay en la carpeta
cat archivo.txt | wc -w        # cuántas palabras tiene el archivo
grep "error" log.txt | wc -l   # cuántas líneas contienen "error"
```

---

## `grep` — Buscar texto

```bash
grep "palabra" archivo.txt       # busca líneas que contengan "palabra"
grep -i "palabra" archivo.txt    # ignora mayúsculas/minúsculas
grep -r "palabra" carpeta/       # busca en todos los archivos de una carpeta
grep -n "palabra" archivo.txt    # muestra el número de línea
grep -v "palabra" archivo.txt    # muestra las líneas que NO contienen "palabra"
grep -c "palabra" archivo.txt    # cuenta cuántas líneas contienen "palabra"
grep -l "palabra" *.txt          # muestra qué archivos contienen "palabra"
```

### Con pipe
```bash
ls | grep ".txt"                  # filtra solo los archivos .txt
cat log.txt | grep "error"        # busca errores en un log
cat log.txt | grep -i "warning"   # busca warnings sin importar mayúsculas
ps aux | grep "firefox"           # busca si firefox está corriendo
```

---

## `head` — Ver las primeras líneas

```bash
head archivo.txt        # muestra las primeras 10 líneas (por defecto)
head -n 5 archivo.txt   # muestra las primeras 5 líneas
head -n 1 archivo.txt   # muestra solo la primera línea
```

### Con pipe
```bash
ls | head -n 5           # muestra solo los primeros 5 archivos
sort archivo.txt | head  # los 10 primeros en orden alfabético
```

---

## `tail` — Ver las últimas líneas

```bash
tail archivo.txt         # muestra las últimas 10 líneas (por defecto)
tail -n 5 archivo.txt    # muestra las últimas 5 líneas
tail -f archivo.txt      # sigue el archivo en tiempo real (útil para logs)
```

### Con pipe
```bash
ls | tail -n 5                    # muestra solo los últimos 5 archivos
sort archivo.txt | tail           # los 10 últimos en orden alfabético
cat log.txt | grep "error" | tail # los últimos errores del log
```

> 💡 `tail -f` es muy útil para monitorear logs en tiempo real mientras se van generando.

---

## `tee` — Ver Y guardar al mismo tiempo

Muestra la salida en pantalla **y** la guarda en un archivo a la vez.

```bash
comando | tee archivo.txt       # muestra y guarda (sobreescribe)
comando | tee -a archivo.txt    # muestra y agrega al archivo
```

```bash
ls | tee lista.txt                        # ve la lista y la guarda
cat log.txt | grep "error" | tee errores.txt  # ve los errores y los guarda
```

> 💡 A diferencia de `>`, con `tee` seguís viendo la salida en pantalla mientras se guarda.

---

## Combinaciones poderosas

```bash
# Los 5 archivos más grandes de la carpeta
ls -lS | head -n 5

# Palabras más repetidas en un archivo
cat archivo.txt | tr ' ' '\n' | sort | uniq -c | sort -rn | head -10

# Buscar errores en un log y guardarlos
cat sistema.log | grep -i "error" | tee errores.txt

# Contar cuántos procesos está corriendo un usuario
ps aux | grep "gonza" | wc -l

# Ver los últimos 20 errores en tiempo real
tail -f sistema.log | grep "error"

# Buscar en varios archivos y ordenar resultados
grep -r "TODO" *.txt | sort | uniq
```

---

## Resumen de comandos

| Comando | Para qué sirve |
|---|---|
| `\|` | Encadena comandos pasando la salida como entrada |
| `sort` | Ordena líneas |
| `uniq` | Elimina o cuenta líneas duplicadas |
| `wc` | Cuenta líneas, palabras o caracteres |
| `grep` | Busca texto por patrón |
| `head` | Muestra las primeras líneas |
| `tail` | Muestra las últimas líneas |
| `tee` | Muestra y guarda la salida al mismo tiempo |

---

> 💡 **Tip:** La verdadera potencia de estos comandos está en combinarlos con `|`. Solos son útiles, juntos son muy poderosos.
