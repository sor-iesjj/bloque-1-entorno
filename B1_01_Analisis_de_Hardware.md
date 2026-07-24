---
Práctica: B1.1
Bloque: 01_Entorno
Nivel: 1
Nivel_nombre: Básico
Título: Análisis del hardware de un equipo con CPU-Z
RA: RA1
CE: 1.a, 1.b
Playlist: B1_Entorno
Vídeo: B1.1 · Análisis de hardware con CPU-Z
---

## B1.1 — Análisis del hardware de un equipo con CPU-Z

> [!abstract] Ficha de la práctica
> ### 📌 `B1.1` — Análisis de hardware con CPU-Z
> - **Bloque 1** (Preparar el entorno) · **Nivel 1** (Básico) · **RA1** · **CE 1.a, 1.b**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.1 · Análisis de hardware con CPU-Z`

> [!info] Caso real (contexto profesional)
> Llega al taller un lote de ordenadores que hay que reinstalar. Antes de decidir **qué sistema operativo** admite cada uno o **qué ampliaciones** necesita, el técnico tiene que saber **exactamente qué lleva dentro**: procesador, memoria, placa base. Abrir la caja no basta — hay que leer los datos reales del sistema y **dejarlos documentados**.

- **🎯 Objetivo real:** inventariar el hardware de un equipo (CPU, RAM, placa base) para documentarlo y decidir SO y ampliaciones.
- **🧩 Problema que resuelve:** sin conocer el hardware real, no se puede comprobar si un SO cumple requisitos ni planificar una mejora. Se trabaja a ciegas.

---

## 📚 Fundamento

> [!info] Antes de empezar: ¿por qué inventariar el hardware?
> Cada equipo tiene un hardware concreto que **condiciona** qué sistema operativo puede ejecutar y con qué soltura. El procesador (núcleos, arquitectura), la memoria (tipo y cantidad) y la placa base (chipset, tipo de arranque BIOS/UEFI) determinan si un equipo sirve para Windows Server, para Ubuntu Server o solo para tareas ligeras. Documentar esto es el **primer paso** de cualquier despliegue o mantenimiento profesional.

> [!tip] Idea clave
> **No te fíes de la etiqueta ni de la memoria.** Un equipo "de 8 GB" puede tener 4+4 en doble canal o un solo módulo de 8 (peor rendimiento). Solo una herramienta de diagnóstico te da el dato **real** y verificable.

> [!example] Vocabulario de esta práctica
> - **CPU-Z:** programa gratuito y portable (no requiere instalación) que muestra los datos reales del hardware. Web oficial: `cpuid.com`.
> - **Núcleos / hilos:** unidades de proceso del CPU (p. ej. 8 núcleos / 16 hilos).
> - **Socket:** el zócalo de la placa donde encaja el procesador (define qué CPUs admite).
> - **Canal de memoria (Single/Dual):** cómo están repartidos los módulos de RAM; el doble canal rinde más.
> - **BIOS/UEFI:** el firmware de arranque de la placa (importante para instalar el SO).
> - **OBS · Playlist · Timestamp:** grabación de pantalla · lista de YouTube de este bloque (`B1_Entorno`) · marca de tiempo por paso en la descripción.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> Esta práctica se **graba entera con OBS**, de principio a fin. No es un repaso al final: quiero ver **cómo lo haces tú**.
> 1. **Prepárate primero** (Paso 0): léete el ejercicio entero y ten a mano OBS y tu identificación.
> 2. **Arranca OBS y, nada más empezar, PRESÉNTATE:** *"Hola, me llamo [Nombre], soy alumno de 2.º SMR, y en este vídeo voy a hacer la práctica B1.1 — Análisis de hardware con CPU-Z."* Y **muestra en pantalla algo que demuestre que eres tú** (tu **Teams** o tu correo `@alu.edu.gva.es`). Di **qué vas a hacer**.
> 3. **Graba todos los pasos** sin cortes, hablando lo que haces.
> 4. **Timestamps SIEMPRE** en la descripción del vídeo: `00:00 Presentación` y **uno por cada paso** (`mm:ss`).
> 5. **Al terminar:** nombra el vídeo **`B1.1 · Análisis de hardware con CPU-Z`** y súbelo a tu playlist de YouTube **`B1_Entorno`** (como **"No listado"**).
> 6. **Una sola entrega** (no se duplica casa/centro).

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> 1. **Léete el ejercicio entero** antes de tocar nada.
> 2. **Ten a mano OBS** y una pestaña con tu **Teams** o tu correo `@alu.edu.gva.es` (para presentarte).
> 3. **Arranca OBS** y pulsa **"Iniciar grabación"**. A partir de aquí, **todo queda grabado**.
> 4. **Preséntate** (mira la caja de grabación de arriba): di tu nombre, muestra tu identidad y di qué vas a hacer.

> [!example] Paso 1 — Descarga CPU-Z (versión portable)
> En el navegador, entra en la web oficial `https://www.cpuid.com/softwares/cpu-z.html` y descarga la **versión ZIP portable** (no necesita instalación). Descomprímela y ejecuta el `.exe` correspondiente a tu Windows (64 bits).

