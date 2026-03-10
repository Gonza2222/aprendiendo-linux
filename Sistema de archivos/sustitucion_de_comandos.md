# 🔄 Sustitución de Comandos en Bash

Permite usar la **salida de un comando** como valor dentro de otro comando.

---

## Sintaxis

```bash
$(comando)     # forma moderna y recomendada
`comando`      # forma antigua (backticks), funciona igual
```

---

## Ejemplos básicos

```bash
echo "Hoy es $(date)"
echo "Estoy en $(pwd)"
echo "Usuario: $(whoami)"
echo "Kernel: $(uname -r)"
```

---

## Guardar resultado en una variable

```bash
fecha=$(date)
usuario=$(whoami)
ruta=$(pwd)

echo "Fecha: $fecha"
echo "Usuario: $usuario"
echo "Ruta actual: $ruta"
```

---

## Usar dentro de comandos

```bash
# Crear carpeta con la fecha de hoy
mkdir backup_$(date +%Y-%m-%d)

# Copiar archivos al directorio actual
cp /etc/hosts $(pwd)/hosts_backup

# Contar archivos en una carpeta
echo "Hay $(ls | wc -l) archivos aquí"
```

---

## Anidado (uno dentro de otro)

```bash
echo "Archivos en home: $(ls $(echo $HOME) | wc -l)"
```

> 💡 Con backticks `` ` `` anidar es más complicado, por eso se prefiere `$()`.

---

## Casos útiles del día a día

```bash
# Ver qué versión de python tenés instalada
echo "Python: $(python3 --version)"

# Saber cuánto pesa una carpeta
echo "Tamaño: $(du -sh ~/Documentos)"

# Usar la salida de find
cat $(find . -name "config.txt")
```

---

> 💡 **Tip:** Si el comando falla o no existe, la sustitución devuelve vacío. Podés probarlo con:
> ```bash
> echo "Resultado: $(comandofalso 2>/dev/null)"
> ```
