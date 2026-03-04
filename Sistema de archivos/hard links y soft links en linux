# Enlaces en Linux: Hard Links y Soft Links

En Linux existen dos tipos principales de enlaces:

- Hard Link (enlace duro)
- Soft Link o Symbolic Link (enlace simbolico)

Comprender la diferencia es fundamental para entender como funciona el sistema de archivos.

---

## 1. Hard Link (Enlace Duro)

Un hard link es un nuevo nombre que apunta al mismo inodo que el archivo original.

### Crear un hard link

```bash
ln archivo.txt copia.txt
```

### Que sucede internamente

Si ejecutamos:

```bash
ls -i archivo.txt copia.txt
```

Veremos que ambos tienen el mismo numero de inodo.

Ejemplo:

```
2359510 archivo.txt
2359510 copia.txt
```

Ambos nombres apuntan al mismo inodo.

### Caracteristicas

- Comparten el mismo inodo
- Comparten el mismo contenido
- Si se modifica uno, se modifica el otro
- El archivo solo se elimina cuando el contador de Links llega a 0
- No se pueden hacer hard links a directorios (para evitar ciclos)
- No funcionan entre distintos sistemas de archivos

---

## 2. Soft Link (Enlace Simbolico)

Un soft link es un archivo especial que apunta al nombre de otro archivo.

### Crear un soft link

```bash
ln -s archivo.txt acceso.txt
```

### Que sucede internamente

Si ejecutamos:

```bash
ls -l
```

Veremos algo como:

```
acceso.txt -> archivo.txt
```

El soft link tiene su propio inodo distinto al original.

Si ejecutamos:

```bash
ls -i archivo.txt acceso.txt
```

Veremos numeros de inodo diferentes.

### Caracteristicas

- Tiene un inodo propio
- Apunta al nombre del archivo original
- Puede apuntar a directorios
- Puede cruzar sistemas de archivos
- Si se elimina el archivo original, el enlace queda roto (broken link)

---

## Diferencia clave

| Caracteristica                   | Hard Link | Soft Link |
|----------------------------------|-----------|-----------|
| Comparte inodo                   | Si        | No        |
| Puede cruzar filesystem          | No        | Si        |
| Puede enlazar directorios        | No        | Si        |
| Se rompe si se borra el original | No        | Si        |

---

## Como pensarlo mentalmente

**Hard Link:**

```
nombre -> mismo inodo <- otro nombre
```

**Soft Link:**

```
nombre -> inodo propio -> apunta al nombre original -> inodo real
```

---

## Conclusion

Un hard link es simplemente otro nombre para el mismo archivo.

Un soft link es un acceso indirecto que referencia al archivo original por su nombre.

Comprender esta diferencia ayuda a entender mejor como Linux gestiona archivos, almacenamiento y referencias internas.