> [!example] Paso 2 — Lee la pestaña **CPU**
> Anota: **nombre y fabricante** del procesador, **nombre en clave** (arquitectura), **socket**, **número de núcleos e hilos** y las **cachés (L1/L2/L3)**.

> [!example] Paso 3 — Lee la pestaña **Mainboard** (placa base)
> Anota: **fabricante y modelo** de la placa, **chipset** y la **versión y tipo de BIOS/UEFI** (importante para saber cómo arrancará la instalación del SO).

> [!example] Paso 4 — Lee la pestaña **Memory** (memoria)
> Anota: **tipo** de memoria (DDR4/DDR5), **tamaño total**, **canal** (Single/Dual) y la **frecuencia** efectiva.

> [!example] Paso 5 — Documenta el inventario
> Vuelca los datos en una **tabla de inventario** (en tu bóveda o en un documento). Ejemplo mínimo:
> | Componente | Dato real (según CPU-Z) |
> | :--- | :--- |
> | Procesador | … núcleos / … hilos, socket … |
> | Placa base | modelo …, chipset …, UEFI/BIOS … |
> | Memoria | … GB DDR…, canal …, … MHz |

> [!example] Paso 6 — Cierra la grabación y súbela
> 1. **Detén la grabación** en OBS y localiza el archivo del vídeo.
> 2. **Súbelo a YouTube**, a tu playlist **`B1_Entorno`**, como **"No listado"**.
> 3. Nombra el vídeo **`B1.1 · Análisis de hardware con CPU-Z`**.
> 4. En la **descripción**, añade los **timestamps** (uno por paso).

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Descargar CPU-Z de una web no oficial | Riesgo de malware/adware | Descárgalo **solo** desde `cpuid.com`. |
> | Confundir núcleos con hilos | Datos de inventario incorrectos | En CPU-Z, campo **Cores** = núcleos, **Threads** = hilos. |
> | Anotar "8 GB" sin mirar el canal | Pierdes info de rendimiento | Mira **Channel** en la pestaña Memory (Single/Dual). |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Tienes una **tabla de inventario** con CPU, placa base y memoria, con datos reales de CPU-Z.
> - Sabes decir si el equipo arranca en **UEFI** o **BIOS**.
> - El vídeo está subido a la playlist `B1_Entorno` con presentación y timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué diferencia hay entre **núcleos** e **hilos**?
> 2. ¿Por qué importa saber si la RAM está en **canal simple o doble**?
> 3. ¿Para qué sirve conocer si la placa arranca en **UEFI o BIOS** antes de instalar un SO?

---

## ✅ Entregables y cierre

- **Entregable vídeo:** `B1.1 · Análisis de hardware con CPU-Z` subido a la playlist `B1_Entorno` (No listado), con presentación al principio y timestamps. **Una sola entrega**.
- **Entregable documento:** la **tabla de inventario** del equipo analizado.
- **Criterio de éxito:** inventario completo y correcto (CPU, placa, memoria) + vídeo subido a su playlist.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A **inventariar el hardware real** de un equipo con **CPU-Z**.
> - A leer y **documentar** procesador, placa base y memoria.
> - Por qué el hardware condiciona **qué SO** puede instalarse y cómo arranca (UEFI/BIOS).
>
> **Siguiente:** B1.2 — Presupuesto profesional de un servidor.
