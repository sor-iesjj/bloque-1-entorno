---
Práctica: B1.12
Bloque: 01_Entorno
Nivel: 3
Nivel_nombre: Avanzado
RA: RA.01 · RA.05
CE: CE.01.f, CE.05.e
Playlist: B1_Entorno
Vídeo: B1.12 · Instalación desatendida
Opcional: true
---

## B1.12 — Instalación desatendida (despliegue en masa)

> [!abstract] Ficha de la práctica
> ### 📌 `B1.12` — Instalación desatendida *(opcional / ampliación)*
> - **Bloque 1** (Preparar el entorno) · **Nivel 3** (Avanzado) · **RA.01 · RA.05** · **CE.01.f · CE.05.e**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.12 · Instalación desatendida`

> [!info] Caso real (contexto profesional)
> Hay que instalar **20 equipos idénticos**. Hacer clic uno a uno en cada instalador es lento y propenso a errores. El técnico prepara una **instalación desatendida**: un archivo de respuestas con todas las decisiones (disco, red, usuario…), de modo que la instalación se ejecuta **sola** y **siempre igual**.

- **🎯 Objetivo real:** automatizar la instalación con un archivo de respuestas para desplegar en masa de forma consistente.
- **🧩 Problema que resuelve:** el "despliegue masivo" real de hoy, viable en el aula (a diferencia de tocar el DHCP para un PXE clásico).

---

## 📚 Fundamento

> [!info] Antes de empezar: el archivo de respuestas
> Una instalación desatendida usa un **archivo de respuestas** que el instalador lee para no preguntar nada:
> - **Ubuntu Server 26.04:** **autoinstall** (basado en **cloud-init**), con un fichero `user-data` (YAML).
> - **Windows:** **unattend.xml**, generado (p. ej. con herramientas de respuesta) y colocado en el medio de instalación.

> [!tip] Idea clave
> Automatizar la instalación garantiza que los 20 equipos quedan **exactamente iguales**: mismo particionado, mismos usuarios, mismos paquetes. La consistencia es clave en un parque de equipos.

> [!example] Vocabulario de esta práctica
> - **Instalación desatendida:** instalación que se ejecuta sola con un archivo de respuestas.
> - **autoinstall / cloud-init:** mecanismo de Ubuntu Server (`user-data` YAML).
> - **unattend.xml:** archivo de respuestas de Windows.
> - **Idempotente:** que repetido da siempre el mismo resultado.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-12-instalacion-desatendida.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura de la Fase 0.1 y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.12 · Instalación desatendida`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `Enlace al vídeo explicativo`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate. Elige **una** de las dos vías (Ubuntu o Windows) según tu SO objetivo.

> [!example] Paso 1 (Ubuntu) — Prepara el `user-data`
> Crea un fichero **`user-data`** (YAML) con la configuración de autoinstall: idioma, particionado, usuario, paquetes (p. ej. OpenSSH). Añade un `meta-data` vacío.

> [!example] Paso 1 (Windows) — Prepara el `unattend.xml`
> Genera un **`unattend.xml`** con las respuestas (idioma, disco, usuario, clave) y colócalo donde el instalador lo detecte.

> [!example] Paso 2 — Pon el archivo a disposición del instalador
> Sirve el `user-data`/`unattend.xml` al instalador (por USB, por red o por el parámetro de arranque `autoinstall` en Ubuntu).

> [!example] Paso 3 — Lanza la instalación desatendida
> Arranca la VM/equipo y comprueba que la instalación **avanza sola**, sin preguntar.

> [!example] Paso 4 — Verifica el resultado
> Al terminar, comprueba que el equipo quedó con **lo definido** (usuario, red, paquetes). Repite en una segunda VM para comprobar que sale **idéntico**.

> [!example] Paso 5 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.12 · Instalación desatendida`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | YAML de `user-data` mal indentado | El autoinstall falla | Respeta la **indentación** del YAML (espacios, no tabuladores). |
> | El instalador no encuentra el archivo | Sigue preguntando | Colócalo donde el instalador lo busca (medio/parámetro correctos). |
> | Contraseñas en claro sin cuidado | Riesgo de seguridad | Usa hashes cuando el formato lo permita; no reutilices claves reales. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - La instalación se completa **sin intervención**.
> - Dos equipos salen **idénticos** con el mismo archivo.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué es un **archivo de respuestas** y qué problema resuelve?
> 2. ¿Cómo se llama el mecanismo en **Ubuntu**? ¿Y en **Windows**?
> 3. ¿Por qué importa que el resultado sea **idéntico** en todos los equipos?

---

## ✅ Entregables y cierre

- **Entregable:** archivo de respuestas (`user-data` o `unattend.xml`) + instalación desatendida (evidenciada en el vídeo).
- **Entregable vídeo:** `B1.12 · Instalación desatendida` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** instalación completada sola + resultado reproducible en un segundo equipo.
- **Entregable apuntes:** `b1-12-instalacion-desatendida.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A automatizar una instalación con un **archivo de respuestas**.
> - **autoinstall/cloud-init** (Ubuntu) y **unattend.xml** (Windows).
> - El **despliegue en masa** consistente, la forma real de instalar muchos equipos hoy.
>
> **Siguiente:** B1.13 — Proyecto final de integración.
