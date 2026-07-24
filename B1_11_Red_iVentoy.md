---
Práctica: B1.11
Bloque: 01_Entorno
Nivel: 3
Nivel_nombre: Avanzado
RA: RA1, RA2, RA5
CE: 1.a, 1.d, 2.a, 2.c, 5.a
Playlist: B1_Entorno
Vídeo: B1.11 · Instalación por red con iVentoy
---

## B1.11 — Instalación por red con iVentoy

> [!abstract] Ficha de la práctica
> ### 📌 `B1.11` — Instalación por red con iVentoy
> - **Bloque 1** (Preparar el entorno) · **Nivel 3** (Avanzado) · **RA1, RA2, RA5** · **CE 1.a, 1.d, 2.a, 2.c, 5.a**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.11 · Instalación por red con iVentoy`

> [!info] Caso real (contexto profesional)
> En un aula sin red fija (o para desplegar rápido en varios equipos a la vez), el técnico necesita **instalar por red** sin ir con un USB equipo por equipo. Con **iVentoy** convierte su portátil en un **servidor PXE portátil** que distribuye las ISOs a los clientes conectados por switch.

- **🎯 Objetivo real:** montar un entorno PXE moderno con iVentoy e instalar sistemas por red sin USB.
- **🧩 Problema que resuelve:** desplegar en varios equipos simultáneamente, ahorrando tiempo frente al USB uno a uno.

---

## 📚 Fundamento

> [!info] Antes de empezar: qué es el arranque por red (PXE)
> **PXE** permite que un equipo **arranque desde la red** en vez de desde su disco o un USB. Para ello necesita que alguien le dé una IP (**DHCP**) y le sirva los archivos de arranque (**TFTP/HTTP**). Montar todo esto a mano es laborioso; **iVentoy** lo integra en una sola aplicación: es el "Ventoy pero por red".

> [!tip] Idea clave
> iVentoy hace por **red** lo que Ventoy hace por **USB**: pones tus ISOs en el servidor y los clientes eligen del menú al arrancar por red. Mucho más simple que montar DHCP+TFTP+HTTP por separado.

> [!warning] Hazlo en red aislada
> Un servidor DHCP/PXE **interfiere con la red del centro**. Monta esta práctica en una **red aislada** (switch propio o red interna/host-only de VirtualBox con varias VMs), **nunca** enchufado a la red del instituto.

> [!example] Vocabulario de esta práctica
> - **iVentoy:** servidor PXE "todo en uno" (`iventoy.com`).
> - **PXE:** arranque de un equipo desde la red.
> - **DHCP / TFTP / HTTP:** dar IP / servir arranque / servir la imagen.
> - **Cliente PXE:** equipo configurado para arrancar por red.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.11 · Instalación por red con iVentoy`** y súbelo a **`B1_Entorno`** (No listado).
> 5. **Una sola entrega.**

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate. Prepara una **red aislada**: un servidor (tu portátil o una VM) y uno o varios **clientes** en la misma red interna/host-only.

> [!example] Paso 1 — Instala iVentoy y añade las ISOs
> Descarga **iVentoy** de `https://www.iventoy.com`, ejecútalo y **coloca tus ISOs** verificadas (Ubuntu Server, Windows 10…) en su carpeta de imágenes.

> [!example] Paso 2 — Conecta el servidor y los clientes
> Conecta el servidor y los clientes al **mismo switch** (o a la misma red interna de VirtualBox). Asegúrate de que no hay otro DHCP compitiendo.

> [!example] Paso 3 — Inicia iVentoy y detecta equipos
> Arranca el servicio de iVentoy. Debe quedar a la escucha, listo para servir el menú por red.

> [!example] Paso 4 — Arranca los clientes por PXE
> En cada cliente, configura el arranque por **red (PXE)** en la BIOS/UEFI. Al arrancar, aparece el **menú de iVentoy**: selecciona la ISO e instala.

> [!example] Paso 5 — Supervisa la instalación
> Comprueba en el panel de iVentoy los clientes conectados y que la instalación avanza.

> [!example] Paso 6 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.11 · Instalación por red con iVentoy`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Conectarlo a la red del centro | Interfieres con el DHCP del instituto | Usa **red aislada** (switch propio o red interna VirtualBox). |
> | El cliente no arranca por red | No está activado PXE | Activa **arranque por red (PXE)** en la BIOS/UEFI del cliente. |
> | Dos DHCP en la misma red | Conflicto de IPs | Que solo iVentoy dé IPs en esa red aislada. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Un cliente **arranca por red** y muestra el menú de iVentoy.
> - Se completa (o inicia) una **instalación por red**.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué es **PXE** y qué servicios necesita (DHCP, TFTP/HTTP)?
> 2. ¿Por qué hay que montarlo en una **red aislada**?
> 3. ¿Qué hace iVentoy por red que Ventoy hace por USB?

---

## ✅ Entregables y cierre

- **Entregable:** cliente instalado (o iniciado) por red vía iVentoy (evidenciado en el vídeo).
- **Entregable vídeo:** `B1.11 · Instalación por red con iVentoy` en `B1_Entorno`. **Una sola entrega.**
- **Criterio de éxito:** arranque PXE del cliente + instalación por red desde el menú de iVentoy.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - Qué es el **arranque por red (PXE)** y qué servicios intervienen.
> - A montar un **servidor PXE moderno** con iVentoy en red aislada.
> - A **desplegar SO por red** sin USB.
>
> **Siguiente:** B1.12 — Instalación desatendida (opcional).
