---
Práctica: B1.9
Bloque: 01_Entorno
Nivel: 2
Nivel_nombre: Intermedio
RA: RA1, RA3
CE: 1.c, 3.b
Playlist: B1_Entorno
Vídeo: B1.9 · Laboratorio de virtualización (VirtualBox / Hyper-V)
---

## B1.9 — Montar el laboratorio de virtualización

> [!abstract] Ficha de la práctica
> ### 📌 `B1.9` — Laboratorio de virtualización (VirtualBox / Hyper-V)
> - **Bloque 1** (Preparar el entorno) · **Nivel 2** (Intermedio) · **RA1, RA3** · **CE 1.c, 3.b**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.9 · Laboratorio de virtualización (VirtualBox / Hyper-V)`

> [!info] Caso real (contexto profesional)
> Antes de tocar servidores reales, un técnico monta un **laboratorio virtual** donde probar sin riesgo: instala un **hipervisor** en su equipo y crea máquinas virtuales que puede romper y rehacer a voluntad. Este laboratorio es la base sobre la que harás **todo el proyecto Boochan** de las próximas unidades.

- **🎯 Objetivo real:** dejar montado un hipervisor (VirtualBox / Hyper-V) con virtualización activa, entendiendo los tipos de red y los snapshots.
- **🧩 Problema que resuelve:** poder practicar instalaciones y servidores sin arriesgar el equipo físico ni la red del centro.

---

## 📚 Fundamento

> [!info] Antes de empezar: hipervisor de Tipo 1 y Tipo 2
> Un **hipervisor** crea "ordenadores dentro del ordenador". Hay dos tipos: **Tipo 1** (se instala directo sobre el hardware, como Hyper-V o los de la nube) y **Tipo 2** (se instala como un programa más sobre tu SO, como VirtualBox). Tu equipo (**host**) reparte CPU, RAM y disco entre el SO anfitrión y las máquinas virtuales (**guests**).

> [!warning] Requisito imprescindible: virtualización por hardware
> El hipervisor necesita **VT-x (Intel) / AMD-V** activado en la **BIOS/UEFI**. En equipos de aula gestionados puede estar bloqueado: si la VM no arranca, es lo primero a revisar con el profesor.

> [!example] Vocabulario de esta práctica
> - **Hipervisor:** software que crea y ejecuta máquinas virtuales.
> - **Host / Guest:** anfitrión (tu equipo) / invitado (la VM).
> - **Tipos de red VirtualBox:** **NAT** (salida a Internet), **Solo-Anfitrión/Host-Only** (red privada host↔VM), **Puente** (la VM como un equipo más de la red), **Interna** (VM↔VM aisladas).
> - **Snapshot:** foto del estado de una VM para volver atrás si algo se rompe.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-9-laboratorio-de-virtualizacion-virtualbox-hype.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura de la Fase 0.1 y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.9 · Laboratorio de virtualización (VirtualBox / Hyper-V)`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `Enlace al vídeo explicativo`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate.

> [!example] Paso 1 — Comprueba/instala el hipervisor
> Verifica que **VirtualBox** está instalado (o **Hyper-V** activado en Windows). Si falta y no tienes permisos, avisa al profesor — **no** instales versiones no autorizadas.

> [!example] Paso 2 — Confirma la virtualización por hardware
> Comprueba en el Administrador de tareas (Windows → Rendimiento → CPU → "Virtualización: Habilitada") o en la BIOS/UEFI que **VT-x/AMD-V** está activo.

> [!example] Paso 3 — Crea una VM de prueba
> Crea una máquina virtual vacía dimensionada con criterio (RAM/CPU/disco realistas para un portátil de aula). Aún **sin instalar** SO (eso es B1.10).

> [!example] Paso 4 — Explora los tipos de red
> En la configuración de red de la VM, identifica y explica **NAT**, **Solo-Anfitrión**, **Puente** e **Interna**. Configura una tarjeta **NAT** (Internet) y otra **Solo-Anfitrión** (red privada) — la base de Boochan.

> [!example] Paso 5 — Haz un snapshot
> Crea un **snapshot** de la VM. Cambia algo, y **restaura** el snapshot para comprobar que vuelve al estado anterior.

> [!example] Paso 6 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.9 · Laboratorio de virtualización (VirtualBox / Hyper-V)`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | VT-x/AMD-V desactivado | La VM no arranca / va lentísima | Actívalo en BIOS/UEFI (con el profesor si está bloqueado). |
> | Asignar demasiada RAM a la VM | El host se queda sin recursos | Dimensiona dejando margen al host. |
> | Confundir NAT con Puente | La red no se comporta como esperas | NAT = salida a Internet; Puente = la VM en la red real. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Tienes una **VM creada** con virtualización por hardware activa.
> - Sabes explicar **NAT, Host-Only, Puente e Interna**.
> - Has hecho y **restaurado** un snapshot.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué diferencia hay entre un hipervisor de **Tipo 1** y de **Tipo 2**?
> 2. ¿Para qué sirve la red **Solo-Anfitrión**? ¿Y la **NAT**?
> 3. ¿Qué es un **snapshot** y cuándo lo usarías?

---

## ✅ Entregables y cierre

- **Entregable:** VM de laboratorio creada, con dos tarjetas de red y un snapshot (evidenciado en el vídeo).
- **Entregable vídeo:** `B1.9 · Laboratorio de virtualización (VirtualBox / Hyper-V)` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** hipervisor operativo + VM con redes NAT/Host-Only + snapshot funcional.
- **Entregable apuntes:** `b1-9-laboratorio-de-virtualizacion-virtualbox-hype.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - Qué es un **hipervisor** (Tipo 1 vs Tipo 2) y el papel de **VT-x/AMD-V**.
> - Los **tipos de red** de VirtualBox y para qué sirve cada uno.
> - A usar **snapshots** para practicar sin miedo. Este laboratorio es la base de **Boochan**.
>
> **Siguiente:** B1.9b — Verificar tu red con APIs públicas: comprobarás **desde fuera** que el NAT que acabas de configurar hace lo que crees.
