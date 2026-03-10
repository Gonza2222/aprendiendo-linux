# 🔤 Comillas en Bash: Simples y Dobles

En Bash las comillas **no son lo mismo**. Cada tipo tiene un comportamiento distinto.

---

## `" "` — Comillas Dobles

Permiten que Bash **interprete** variables y sustituciones de comandos adentro.

```bash
nombre="Gonza"

echo "Hola $nombre"         # → Hola Gonza
echo "Estoy en $(pwd)"      # → Estoy en /home/gonza
echo "Usuario: $USER"       # → Usuario: gonza
```

> ✅ Las variables y `$()` **sí funcionan** adentro.

---

## `' '` — Comillas Simples

Todo lo que está adentro se toma **literalmente**. Bash no interpreta nada.

```bash
nombre="Gonza"

echo 'Hola $nombre'         # → Hola $nombre
echo 'Estoy en $(pwd)'      # → Estoy en $(pwd)
echo 'Usuario: $USER'       # → Usuario: $USER
```

> ❌ Las variables y `$()` **NO funcionan** adentro, se imprimen tal cual.

---

## Comparación directa

```bash
echo "Hola $USER"    # → Hola gonza       (interpreta la variable)
echo 'Hola $USER'    # → Hola $USER       (lo toma literal)
```

---

## ¿Cuándo usar cada una?

| Situación | Usar |
|---|---|
| Necesitás usar variables | `" "` dobles |
| Necesitás usar `$()` | `" "` dobles |
| Querés que se imprima tal cual | `' '` simples |
| Nombres de archivos con espacios | cualquiera de las dos |

---

## Nombres de archivos con espacios

Ambas funcionan para manejar archivos cuyos nombres tienen espacios:

```bash
cat "archivo con espacios.txt"
cat 'archivo con espacios.txt'
```

---

## Ejemplo práctico combinando las dos

```bash
echo "Hoy es $(date +%Y-%m-%d) y el usuario es $USER"
# → Hoy es 2026-03-10 y el usuario es gonza

echo 'Hoy es $(date +%Y-%m-%d) y el usuario es $USER'
# → Hoy es $(date +%Y-%m-%d) y el usuario es $USER
```

---

> 💡 **Regla simple:** Si necesitás que Bash procese algo → `" "`. Si querés que se imprima exacto → `' '`.
