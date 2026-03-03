# Inodos en Linux

## ¿Qué es un inodo?

Un inodo es una estructura de datos que almacena la **metadata** de un archivo:

- Permisos
- UID / GID
- Tamaño
- Fechas (Access, Modify, Change)
- Cantidad de enlaces
- Bloques donde se guardan los datos

> ⚠ El nombre del archivo **NO** está en el inodo.  
> El nombre está almacenado en el directorio, que contiene una referencia al inodo.

---

## Ver el número de inodo

Para ver el número de inodo de un archivo:

```bash
ls -i archivo.txt
```

Salida de ejemplo:

```bash
2359510 archivo.txt
```

---

## Ver información completa del archivo

Para obtener información detallada:

```bash
stat archivo.txt
```

Salida de ejemplo:

```bash
File: archivo.txt
Size: 34            Blocks: 8          IO Block: 4096   regular file
Device: 803h/2051d  Inode: 2359510     Links: 1
Access: (0664/-rw-rw-r--)  Uid: (1000/gonza)   Gid: (1000/gonza)
Access: 2026-03-03 00:26:53.986457374 -0300
Modify: 2026-03-03 00:26:18.247990500 -0300
Change: 2026-03-03 00:26:18.247990500 -0300
Birth:  2026-03-03 00:26:18.246990546 -0300
```

---

## Explicación detallada de los campos

| Campo | Valor | Descripción |
|-------|-------|-------------|
| Inode | 2359510 | Identificador único dentro del filesystem |
| Size | 34 bytes | Tamaño real del contenido del archivo |
| Blocks | 8 | Bloques de disco asignados (8 × 512 = 4096 bytes) |
| IO Block | 4096 | Tamaño del bloque del filesystem |
| Links | 1 | Cantidad de hard links que apuntan al mismo inodo |
| Uid/Gid | 1000/gonza | Usuario propietario y grupo |
| 0664 | -rw-rw-r-- | Permisos del archivo |
| atime | 00:26:53 | Última vez que el archivo fue leído |
| mtime | 00:26:18 | Última modificación del contenido |
| ctime | 00:26:18 | Último cambio en la metadata del inodo |
| Birth | 00:26:18 | Fecha de creación del archivo |

---

## Estructura lógica de un archivo en Linux

En Linux, un archivo funciona de la siguiente manera:

Directorio → Inodo → Bloques de datos

- El directorio almacena el nombre del archivo.
- El inodo almacena la metadata.
- Los bloques contienen el contenido real del archivo.

---

## Conclusión

El inodo representa la identidad real del archivo dentro del sistema de archivos.  
Comprender su funcionamiento es fundamental para entender cómo Linux maneja archivos, permisos y enlaces.

