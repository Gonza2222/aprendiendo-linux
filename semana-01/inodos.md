¿Qué es un inodo?
Un inodo es una estructura de datos que almacena la metadata de un archivo:
Permisos
UID / GID
Tamaño
Fechas (Access, Modify, Change)
Cantidad de enlaces
Bloques donde se guardan los datos

El nombre del archivo NO está en el inodo.
El nombre está en el directorio, que apunta al inodo.

Para ver el numero de un inodo ej:
ls -i archivo.txt
Salida:
2359510 archivo.txt

Para ver la información completa:
stat archivo.txt

Salida:
File: archivo.txt
  Size: 34            Blocks: 8          IO Block: 4096   regular file
Device: 803h/2051d    Inode: 2359510     Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/gonza)   Gid: ( 1000/gonza)
Access: 2026-03-03 00:26:53.986457374 -0300
Modify: 2026-03-03 00:26:18.247990500 -0300
Change: 2026-03-03 00:26:18.247990500 -0300
 Birth: 2026-03-03 00:26:18.246990546 -0300

Explicacion detallada:
| Campo | Valor | Descripción |
|-------|-------|-------------|
| `Inode` | 2359510 | Identificador único en el filesystem |
| `Size` | 34 bytes | Tamaño del contenido |
| `Blocks` | 8 | Bloques de disco asignados (8 × 512 = 4096 bytes) |
| `IO Block` | 4096 | Tamaño del bloque del filesystem |
| `Links` | 1 | Cantidad de hard links apuntando a este inodo |
| `Uid/Gid` | 1000/gonza | Propietario y grupo |
| `Access (0664)` | -rw-rw-r-- | Permisos |
| `atime` | 00:26:53 | Última lectura |
| `mtime` | 00:26:18 | Última modificación del contenido |
| `ctime` | 00:26:18 | Último cambio del inodo |
| `Birth` | 00:26:18 | Creación del archivo |

