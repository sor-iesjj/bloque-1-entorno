---
Práctica: B1.7
Bloque: 01_Entorno
Nivel: 2
Nivel_nombre: Intermedio
RA: RA.01
CE: CE.01.b
Playlist: B1_Entorno
Vídeo: B1.7 · Kit multiboot con Ventoy
---

## B1.7 — Creación de un kit técnico actualizable con Ventoy

> [!abstract] Ficha de la práctica
> ### 📌 `B1.7` — Kit multiboot con Ventoy
> - **Bloque 1** (Preparar el entorno) · **Nivel 2** (Intermedio) · **RA.01** · **CE.01.b**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.7 · Kit multiboot con Ventoy`

> [!info] Caso real (contexto profesional)
> Un servicio técnico necesita un **único pendrive** con varios sistemas operativos y utilidades (Ubuntu, Windows, GParted…) y poder **mantenerlo actualizado** sin tener que reformatearlo cada vez. **Ventoy** resuelve esto: instalas Ventoy una vez y luego solo **copias o borras las ISOs** en el USB.

- **🎯 Objetivo real:** montar y mantener un USB multiboot con Ventoy, la herramienta estándar hoy para kits técnicos.
- **🧩 Problema que resuelve:** llevar muchas ISOs en un solo soporte y actualizarlas sin rehacer el USB.

---

## 📚 Fundamento

> [!info] Antes de empezar: por qué Ventoy y no las herramientas antiguas
> Las herramientas multiboot clásicas (YUMI, MultiBootUSB) obligaban a "instalar" cada ISO con un proceso tedioso. **Ventoy** cambió el paradigma: instala un gestor de arranque en el USB **una sola vez**, y a partir de ahí **arrastras las ISOs en crudo** a la unidad. Al arrancar, Ventoy muestra un **menú** con todas las ISOs disponibles.

> [!tip] Idea clave
> Con Ventoy, **añadir, quitar o actualizar** un sistema es tan simple como copiar o borrar un archivo. El USB sigue siendo un USB normal donde también puedes guardar datos.

> [!example] Vocabulario de esta práctica
> - **Ventoy:** gestor multiboot persistente (`ventoy.net`).
> - **Persistente:** el gestor queda instalado; no se reformatea al añadir ISOs.
> - **Menú de arranque:** lista de ISOs que Ventoy muestra al arrancar.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-7-kit-multiboot-con-ventoy.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura del **Bloque 0 · Fase 0.1.b** y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.7 · Kit multiboot con Ventoy`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `Enlace al vídeo explicativo`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate. Ten un USB de **al menos 64 GB** y varias ISOs verificadas (Ubuntu, Windows, GParted).

> [!example] Paso 1 — Instala Ventoy en el USB
> Descarga **Ventoy** de `https://www.ventoy.net`, ejecútalo, selecciona tu USB y pulsa **Install**. ⚠️ **Se formatea el USB** (solo esta vez).

> [!example] Paso 2 — Copia las ISOs
> Copia las **ISOs en crudo** a la raíz del USB (arrastrar y soltar). No hay que "instalarlas": Ventoy las detecta solas.

> [!example] Paso 3 — Arranca desde el USB
> Arranca un equipo/VM desde el USB. Aparece el **menú de Ventoy** con todas las ISOs. Selecciona una y comprueba que arranca.

> [!example] Paso 4 — Actualiza el kit sin reformatear
> **Sustituye** una ISO por una versión más nueva (borra la vieja, copia la nueva). Vuelve a arrancar y comprueba que el menú se actualiza **sin reinstalar** Ventoy.

> [!example] Paso 5 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.7 · Kit multiboot con Ventoy`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Reinstalar Ventoy cada vez que añades una ISO | Borras el USB sin necesidad | Ventoy se instala **una vez**; luego solo copias ISOs. |
> | Copiar ISOs no verificadas | Riesgo de imagen corrupta | Usa ISOs verificadas (B1.4). |
> | USB demasiado pequeño | No caben las ISOs | Usa **64 GB o más**. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - El menú de Ventoy muestra **varias ISOs** y arrancan.
> - Has **actualizado** una ISO sin reformatear el USB.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué ventaja tiene Ventoy frente a instalar cada ISO una por una?
> 2. ¿Cuántas veces hay que **formatear** el USB con Ventoy?
> 3. ¿Cómo se **actualiza** un sistema del kit?

---

## ✅ Entregables y cierre

- **Entregable:** USB multiboot con Ventoy y varias ISOs (evidenciado en el vídeo).
- **Entregable vídeo:** `B1.7 · Kit multiboot con Ventoy` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** kit funcional + demostrada la actualización sin reformatear.
- **Entregable apuntes:** `b1-7-kit-multiboot-con-ventoy.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A montar un **USB multiboot** con Ventoy.
> - A **mantenerlo actualizado** copiando/borrando ISOs.
> - Por qué Ventoy es hoy el **estándar** para kits técnicos.
>
> **Siguiente:** B1.8 — Particiones MBR/GPT con GParted.
