---
Práctica: B1.5
Bloque: 01_Entorno
Nivel: 1
Nivel_nombre: Básico
RA: RA1
CE: 1.a, 1.b, 1.c, 1.d
Playlist: B1_Entorno
Vídeo: B1.5 · USB booteable con Rufus
---

## B1.5 — Creación de un USB booteable con Rufus

> [!abstract] Ficha de la práctica
> ### 📌 `B1.5` — USB booteable con Rufus
> - **Bloque 1** (Preparar el entorno) · **Nivel 1** (Básico) · **RA1** · **CE 1.a, 1.b, 1.c, 1.d**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.5 · USB booteable con Rufus`

> [!info] Caso real (contexto profesional)
> En el aula (o en una empresa) varios equipos carecen de lector óptico y hay que reinstalarlos con Ubuntu Server. El técnico crea un **medio de instalación USB** compatible tanto con **BIOS** como con **UEFI**. Es una tarea frecuentísima en despliegues rápidos sin soporte óptico.

- **🎯 Objetivo real:** crear un USB de arranque a partir de una ISO, eligiendo bien el esquema de partición según el firmware del equipo destino.
- **🧩 Problema que resuelve:** sin un medio de arranque válido, no se puede instalar el SO en un equipo físico.

---

## 📚 Fundamento

> [!info] Antes de empezar: partición y firmware van de la mano
> El **firmware** del equipo (el arranque de la placa) puede ser **BIOS** (antiguo) o **UEFI** (moderno). El esquema de partición del USB debe coincidir: **GPT** para UEFI, **MBR** para BIOS. Y el sistema de archivos del arranque suele ser **FAT32** (obligatorio para UEFI).

> [!warning] Secure Boot (el "por qué no arranca" nº 1)
> En equipos UEFI modernos está activo el **Secure Boot**, que solo permite arrancar software firmado. Algunos medios (o herramientas antiguas) no arrancan con Secure Boot activo. Si el USB no arranca en UEFI, **entra en la BIOS/UEFI y desactiva temporalmente Secure Boot** (o usa una ISO firmada, como Ubuntu, que sí lo soporta).

> [!example] Vocabulario de esta práctica
> - **Rufus:** programa gratuito de Windows para crear USB booteables (`rufus.ie`).
> - **MBR / GPT:** esquemas de tabla de particiones (BIOS / UEFI).
> - **FAT32:** sistema de archivos exigido para el arranque UEFI.
> - **Secure Boot:** control UEFI que solo permite arrancar software firmado.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.5 · USB booteable con Rufus`** y súbelo a **`B1_Entorno`** (No listado).
> 5. **Una sola entrega.**

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate. Ten a mano la ISO ya **verificada** (B1.4) y un USB de **8 GB o superior**.

> [!example] Paso 1 — Descarga y ejecuta Rufus
> Descarga **Rufus** desde `https://rufus.ie/es/` (versión portable) y ejecútalo **con privilegios de administrador**.

> [!example] Paso 2 — Selecciona el USB y la ISO
> En **Dispositivo**, elige tu unidad USB. En **Elección de arranque**, selecciona la **ISO** verificada.

> [!example] Paso 3 — Configura esquema y sistema de archivos
> - **Esquema de partición:** **GPT** (para UEFI) o **MBR** (para BIOS), según el equipo destino.
> - **Sistema de archivos:** **FAT32** (para UEFI) o NTFS (para BIOS).

> [!example] Paso 4 — Escribe la ISO
> Pulsa **EMPEZAR** y espera a que termine. ⚠️ **Se borra todo el contenido del USB.**

> [!example] Paso 5 — Prueba el arranque (BIOS y UEFI)
> Arranca un equipo o máquina virtual desde el USB. Comprueba que entra el instalador. Si en UEFI no arranca, revisa **Secure Boot** (desactívalo temporalmente si hace falta).

> [!example] Paso 6 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.5 · USB booteable con Rufus`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Elegir MBR para un equipo UEFI | El USB no arranca | Usa **GPT** en UEFI, **MBR** en BIOS. |
> | No arranca con Secure Boot activo | Bloqueo de arranque | Desactiva **Secure Boot** temporalmente o usa ISO firmada. |
> | Seleccionar el disco equivocado | Borras un disco que no era | Comprueba la letra/tamaño del USB antes de EMPEZAR. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - El USB **arranca** el instalador en el modo previsto (BIOS o UEFI).
> - Sabes explicar la relación **esquema de partición ↔ firmware**.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué esquema de partición usarías para un equipo **UEFI**? ¿Y para **BIOS**?
> 2. ¿Por qué el arranque UEFI suele exigir **FAT32**?
> 3. ¿Qué es **Secure Boot** y por qué puede impedir el arranque?

---

## ✅ Entregables y cierre

- **Entregable:** USB booteable funcional (evidenciado en el vídeo arrancando).
- **Entregable vídeo:** `B1.5 · USB booteable con Rufus` en `B1_Entorno`. **Una sola entrega.**
- **Criterio de éxito:** USB que arranca correctamente + comprensión del vínculo partición/firmware.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A crear un **USB booteable** con Rufus a partir de una ISO.
> - A elegir **MBR/GPT** y **FAT32** según BIOS/UEFI.
> - Qué es **Secure Boot** y cómo resolver que un USB no arranque.
>
> **Siguiente:** B1.6 — Comparativa Rufus vs Balena Etcher.
