# Permisos y Usuarios en Linux

## Usuarios y grupos

En Linux, cada archivo pertenece a un **usuario** (owner) y a un **grupo**.
Cada usuario tiene un identificador numérico:

| Identificador | Descripción |
|---------------|-------------|
| `UID` | User ID — identifica al usuario |
| `GID` | Group ID — identifica al grupo principal |
```bash
# Ver tu usuario actual
whoami

# Ver tu UID, GID y grupos
id

# Ejemplo de salida
uid=1000(gonza) gid=1000(gonza) groups=1000(gonza),27(sudo)
```

---

## Los tres tipos de permisos

| Permiso | Símbolo | Valor numérico | Sobre archivos | Sobre directorios |
|---------|---------|----------------|----------------|-------------------|
| Lectura | `r` | 4 | Leer contenido | Listar archivos (`ls`) |
| Escritura | `w` | 2 | Modificar contenido | Crear/eliminar archivos dentro |
| Ejecución | `x` | 1 | Ejecutar como programa | Entrar al directorio (`cd`) |
| Sin permiso | `-` | 0 | — | — |

---

## Los tres niveles de permisos
```
-rw-rw-r--
│└──┘└──┘└──┘
│  │   │   └── others  (todos los demás)
│  │   └─────── group   (el grupo dueño)
│  └─────────── user    (el dueño)
└────────────── tipo de archivo
```

### Tipo de archivo

| Símbolo | Tipo |
|---------|------|
| `-` | Archivo regular |
| `d` | Directorio |
| `l` | Link simbólico |
| `b` | Dispositivo de bloque |
| `c` | Dispositivo de carácter |

---

## Leer permisos con `ls -l`
```bash
$ ls -l archivo.txt
-rw-rw-r-- 1 gonza gonza 34 mar  3 00:26 archivo.txt
```

Desglose:
```
-  rw-  rw-  r--   1   gonza  gonza   34   mar 3 00:26   archivo.txt
│   │    │    │    │     │      │       │       │              │
│   │    │    │    │     │      │       │       │              └── nombre
│   │    │    │    │     │      │       │       └── fecha de modificación
│   │    │    │    │     │      │       └── tamaño en bytes
│   │    │    │    │     │      └── grupo dueño
│   │    │    │    │     └── usuario dueño
│   │    │    │    └── cantidad de hard links
│   │    │    └── permisos de others
│   │    └── permisos de group
│   └── permisos de user
└── tipo de archivo
```

---

## Notación octal

Los permisos también se expresan con números. Cada nivel (user/group/others)
se calcula sumando los valores de los permisos activos:

| Permiso | Valor |
|---------|-------|
| `r` | 4 |
| `w` | 2 |
| `x` | 1 |
| `-` | 0 |

### Ejemplos

| Octal | Simbólico | Cálculo |
|-------|-----------|---------|
| `7` | `rwx` | 4+2+1 |
| `6` | `rw-` | 4+2+0 |
| `5` | `r-x` | 4+0+1 |
| `4` | `r--` | 4+0+0 |
| `0` | `---` | 0+0+0 |
```bash
# -rw-rw-r-- en octal es 664
# user=rw(6)  group=rw(6)  others=r(4)
```

---

## `chmod` — cambiar permisos

### Notación simbólica
```bash
chmod [quien][operador][permiso] archivo

# quien:     u (user)  g (group)  o (others)  a (all)
# operador:  + agregar  - quitar  = asignar exacto
# permiso:   r  w  x

chmod u+x script.sh        # agregar ejecución al dueño
chmod g-w archivo.txt      # quitar escritura al grupo
chmod o=r archivo.txt      # others solo puede leer
chmod a+x script.sh        # todos pueden ejecutar
chmod u+x,g-w archivo.txt  # múltiples cambios a la vez
```

### Notación octal
```bash
chmod 644 archivo.txt    # rw-r--r--
chmod 755 script.sh      # rwxr-xr-x
chmod 600 privado.txt    # rw-------
chmod 777 archivo.txt    # rwxrwxrwx (evitar en producción)
```

---

## `chown` — cambiar dueño y grupo
```bash
chown usuario archivo.txt               # cambiar dueño
chown usuario:grupo archivo.txt         # cambiar dueño y grupo
chown :grupo archivo.txt                # cambiar solo el grupo
chown -R usuario:grupo directorio/      # recursivo
```
```bash
# Ejemplo
sudo chown gonza:gonza archivo.txt
```

---

## `chgrp` — cambiar grupo
```bash
chgrp grupo archivo.txt
chgrp -R grupo directorio/
```

---

## Permisos especiales

### SUID (Set User ID) — valor `4`

Cuando se ejecuta el archivo, corre con los permisos del **dueño**, no del que lo ejecuta.
```bash
chmod u+s programa       # simbólico
chmod 4755 programa      # octal

# Se muestra con 's' en lugar de 'x' en el user
-rwsr-xr-x
```

> Ejemplo real: `/usr/bin/passwd` usa SUID para que cualquier usuario pueda cambiar su contraseña.

### SGID (Set Group ID) — valor `2`

En archivos: corre con los permisos del grupo dueño.  
En directorios: los archivos creados dentro heredan el grupo del directorio.
```bash
chmod g+s directorio/
chmod 2755 directorio/

# Se muestra con 's' en el group
drwxr-sr-x
```

### Sticky Bit — valor `1`

En directorios: solo el dueño del archivo puede eliminarlo, aunque otros tengan permiso de escritura.
```bash
chmod +t /tmp
chmod 1777 /tmp

# Se muestra con 't' en others
drwxrwxrwt
```

> Ejemplo real: el directorio `/tmp` usa sticky bit.

---

## `umask` — permisos por defecto

`umask` define qué permisos se **restan** al crear archivos o directorios.
```bash
umask          # ver umask actual
umask 022      # asignar umask

# Con umask 022:
# Archivos:     666 - 022 = 644  →  rw-r--r--
# Directorios:  777 - 022 = 755  →  rwxr-xr-x
```

---

## Permisos en la práctica — casos comunes

| Caso | Octal | Simbólico |
|------|-------|-----------|
| Archivo de texto normal | `644` | `-rw-r--r--` |
| Script ejecutable | `755` | `-rwxr-xr-x` |
| Archivo privado | `600` | `-rw-------` |
| Directorio compartido | `775` | `drwxrwxr-x` |
| Directorio privado | `700` | `drwx------` |

---

## Resumen de comandos

| Comando | Descripción |
|---------|-------------|
| `ls -l` | Ver permisos de archivos |
| `stat archivo` | Ver metadata completa incluyendo permisos |
| `chmod` | Cambiar permisos |
| `chown` | Cambiar dueño (y grupo) |
| `chgrp` | Cambiar grupo |
| `umask` | Ver/configurar permisos por defecto |
| `id` | Ver UID, GID y grupos del usuario actual |
| `whoami` | Ver usuario actual |
| `groups` | Ver grupos a los que pertenece el usuario |
