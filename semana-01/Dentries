# Dentries en Linux (Directory Entries)

## ¿Qué es una dentry?

Dentry significa "Directory Entry" (Entrada de Directorio).

Es una estructura que relaciona un nombre de archivo con su inodo.

En otras palabras:

nombre → inodo

---

## Diferencia entre Inodo y Dentry

| Concepto | Función |
|----------|---------|
| Inodo | Contiene la metadata del archivo y la ubicación de los datos |
| Dentry | Relaciona un nombre con un inodo |

El inodo representa la identidad real del archivo.

La dentry es la referencia que conecta el nombre con ese inodo.

---

## Cómo funciona internamente

Cuando el sistema accede a un archivo:

1. Busca el nombre en el directorio.
2. Encuentra la dentry correspondiente.
3. La dentry apunta al número de inodo.
4. El kernel accede al inodo.
5. El inodo apunta a los bloques de datos.
6. Se leen los datos del disco.

Flujo completo:

Directorio → Dentry → Inodo → Bloques

---

## Dentry Cache (dcache)

Linux mantiene dentries en memoria RAM para acelerar el acceso a archivos.

Esto evita búsquedas repetidas en el disco y mejora el rendimiento del sistema.

Si un archivo se accede frecuentemente, su dentry puede permanecer en cache.

---

## Relación con Hard Links

Cuando existen múltiples hard links:

archivo.txt → inodo 2359510  
copia.txt   → inodo 2359510  

Existen múltiples dentries apuntando al mismo inodo.

Esto explica por qué el contador de Links del inodo aumenta.

---

## Conclusión

La dentry es el puente entre el nombre del archivo y su identidad real (inodo).

Comprender dentries ayuda a entender:

- Cómo Linux resuelve rutas
- Cómo funciona el cache del sistema de archivos
- Por qué los hard links comparten inodo
