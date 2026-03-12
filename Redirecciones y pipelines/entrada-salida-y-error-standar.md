# 📡 Entrada, Salida y Error Estándar en Bash

En Linux toda comunicación de la shell pasa por 3 canales. Entender esto es clave para manejar comandos como un pro.

---

## Los 3 canales

| Canal | Número | Qué es |
|---|---|---|
| `stdin`  | 0 | Lo que **entrás** al comando (por defecto: el teclado) |
| `stdout` | 1 | Lo que **sale** cuando todo va bien |
| `stderr` | 2 | Lo que **sale cuando hay un error** |

---

## `stdout` — Salida estándar

Por defecto el resultado de un comando se muestra en pantalla. Con `>` y `>>` lo redirigís a un archivo.

```bash
ls                  # muestra el resultado en pantalla
ls > lista.txt      # guarda el resultado en un archivo (sobreescribe)
ls >> lista.txt     # agrega el resultado al archivo sin borrar lo que había
```

> ⚠️ `>` borra el contenido anterior del archivo. `>>` lo conserva y agrega al final.

---

## `stdin` — Entrada estándar

Por defecto los comandos esperan que vos escribas. Con `<` le pasás un archivo como entrada.

```bash
cat < archivo.txt        # lee el archivo como si lo escribieras vos
sort < nombres.txt       # ordena las líneas del archivo
wc -l < archivo.txt      # cuenta las líneas del archivo
```

### `<<` — Here Document

Permite escribir varias líneas de input directamente en la terminal hasta una palabra clave de cierre.

```bash
cat << FIN
Hola
esto es una prueba
FIN
```
> Todo lo que escribís entre `<< FIN` y `FIN` se toma como entrada del comando.

---

## `stderr` — Salida de errores

Los errores van por un canal separado. Con `2>` los redirigís a un archivo.

```bash
ls carpeta_falsa 2> errores.txt    # guarda el error en un archivo (sobreescribe)
ls carpeta_falsa 2>> errores.txt   # agrega el error al archivo
```

---

## Redirigir `stdout` y `stderr` juntos

### Forma clásica (todas las versiones de Bash)

```bash
ls > todo.txt 2>&1
```
Primero redirige `stdout` al archivo, después redirige `stderr` al mismo lugar que `stdout`.

> ⚠️ El orden importa: `2>&1` siempre va después de `>`.

### Forma moderna (Bash 4+)

```bash
ls &> todo.txt     # redirige stdout y stderr al archivo (sobreescribe)
ls &>> todo.txt    # redirige stdout y stderr al archivo (agrega)
```
> ✅ `&>` es más corto y hace lo mismo que `> archivo 2>&1`.

---

## `/dev/null` — El agujero negro 🕳️

Es un archivo especial de Linux que descarta todo lo que recibe. Se usa para ignorar salidas que no te interesan.

```bash
ls carpeta_falsa 2>/dev/null          # ignora los errores
ls > /dev/null                        # ignora el resultado
ls > /dev/null 2>&1                   # ignora todo (stdout y stderr)
ls &> /dev/null                       # ignora todo (forma moderna)
```

---

## Resumen de operadores

| Operador | Qué hace |
|---|---|
| `>`      | Redirige stdout a un archivo (sobreescribe) |
| `>>`     | Redirige stdout a un archivo (agrega) |
| `<`      | Usa un archivo como stdin |
| `<<`     | Usa texto escrito en terminal como stdin (Here Document) |
| `2>`     | Redirige stderr a un archivo (sobreescribe) |
| `2>>`    | Redirige stderr a un archivo (agrega) |
| `2>&1`   | Redirige stderr al mismo lugar que stdout |
| `&>`     | Redirige stdout y stderr a un archivo (moderno, sobreescribe) |
| `&>>`    | Redirige stdout y stderr a un archivo (moderno, agrega) |
| `/dev/null` | Descarta todo lo que recibe |

---

## Ejemplos prácticos

```bash
# Guardar resultado y errores por separado
ls > resultado.txt 2> errores.txt

# Ejecutar un script ignorando todo lo que imprima
bash script.sh &> /dev/null

# Guardar solo los errores de un comando largo
find / -name "config.txt" 2> errores.txt

# Agregar logs a un archivo existente
echo "$(date): tarea completada" >> log.txt
```

---

> 💡 **Tip:** Si un comando tira muchos errores que no te interesan, usá `2>/dev/null` para limpiar la salida y ver solo lo importante.
