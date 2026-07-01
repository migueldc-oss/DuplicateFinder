# DuplicateFinder
Duplicate files finder

# Manual de usuario — DuplicateFinder

> ![Captura de pantalla de la aplicación](capturas/main.png)
> *Vista principal de DuplicateFinder con la barra de búsqueda y la tabla de resultados.*

---

## Índice

1. [Introducción](#1-introducción)
2. [Requisitos del sistema](#2-requisitos-del-sistema)
3. [Interfaz principal](#3-interfaz-principal)
4. [Selección de carpetas](#4-selección-de-carpetas)
5. [Modos de detección](#5-modos-de-detección)
6. [Progreso del escaneo](#6-progreso-del-escaneo)
7. [Resultados](#7-resultados)
8. [Acciones sobre archivos](#8-acciones-sobre-archivos)
9. [Exportación de resultados](#9-exportación-de-resultados)
10. [Preferencias](#10-preferencias)
11. [Consejos y buenas prácticas](#11-consejos-y-buenas-prácticas)

---

## 1. Introducción

**DuplicateFinder** es una aplicación para macOS que busca y gestiona archivos duplicados en tu disco. Escanea una o varias carpetas, calcula la huella digital (hash SHA-256) de cada archivo y agrupa los que son idénticos, permitiéndote revisarlos, abrirlos, borrarlos o exportar un informe.

### Características principales

- Escaneo recursivo de una o varias carpetas simultáneamente.
- Dos modos de detección: **Fiable** (por contenido, SHA-256) y **Rápido** (por nombre + tamaño).
- Filtros por tamaño, extensiones y carpetas excluidas.
- Tabla ordenable y búsqueda en los resultados.
- Acciones individuales y por lotes: abrir, mostrar en Finder, mover a la Papelera o borrar permanentemente.
- Exportación a CSV y JSON con todas las ubicaciones de cada archivo duplicado.
- Interfaz localizada a 8 idiomas.

---

## 2. Requisitos del sistema

- **macOS** 14.0 (Sonora) o superior.
- **Apple Silicon** o **Intel**.
- No requiere ningún paquete o dependencia externa.

---

## 3. Interfaz principal

![Estructura de la interfaz](capturas/interfaz.png)

La ventana se divide en tres zonas:

| Zona | Descripción |
|------|-------------|
| **Barra superior (ScanView)** | Selección de carpetas, modo de detección y control de inicio/cancelación. |
| **Barra de estadísticas** | Métricas globales (archivos totales, duplicados, grupos, espacio recuperable) y botón de exportación. |
| **Tabla de resultados** | Listado de grupos de duplicados ordenable y con búsqueda. |

---

## 4. Selección de carpetas

![Selección de carpetas](capturas/seleccion-carpetas.png)

1. Pulsa el botón **«Elegir carpeta…»** (icono de carpeta).
2. Se abre el diálogo estándar de macOS. Puedes seleccionar **una o varias carpetas** manteniendo pulsada la tecla ⌘ (Command).
3. Las carpetas se van **acumulando** en la lista. Puedes añadir más carpetas en sucesivas selecciones.
4. Para limpiar la selección, pulsa el botón **«Limpiar»** (icono ✕) que aparece a la derecha.

> El botón **«Iniciar búsqueda»** permanece deshabilitado hasta que hayas seleccionado al menos una carpeta. También puedes arrastrar una carpeta desde el Finder directamente sobre la ventana.

---

## 5. Modos de detección

DuplicateFinder ofrece dos modos, seleccionables mediante un control segmentado en la barra superior:

| Modo | Icono | Descripción |
|------|-------|-------------|
| **Fiable** | — | Calcula el hash SHA-256 del **contenido completo** de cada archivo. Garantiza que no hay falsos positivos, pero es más lento porque lee todos los archivos. |
| **Nombre + Tamaño** | — | Compara únicamente el nombre (sin distinción de mayúsculas) y el tamaño en bytes. Es muy rápido (no lee contenido), pero puede generar falsos positivos si dos archivos distintos coinciden en nombre y tamaño. |

> El modo por defecto se configura en **Preferencias → Detección**.

---

## 6. Progreso del escaneo

Durante el escaneo, la barra superior muestra el estado actual:

| Fase | Indicador |
|------|-----------|
| **Escaneando…** | Contador de archivos procesados en la carpeta. |
| **Comparando…** | Barra de progreso con el número de hashes calculados sobre el total de candidatos. |
| **Calculando…** | Progreso del guardado en base de datos y cálculo de agregados. |
| **Completada** | Icono verde de verificación. |
| **Cancelada** | Icono naranja. |

Puedes cancelar la búsqueda en cualquier momento pulsando el botón **«Cancelar»**.

---

## 7. Resultados

![Tabla de resultados](capturas/resultados.png)

Una vez finalizada la búsqueda, aparece la tabla de resultados con las siguientes columnas:

| Columna | Descripción |
|---------|-------------|
| **Nombre** | Nombre del archivo con su icono. |
| **Tamaño** | Tamaño de cada copia. |
| **Copias** | Número de repeticiones del archivo. |
| **Tamaño × Copias** | Espacio total ocupado por todas las copias. |
| **Ubicación** | Ruta completa de cada copia, con botones de acción. |

Puedes **ordenar** la tabla pulsando en cualquier cabecera de columna. También puedes **buscar** archivos por nombre o ruta usando el campo de búsqueda en la parte inferior.

### Barra de estadísticas

En la parte superior de los resultados se muestran cuatro métricas:

- **Ficheros totales**: todos los archivos escaneados.
- **Duplicados**: archivos que pertenecen a algún grupo duplicado.
- **Grupos**: conjuntos de archivos idénticos.
- **Recuperable**: espacio que se liberaría si se eliminan todas las copias sobrantes (una copia por grupo se conserva).

---

## 8. Acciones sobre archivos

Cada archivo duplicado en la columna «Ubicación» tiene botones de acción:

| Botón | Acción | Atajo |
|-------|--------|-------|
| 👁 (Ojo) | Abrir el archivo con la aplicación predeterminada. | — |
| 📁 (Carpeta) | Mostrar el archivo en el Finder. | — |
| 🗑 (Papelera) | Mover a la Papelera (o borrar permanentemente según preferencias). | — |

### Borrado por lotes

Puedes seleccionar varios archivos marcando la casilla cuadrada junto a cada uno:

1. Marca los archivos que quieras eliminar pulsando en su casilla.
2. Aparecerá el botón **«Borrar seleccionados (N)»** en la barra de estadísticas.
3. Púlsalo para abrir la confirmación y completar el borrado.

> Puedes cambiar el comportamiento de borrado en **Preferencias → General**: marca o desmarca «Mover los ficheros borrados a la Papelera».

---

## 9. Exportación de resultados

Pulsa el botón **«Exportar»** (icono de compartir) en la barra de estadísticas y elige entre:

- **CSV** — Archivo de texto delimitado por comas, compatible con Excel, Numbers y hojas de cálculo.
- **JSON** — Formato estructurado, ideal para procesamiento programático.

Ambos formatos incluyen **todas las copias de cada archivo duplicado** (no solo una por grupo), con los campos: nombre, ruta, tamaño, número de repeticiones, espacio total ocupado y hash SHA-256.

Se abre un diálogo `NSSavePanel` para elegir la ubicación y el nombre del archivo exportado.

---

## 10. Preferencias

Pulsa `⌘,` (Comando + ,) para abrir las preferencias, organizadas en cuatro pestañas.

### General

| Opción | Descripción |
|--------|-------------|
| **Número de resultados (Top N)** | Número máximo de filas en la tabla de resultados (10–100.000). |
| **Mover a la Papelera** | Si está activo, los archivos se envían a la Papelera en lugar de borrarse permanentemente. |
| **Selección inteligente** | Estrategia para marcar automáticamente qué copia conservar (la más antigua, la más reciente, o la de ruta más corta). |
| **Apariencia** | Modo de visualización. |

### Detección

| Opción | Descripción |
|--------|-------------|
| **Método por defecto** | Modo de detección seleccionado al abrir la aplicación. |

### Filtros

| Opción | Descripción |
|--------|-------------|
| **Tamaño mínimo / máximo** | Rango de tamaño en bytes. Los archivos fuera de este rango se ignoran. |
| **Incluir ocultos** | Incluir archivos y carpetas ocultos (que empiezan por `.`). |
| **Seguir enlaces simbólicos** | Si está activo, los enlaces simbólicos se siguen durante el escaneo. |
| **Extensiones permitidas** | Lista separada por comas (ej. `jpg, png, mp4`). Vacío = todas las extensiones. |
| **Carpetas excluidas** | Lista separada por comas de nombres de carpeta que se saltan durante el escaneo (ej. `node_modules, .git`). |

### Idioma

Permite cambiar el idioma de la interfaz entre los 8 disponibles. Puede ser necesario reiniciar la aplicación para aplicar el cambio por completo.

---

## 11. Consejos y buenas prácticas

1. **Empieza con el modo Rápido** si tienes muchas carpetas. Es mucho más veloz y puede ser suficiente para encontrar la mayoría de duplicados.
2. **Usa el modo Fiable para decisiones definitivas**. Antes de borrar, especialmente si los nombres no coinciden, utiliza el modo Fiable para evitar falsos positivos.
3. **Selecciona carpetas específicas**, no todo el disco. Escanear solo las carpetas que más te interesen (Descargas, Documentos, Escritorio) reduce drásticamente el tiempo y el ruido en los resultados.
4. **Revisa las ubicaciones** en la columna «Ubicación» antes de borrar. A veces un archivo duplicado está en una carpeta del sistema y es mejor conservarlo.
5. **Exporta un CSV** antes de hacer limpieza para tener un registro de los archivos eliminados.
6. **Configura los filtros** si buscas tipos de archivo concretos (ej. solo imágenes `.jpg` y `.png`).
7. **Usa el botón «Limpiar»** para empezar de cero con una nueva selección de carpetas sin cerrar la aplicación.

---

> **DuplicateFinder** — https://github.com/migueldc-oss/DuplicateFinder
>
> Documentación generada el 1 de julio de 2026.
