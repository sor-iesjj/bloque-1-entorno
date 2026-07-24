---
Práctica: B1.8
Bloque: 01_Entorno
Nivel: 2
Nivel_nombre: Intermedio
RA: RA1, RA3, RA5
CE: 1.b, 1.c, 3.b, 5.a
Playlist: B1_Entorno
Vídeo: B1.8 · Particiones MBR/GPT con GParted
---

## B1.8 — Gestión y reparación de particiones con GParted

> [!abstract] Ficha de la práctica
> ### 📌 `B1.8` — Particiones MBR/GPT con GParted
> - **Bloque 1** (Preparar el entorno) · **Nivel 2** (Intermedio) · **RA1, RA3, RA5** · **CE 1.b, 1.c, 3.b, 5.a**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.8 · Particiones MBR/GPT con GParted`

> [!info] Caso real (contexto profesional)
> Una empresa de mantenimiento recibe ordenadores en los que el instalador de Windows o Linux **no detecta los discos**. El problema son particiones dañadas o un esquema incompatible. El técnico usa **GParted Live** para diagnosticar, borrar y crear una tabla de particiones compatible **antes** de instalar el SO.

- **🎯 Objetivo real:** preparar el disco (tabla de particiones y sistemas de archivos) antes de una instalación limpia.
- **🧩 Problema que resuelve:** discos con particiones defectuosas o incompatibles que impiden instalar.

---

## 📚 Fundamento

> [!info] Antes de empezar: la tabla de particiones
> Un disco necesita una **tabla de particiones** que organice su espacio. Hay dos esquemas: **MBR** (antiguo, máximo 4 primarias, discos ≤ 2 TB, ligado a BIOS) y **GPT** (moderno, muchas particiones, discos grandes, ligado a UEFI). En UEFI se necesita una pequeña **partición EFI** (FAT32) para el arranque.

> [!tip] Idea clave
> **Preparar el disco es un paso previo, no la instalación.** GParted Live arranca desde USB como un sistema independiente, así que puedes tocar el disco **sin** tener ningún SO instalado — perfecto para dejarlo limpio antes de instalar.

> [!example] Vocabulario de esta práctica
> - **GParted Live:** distribución mínima que arranca desde USB solo para gestionar particiones.
> - **Tabla de particiones (MBR/GPT):** cómo se organiza el disco.
> - **Partición EFI:** pequeña partición FAT32 necesaria para arrancar en UEFI.
> - **Sistema de archivos:** FAT32 / NTFS / ext4 según el uso.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.8 · Particiones MBR/GPT con GParted`** y súbelo a **`B1_Entorno`** (No listado).
> 5. **Una sola entrega.**

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate. Trabaja sobre un **disco de pruebas** (VM o disco secundario), **nunca** sobre el disco del sistema en uso.

> [!example] Paso 1 — Crea un USB de arranque con GParted Live
> Descarga la ISO de **GParted Live** y crea un USB booteable (con Rufus, B1.5, o añádela a tu Ventoy, B1.7).

> [!example] Paso 2 — Arranca el equipo desde GParted Live
> Arranca la VM/equipo desde el USB y entra en GParted.

> [!example] Paso 3 — Examina la tabla de particiones actual
> Selecciona el disco correcto (arriba a la derecha) y observa su esquema y particiones actuales.

> [!example] Paso 4 — Crea una tabla nueva (GPT) y particiones
> En *Dispositivo → Crear tabla de particiones*, elige **GPT**. Crea las particiones necesarias (p. ej. EFI FAT32 + una ext4 o NTFS) y formatéalas.

> [!example] Paso 5 — Aplica y verifica
> Pulsa **Aplicar** (✓) y comprueba que el disco queda con la tabla y las particiones previstas, listo para instalar.

> [!example] Paso 6 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.8 · Particiones MBR/GPT con GParted`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Trabajar sobre el disco equivocado | Pierdes datos reales | Selecciona con cuidado el disco (tamaño/nombre) y usa disco de pruebas. |
> | Crear GPT sin partición EFI | No arranca en UEFI | Añade una partición **EFI (FAT32)** para UEFI. |
> | Olvidar pulsar "Aplicar" | Los cambios no se guardan | Los cambios solo se hacen al pulsar **✓ Aplicar**. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - El disco queda con la **tabla de particiones** prevista (MBR o GPT).
> - Entiendes cuándo usar **MBR** y cuándo **GPT**.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué diferencias hay entre **MBR** y **GPT**?
> 2. ¿Para qué sirve la **partición EFI**?
> 3. ¿Por qué GParted Live arranca desde USB en vez de instalarse?

---

## ✅ Entregables y cierre

- **Entregable:** disco de pruebas preparado con la tabla y particiones (evidenciado en el vídeo).
- **Entregable vídeo:** `B1.8 · Particiones MBR/GPT con GParted` en `B1_Entorno`. **Una sola entrega.**
- **Criterio de éxito:** disco correctamente particionado y formateado, listo para instalar.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A gestionar **tablas de particiones (MBR/GPT)** con GParted Live.
> - A preparar un disco **antes** de una instalación limpia.
> - El papel de la **partición EFI** en UEFI.
>
> **Siguiente:** B1.8b — Gestión de disco con DISKPART (la misma tarea, pero por línea de comandos en Windows).
