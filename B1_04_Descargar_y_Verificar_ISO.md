---
Práctica: B1.4
Bloque: 01_Entorno
Nivel: 1
Nivel_nombre: Básico
RA: RA1
CE: 1.a, 1.d
Playlist: B1_Entorno
Vídeo: B1.4 · Descargar y verificar la ISO (SHA256)
---

## B1.4 — Descargar y verificar la ISO (SHA256)

> [!abstract] Ficha de la práctica
> ### 📌 `B1.4` — Descargar y verificar la ISO (SHA256)
> - **Bloque 1** (Preparar el entorno) · **Nivel 1** (Básico) · **RA1** · **CE 1.a, 1.d**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.4 · Descargar y verificar la ISO (SHA256)`

> [!info] Caso real (contexto profesional)
> Antes de crear un USB o instalar nada, el técnico descarga la imagen ISO del sistema operativo. Pero una ISO puede **corromperse al descargar** o, peor, haber sido **manipulada** en un sitio no oficial. Instalar una imagen dañada o alterada puede arruinar el equipo o meter malware. Por eso, **siempre se verifica** antes de usarla.

- **🎯 Objetivo real:** descargar la ISO oficial y **comprobar su integridad y autenticidad** con su hash SHA256.
- **🧩 Problema que resuelve:** evitar instalar una imagen corrupta o manipulada — un fallo de seguridad grave.

---

## 📚 Fundamento

> [!info] Antes de empezar: qué es un hash y para qué sirve
> Un **hash** (SHA256) es una "huella digital" de un archivo: una cadena de 64 caracteres calculada a partir de su contenido. Si cambia **un solo bit** del archivo, el hash cambia por completo. El fabricante publica el hash oficial de su ISO; tú calculas el de tu descarga y **los comparas**: si coinciden, la ISO es íntegra y auténtica.

> [!tip] Idea clave
> **Descargar de la web oficial NO es suficiente.** La descarga puede cortarse o corromperse por el camino. Verificar el SHA256 es el paso que confirma que lo que tienes es **exactamente** lo que publicó el fabricante.

> [!example] Vocabulario de esta práctica
> - **ISO:** archivo que contiene la imagen exacta del disco de instalación del SO.
> - **Hash / SHA256:** huella digital del archivo para comprobar integridad.
> - **`Get-FileHash` (Windows):** comando de PowerShell que calcula el hash.
> - **`sha256sum` (Linux):** comando equivalente en Linux.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-4-descargar-y-verificar-la-iso-sha256.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura de la Fase 0.1 y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.4 · Descargar y verificar la ISO (SHA256)`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `Enlace al vídeo explicativo`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate.

> [!example] Paso 1 — Descarga la ISO oficial
> Descarga **Ubuntu Server 26.04 LTS** desde `ubuntu.com` (o la ISO que uses). En la misma página del fabricante, **localiza el hash SHA256 oficial** (suele estar en un fichero `SHA256SUMS` o junto al enlace de descarga). Anótalo o tenlo a la vista.

> [!example] Paso 2 — Calcula el hash de tu descarga
> - **🪟 PowerShell:**
> ```
> Get-FileHash .\ubuntu-26.04-live-server-amd64.iso -Algorithm SHA256
> ```
> - **🐧 Linux / Git Bash:**
> ```
> sha256sum ubuntu-26.04-live-server-amd64.iso
> ```

> [!example] Paso 3 — Compara los dos hash
> Compara el hash que has calculado con el **oficial** del fabricante. Deben ser **idénticos** (los 64 caracteres). Si coinciden → ISO íntegra y auténtica. Si no → **no la uses**: vuelve a descargarla.

> [!example] Paso 4 — Documenta el resultado
> Deja constancia: nombre de la ISO, hash oficial, hash calculado y **veredicto** (✅ coincide / ❌ no coincide).

> [!example] Paso 5 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.4 · Descargar y verificar la ISO (SHA256)`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Descargar la ISO de un sitio no oficial | Puede estar manipulada | Descarga **solo** de la web del fabricante. |
> | Saltarse la verificación | Instalas una imagen corrupta | Calcula y compara **siempre** el SHA256. |
> | Comparar los hash "a ojo" | Se cuela un carácter distinto | Cópialos y compáralos con cuidado (o `Compare`/`diff`). |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Has descargado la ISO de la **web oficial**.
> - El **SHA256 calculado coincide** con el oficial.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué es un **hash SHA256** y qué demuestra que coincida?
> 2. ¿Por qué no basta con descargar de la web oficial?
> 3. ¿Qué harías si el hash **no coincide**?

---

## ✅ Entregables y cierre

- **Entregable documento:** ficha de verificación (ISO, hash oficial, hash calculado, veredicto).
- **Entregable vídeo:** `B1.4 · Descargar y verificar la ISO (SHA256)` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** ISO oficial + SHA256 verificado y documentado.
- **Entregable apuntes:** `b1-4-descargar-y-verificar-la-iso-sha256.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - Qué es un **hash SHA256** y por qué verifica integridad y autenticidad.
> - A calcularlo con **`Get-FileHash`** y **`sha256sum`**.
> - El hábito profesional de **no usar nunca** una ISO sin verificar.
>
> **Siguiente:** B1.5 — USB booteable con Rufus (y Secure Boot).
