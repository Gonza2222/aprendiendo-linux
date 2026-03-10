# 🐚 Expansiones de la Shell (Bash)

Referencia rápida de las expansiones más usadas en Bash/Linux.

---

## `~` — Directorio Home

```bash
cd ~              # va a /home/tuusuario
ls ~/Documentos   # lista la carpeta Documentos del home
```

---

## `*` — Wildcard (cualquier cadena de caracteres)

```bash
ls *.txt          # todos los archivos .txt
rm foto*          # todo lo que empiece con "foto"
cp *.jpg imagenes/
```

---

## `?` — Un solo carácter

```bash
ls foto?.jpg      # foto1.jpg, fotoA.jpg, etc.
ls archivo?.txt   # archivo1.txt, archivox.txt, etc.
```

---

## `[...]` — Rango o conjunto de caracteres

```bash
ls foto[123].jpg     # foto1.jpg, foto2.jpg o foto3.jpg
ls archivo[a-z].txt  # archivoa.txt ... archivoz.txt
ls nota[0-9].md      # nota0.md ... nota9.md
```

---

## `{}` — Expansión de listas o secuencias

```bash
mkdir {enero,febrero,marzo}       # crea 3 carpetas
touch archivo{1..5}.txt           # archivo1.txt al archivo5.txt
cp config.txt config.txt.{bak,old} # crea dos copias con distinto nombre
```

---

## `$( )` — Sustitución de comandos

```bash
echo "Hoy es $(date)"
echo "Estoy en $(pwd)"
ls $(dirname /etc/hosts)
```

---

## `$VAR` — Variables de entorno

```bash
echo $HOME    # /home/tuusuario
echo $USER    # tu nombre de usuario
echo $PATH    # rutas de binarios del sistema
echo $SHELL   # shell que estás usando
```

---

## Combinaciones útiles

```bash
ls ~/*.txt                  # todos los .txt en el home
touch ~/proyectos/{main,test,README}.py
echo "Usuario: $USER en $(hostname)"
```

---

> 💡 **Tip:** Podés probar cualquier expansión con `echo` antes de ejecutarla para ver cómo la interpreta la shell.
> ```bash
> echo rm *.txt   # muestra qué archivos borraría, sin borrar nada
> ```
