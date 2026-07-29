---
Práctica: B1.6
Bloque: 01_Entorno
Nivel: 2
Nivel_nombre: Intermedio
RA: RA1, RA5
CE: 1.a, 1.b, 1.d, 5.a
Playlist: B1_Entorno
Vídeo: B1.6 · Comparativa Rufus vs Balena Etcher
---

## B1.6 — Comparativa entre Rufus y Balena Etcher

> [!abstract] Ficha de la práctica
> ### 📌 `B1.6` — Rufus vs Balena Etcher
> - **Bloque 1** (Preparar el entorno) · **Nivel 2** (Intermedio) · **RA1, RA5** · **CE 1.a, 1.b, 1.d, 5.a**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.6 · Comparativa Rufus vs Balena Etcher`

> [!info] Caso real (contexto profesional)
> Una administración local debe reinstalar ordenadores **antiguos (BIOS)** y **modernos (UEFI)**. El técnico decide comparar dos herramientas populares para crear USB de instalación, **Rufus** y **Balena Etcher**, para determinar cuál resulta más fiable y eficiente en un entorno mixto, y **dejarlo documentado**.

- **🎯 Objetivo real:** crear medios USB con dos herramientas, evaluar diferencias y elaborar documentación técnica comparativa.
- **🧩 Problema que resuelve:** elegir con criterio la herramienta adecuada según el contexto, en vez de "la de siempre".

---

## 📚 Fundamento

> [!info] Antes de empezar: dos filosofías distintas
> - **Rufus** (Windows): muy configurable — permite elegir esquema de partición (MBR/GPT), sistema de archivos y opciones avanzadas. Ideal cuando necesitas control.
> - **Balena Etcher** (multiplataforma): minimalista — "selecciona ISO, selecciona USB, flash". Menos opciones, pero muy simple y difícil de equivocarse.

> [!tip] Idea clave
> **No hay una "mejor" absoluta: hay mejor *para un contexto*.** Para entornos mixtos BIOS/UEFI donde necesitas controlar el esquema de partición, Rufus gana. Para grabar rápido y sin complicaciones, Etcher. Documentar el porqué es parte del trabajo profesional.

> [!example] Vocabulario de esta práctica
> - **Balena Etcher:** grabador de imágenes USB multiplataforma (`etcher.balena.io`).
> - **Flash:** escribir la imagen en el USB.
> - **Documentación comparativa:** informe con criterios, evidencias y conclusión.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-6-comparativa-rufus-vs-balena-etcher.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura de la Fase 0.1 y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.6 · Comparativa Rufus vs Balena Etcher`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `Enlace al vídeo explicativo`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate. Ten **dos USB de 16 GB**, una ISO verificada y equipos/VM de prueba con BIOS y UEFI.

> [!example] Paso 1 — Crea un USB con Rufus
> Graba la ISO con **Rufus** (como en B1.5). **Registra** el tiempo de escritura y los mensajes de verificación.

> [!example] Paso 2 — Crea un USB con Balena Etcher
> Descarga **Balena Etcher** de `https://etcher.balena.io/`, graba la **misma ISO** en el segundo USB. Registra tiempo y mensajes.

> [!example] Paso 3 — Prueba ambos en BIOS y UEFI
> Arranca cada USB en un equipo/VM **BIOS** y en uno **UEFI**. Anota si arrancan correctamente en cada modo.

> [!example] Paso 4 — Elabora la tabla comparativa
> | Criterio | Rufus | Balena Etcher |
> | :--- | :--- | :--- |
> | Control de partición (MBR/GPT) | … | … |
> | Facilidad de uso | … | … |
> | Tiempo de escritura | … | … |
> | Arranque BIOS / UEFI | … | … |
> | Conclusión (¿cuándo usar cada uno?) | … | … |

> [!example] Paso 5 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.6 · Comparativa Rufus vs Balena Etcher`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Comparar con ISOs distintas | La comparación no es justa | Usa **la misma ISO** en ambas herramientas. |
> | Conclusión sin evidencias | Informe poco profesional | Apoya cada afirmación en un dato (tiempo, arranque). |
> | Probar solo en UEFI | Comparación incompleta | Prueba **BIOS y UEFI**. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Tienes **dos USB** creados con herramientas distintas y probados en BIOS/UEFI.
> - Tu tabla comparativa tiene **conclusión justificada**.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿En qué situación es **mejor Rufus** y en cuál **Etcher**?
> 2. ¿Por qué hay que usar la **misma ISO** para comparar?
> 3. ¿Qué evidencias respaldan tu conclusión?

---

## ✅ Entregables y cierre

- **Entregable documento:** informe comparativo con tabla y conclusión.
- **Entregable vídeo:** `B1.6 · Comparativa Rufus vs Balena Etcher` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** comparación basada en evidencias + conclusión técnica razonada.
- **Entregable apuntes:** `b1-6-comparativa-rufus-vs-balena-etcher.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A crear medios USB con **dos herramientas** distintas.
> - A **comparar con criterios** (control, facilidad, velocidad, compatibilidad).
> - A elaborar **documentación técnica** basada en evidencias.
>
> **Siguiente:** B1.7 — Kit multiboot actualizable con Ventoy.
