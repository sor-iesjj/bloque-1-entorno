---
Práctica: B1.13
Bloque: 01_Entorno
Nivel: 3
Nivel_nombre: Avanzado — Integrador
RA: RA.01 · RA.05
CE: CE.01.b, CE.01.c, CE.01.f, CE.05.e, CE.05.f
Playlist: B1_Entorno
Vídeo: B1.13 · Proyecto final de integración
---

## B1.13 — Proyecto final de integración del bloque

> [!abstract] Ficha de la práctica
> ### 📌 `B1.13` — Proyecto final de integración
> - **Bloque 1** (Preparar el entorno) · **Nivel 3** (Integrador) · **RA.01 · RA.05** · **CE.01.b · CE.01.c · CE.01.f · CE.05.e · CE.05.f**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.13 · Proyecto final de integración`

> [!info] Caso real (contexto profesional)
> El departamento de sistemas del instituto **estandariza la preparación** de los equipos del aula. Cada grupo simula ser un **equipo técnico** responsable de un despliegue real: limpiar los discos, instalar los sistemas y dejar un kit de mantenimiento. Es la práctica que **integra todo el bloque**.

- **🎯 Objetivo real:** integrar todos los métodos del bloque en un flujo completo y documentar tiempos, fiabilidad y conclusiones.
- **🧩 Problema que resuelve:** demostrar que no solo ejecutas herramientas sueltas, sino que sabes **diseñar y ejecutar un despliegue completo**.

---

## 📚 Fundamento

> [!info] Antes de empezar: juntar las piezas
> Este proyecto encadena lo aprendido: **verificar la ISO** (B1.4) → **preparar el disco con GParted** (B1.8) → **instalar** por USB (B1.5/B1.10) **y por red con iVentoy** (B1.11) → dejar un **kit Ventoy** de mantenimiento (B1.7). Y, sobre todo, **comparar y documentar** qué método es más rápido y fiable.

> [!tip] Idea clave
> No se evalúa "hacer clics", sino **decidir y justificar**: qué método usarías en cada situación (un equipo suelto vs. 20 equipos), y demostrarlo con datos (tiempos, incidencias).

> [!example] Vocabulario de esta práctica
> - **Flujo de despliegue:** secuencia completa de preparación e instalación de equipos.
> - **Estandarización:** que todos los equipos queden igual y de forma repetible.
> - **Defensa:** explicación razonada de las decisiones tomadas.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por apartado.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> Al ser el proyecto final, el vídeo es también una **defensa**: además de mostrar el flujo, **explicas y justificas** tus decisiones.
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-13-proyecto-final-de-integracion.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura del **Bloque 0 · Fase 0.1.b** y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por apartado/fase.
> 4. **Al terminar:** nombra el vídeo **`B1.13 · Proyecto final de integración`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `🔗 Enlaces`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate. Trabaja en el **laboratorio virtual** (B1.9) con varias VMs como "equipos del aula".

> [!example] Paso 1 — Limpia el disco con GParted
> Arranca GParted (B1.8) y **prepara el disco** de un equipo: tabla nueva y particiones limpias.

> [!example] Paso 2 — Instala por USB (Rufus/Ventoy)
> Instala un SO en ese equipo con **USB booteable** (B1.5) o desde tu **kit Ventoy** (B1.7). Mide el **tiempo**.

> [!example] Paso 3 — Instala por red (iVentoy)
> En otro(s) equipo(s), instala **por red con iVentoy** (B1.11) en red aislada. Mide el **tiempo** y anota incidencias.

> [!example] Paso 4 — Prepara el kit de mantenimiento
> Deja listo un **USB Ventoy** con SO + utilidades (GParted…) como kit del "equipo técnico".

> [!example] Paso 5 — Documenta y compara
> Elabora un informe: **tiempos y fiabilidad de USB vs red**, incidencias, y **conclusión** (qué método usar en cada caso). Justifícalo.

> [!example] Paso 6 — Cierra la grabación (defensa) y súbela
> Detén OBS, nombra el vídeo **`B1.13 · Proyecto final de integración`**, súbelo a **`B1_Entorno`** y añade timestamps por apartado.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Enseñar sin justificar | No demuestras criterio | Explica **por qué** cada decisión (defensa). |
> | Comparar sin datos | Conclusión débil | Mide **tiempos** e incidencias reales. |
> | Montar iVentoy en la red del centro | Interfieres con el instituto | Usa **red aislada** (interna VirtualBox). |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Has ejecutado el **flujo completo**: disco → instalación USB → instalación red → kit.
> - Tienes un **informe comparativo** (USB vs red) con conclusión justificada.
> - El vídeo-defensa está en la playlist `B1_Entorno` con timestamps por apartado.

> [!question] Autoevaluación antes de entregar
> 1. ¿Sabrías decidir, ante un caso, si desplegar por **USB** o por **red**? ¿Con qué argumentos?
> 2. ¿Tu informe respalda la conclusión con **datos** (tiempos, fiabilidad)?
> 3. ¿Podrías **repetir** el despliegue y obtener el mismo resultado?

---

## ✅ Entregables y cierre

- **Entregable documento:** informe del despliegue (flujo, tiempos, comparativa USB vs red, conclusión).
- **Entregable:** kit Ventoy de mantenimiento + equipos instalados (evidenciado en el vídeo).
- **Entregable vídeo (defensa):** `B1.13 · Proyecto final de integración` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** flujo completo ejecutado + comparativa con datos + decisiones justificadas.
- **Entregable apuntes:** `b1-13-proyecto-final-de-integracion.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has demostrado con este proyecto
> - Que **integras** todos los métodos del bloque (verificar, particionar, instalar por USB y por red, kit Ventoy).
> - Que sabes **comparar y decidir** el método adecuado según el caso.
> - Que puedes **documentar y defender** un despliegue como un profesional.
>
> **¡Fin del Bloque 1!** Con el entorno preparado y el laboratorio montado, ya puedes empezar el proyecto **Boochan** (Bloques 2–3).
