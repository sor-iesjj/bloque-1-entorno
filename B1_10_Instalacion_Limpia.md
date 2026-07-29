---
Práctica: B1.10
Bloque: 01_Entorno
Nivel: 2
Nivel_nombre: Intermedio
RA: RA1
CE: 1.a, 1.b, 1.c, 1.d
Playlist: B1_Entorno
Vídeo: B1.10 · Instalación limpia de un SO
---

## B1.10 — Instalación limpia de un sistema operativo

> [!abstract] Ficha de la práctica
> ### 📌 `B1.10` — Instalación limpia de un SO
> - **Bloque 1** (Preparar el entorno) · **Nivel 2** (Intermedio) · **RA1** · **CE 1.a, 1.b, 1.c, 1.d**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.10 · Instalación limpia de un SO`

> [!info] Caso real (contexto profesional)
> Con la ISO verificada (B1.4), el medio de arranque listo (B1.5/B1.7), el disco preparado (B1.8) y el laboratorio montado (B1.9), toca lo esencial: **instalar el sistema operativo desde cero**. Aquí se juntan todos los pasos anteriores en una instalación limpia y bien hecha.

- **🎯 Objetivo real:** instalar un SO servidor desde cero, tomando las decisiones correctas (particionado, red, usuarios) y dejándolo listo para el primer arranque.
- **🧩 Problema que resuelve:** una instalación es la base de todo; hacerla mal (mal particionado, sin red, usuarios flojos) arrastra problemas después.

---

## 📚 Fundamento

> [!info] Antes de empezar: qué se decide durante la instalación
> Una instalación no es "siguiente, siguiente". Se decide: **idioma/teclado**, **particionado** del disco (usar todo o manual con partición EFI + raíz), **configuración de red** (IP fija o DHCP), **usuario administrador** y contraseña, y **paquetes iniciales** (p. ej. servidor SSH). Cada decisión tiene consecuencias.

> [!tip] Idea clave
> **Una instalación limpia es la que parte de cero**, sin restos de un sistema anterior. Por eso preparamos el disco antes (B1.8): para que el instalador encuentre un lienzo limpio.

> [!example] Vocabulario de esta práctica
> - **Instalación limpia:** instalar desde cero, sin migrar de un sistema previo.
> - **IP estática vs DHCP:** dirección fija (típica en servidores) vs asignada automáticamente.
> - **Primer arranque:** primer inicio del SO ya instalado, sin el USB.
> - **OpenSSH:** servicio para administrar el servidor por terminal remota.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-10-instalacion-limpia-de-un-so.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura de la Fase 0.1 y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.10 · Instalación limpia de un SO`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `Enlace al vídeo explicativo`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate. Instala sobre la **VM del laboratorio** (B1.9), arrancando desde el medio con la ISO verificada.

> [!example] Paso 1 — Arranca el instalador
> Arranca la VM desde el USB/ISO. Elige **idioma y teclado**.

> [!example] Paso 2 — Configura el particionado
> Elige el disco y define el particionado (usar todo el disco, o manual con **EFI + raíz**). Confirma que instala sobre el disco correcto.

> [!example] Paso 3 — Configura la red
> Asigna la red del servidor: **IP estática** (recomendado en servidor) o DHCP. Anota la IP.

> [!example] Paso 4 — Crea el usuario administrador
> Define nombre de equipo, **usuario** administrador y **contraseña robusta**. Si el instalador lo ofrece, marca instalar **OpenSSH** para administración remota.

> [!example] Paso 5 — Finaliza y primer arranque
> Deja terminar la instalación, **retira el medio** de instalación y arranca el SO ya instalado. Inicia sesión y comprueba que responde.

> [!example] Paso 6 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.10 · Instalación limpia de un SO`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | No retirar el medio tras instalar | Vuelve a arrancar el instalador | Quita el USB/ISO antes del primer arranque. |
> | Contraseña débil de administrador | Servidor inseguro | Usa una contraseña robusta. |
> | Instalar sobre el disco equivocado | Pérdida de datos | Verifica el disco destino en el paso de particionado. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - El SO **arranca desde el disco** (sin el USB) e inicias sesión.
> - Tiene la **red** configurada (IP conocida) y usuario administrador.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué significa **instalación limpia**?
> 2. ¿Por qué un servidor suele llevar **IP estática**?
> 3. ¿Por qué hay que **retirar el medio** antes del primer arranque?

---

## ✅ Entregables y cierre

- **Entregable:** SO instalado y funcionando en la VM (evidenciado en el vídeo, con el primer arranque).
- **Entregable vídeo:** `B1.10 · Instalación limpia de un SO` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** SO que arranca del disco, con red y usuario administrador configurados.
- **Entregable apuntes:** `b1-10-instalacion-limpia-de-un-so.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A hacer una **instalación limpia** tomando las decisiones clave.
> - A configurar **particionado, red y usuario** durante la instalación.
> - A dejar un servidor listo para el **primer arranque** — la base de Boochan.
>
> **Siguiente:** B1.11 — Instalación por red con iVentoy.
