---
Práctica: B1.4
Bloque: 01_Entorno
Nivel: 1
Nivel_nombre: Básico
RA: RA.01
CE: CE.01.b
Playlist: B1_Entorno
Vídeo: B1.4 · Descargar y verificar la ISO (SHA256)
---

## B1.4 — Descargar y verificar la ISO (SHA256)

> [!abstract] Ficha de la práctica
> ### 📌 `B1.4` — Descargar y verificar la ISO (SHA256)
> - **Bloque 1** (Preparar el entorno) · **Nivel 1** (Básico) · **RA.01** · **CE.01.b**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.4 · Descargar y verificar la ISO (SHA256)`

> [!info] Caso real (contexto profesional)
> Antes de crear un USB o instalar nada, el técnico descarga la imagen ISO del sistema operativo. Pero una ISO puede **corromperse al descargar** o, peor, haber sido **manipulada** en un sitio no oficial. Instalar una imagen dañada o alterada puede arruinar el equipo o meter malware. Por eso, **siempre se verifica** antes de usarla.

- **🎯 Objetivo real:** descargar la ISO oficial y **comprobar su integridad** con su hash SHA256.
- **🧩 Problema que resuelve:** evitar instalar una imagen corrupta o manipulada — un fallo de seguridad grave.

---

## 📚 Fundamento

> [!info] Antes de empezar: qué es un hash y para qué sirve
> Piensa en la **huella dactilar** de una persona: no te dice cómo es, pero si dos huellas coinciden, es la misma persona. Un **hash SHA256** es la huella de un archivo.
>
> - Se calcula leyendo el archivo **entero**, bit a bit, y sale siempre una cadena de **64 caracteres** (letras `a-f` y números `0-9`). Son 256 bits escritos en hexadecimal: de ahí el nombre.
> - Si cambia **un solo bit** del archivo, el hash sale **completamente distinto**, no parecido.
> - Va en **un solo sentido**: del archivo sale el hash, pero del hash no se puede reconstruir el archivo.
>
> El fabricante publica el hash oficial de su ISO. Tú calculas el de tu descarga y **los comparas**: si coinciden, tu archivo es, byte a byte, el que publicó el fabricante.

> [!warning] El fallo nº1: creer que el hash lo demuestra todo
> Que coincida demuestra **integridad**: tu copia es idéntica a la del sitio de donde sacaste el hash. Demuestra **autenticidad** (que la hizo de verdad Ubuntu o Microsoft) **solo si el hash lo has sacado de la web oficial**. Si bajas la ISO y su hash de la misma web falsa, coincidirán igual: el que la manipuló también calculó el hash.
>
> **Descargar de la web oficial NO es suficiente, y comprobar el hash tampoco lo es por sí solo.** Hacen falta las dos cosas: web oficial **y** hash comparado.

> [!important] Dónde está el hash oficial de cada ISO del bloque
> Esta tabla es **la que vas a usar en todos los laboratorios** (B1.14, B1.14b, B1.15 y B1.15b). Allí no se vuelve a explicar: se hace.
>
> | ISO | Archivo | Dónde está el hash oficial |
> | :--- | :--- | :--- |
> | Ubuntu Server 26.04 LTS | `ubuntu-26.04.1-live-server-amd64.iso` | Fichero `SHA256SUMS` en `releases.ubuntu.com/26.04.1/`: busca la línea con el nombre de tu archivo |
> | Ubuntu Desktop 26.04 LTS | `ubuntu-26.04.1-desktop-amd64.iso` | El mismo `SHA256SUMS` de arriba, en su línea |
> | Windows 11 | `Windows11_Client_x64_es-es_…iso` | En la propia página de descarga de Microsoft (`microsoft.com/es-es/software-download/windows11`): publica un hash **por idioma**. Usa el de **Español** |
> | Windows Server 2025 | `…SERVER_EVAL_x64FRE_es-es.iso` | **Microsoft no lo publica** en el Evaluation Center. Ver el aviso de abajo |
>
> El número exacto de versión (`26.04.1`) y el nombre de Windows cambian con el tiempo. **Compara siempre con el hash del archivo que has bajado tú**, no con el de esta tabla ni con el de un compañero.

> [!danger] Windows Server 2025: la ISO que no se puede verificar
> Como no hay hash oficial, **no tienes con qué comparar**. Lo único que puedes hacer:
> 1. Descargarla **solo** del Evaluation Center de Microsoft (`microsoft.com/evalcenter`). Nunca de otra web.
> 2. Calcular su hash igualmente y **apuntarlo**. No demuestra que sea la de Microsoft, pero sí te sirve para comprobar que la copia que pases a un USB u otro equipo es la misma que descargaste.
>
> Si en un foro te dicen «este es el hash oficial de Server 2025», desconfía: no viene de Microsoft.

> [!example] Vocabulario de esta práctica
> - **ISO:** archivo que contiene la imagen exacta del disco de instalación del SO.
> - **Hash / SHA256:** huella digital del archivo, de 64 caracteres.
> - **Integridad / autenticidad:** que el archivo está intacto / que viene de quien dice.
> - **`Get-FileHash` (Windows):** comando de PowerShell que calcula el hash.
> - **`sha256sum` (Linux y Git Bash):** comando equivalente.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-4-descargar-y-verificar-la-iso-sha256.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura del **Bloque 0 · Fase 0.1.b** y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.4 · Descargar y verificar la ISO (SHA256)`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `🔗 Enlaces`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate.

> [!example] Paso 1 — Descarga la ISO oficial y localiza su hash
> Descarga **Ubuntu Server 26.04 LTS** desde `ubuntu.com`. Después abre `releases.ubuntu.com/26.04.1/SHA256SUMS` y busca **la línea que lleva el nombre de tu archivo**: los 64 caracteres de delante son el hash oficial. Cópialo.

> [!example] Paso 2 — Calcula el hash de tu descarga
> Abre **PowerShell** y entra en la carpeta donde se ha descargado la ISO (normalmente `Descargas`):
> ```powershell
> cd $HOME\Downloads
> Get-FileHash .\ubuntu-26.04.1-live-server-amd64.iso -Algorithm SHA256
> ```
> Tarda unos segundos: está leyendo el archivo entero. El hash sale en la columna `Hash`, **en mayúsculas**. El de Ubuntu está en minúsculas. Es el mismo número: las mayúsculas no cuentan.
>
> En **Git Bash** el equivalente es:
> ```bash
> cd ~/Downloads
> sha256sum ubuntu-26.04.1-live-server-amd64.iso
> ```
> *(`~` es tu carpeta personal, `C:\Users\TU-USUARIO`.)*

> [!example] Paso 3 — Compara los dos hash (sin hacerlo a ojo)
> Comparar 64 caracteres mirándolos es la forma más segura de equivocarse. Que lo haga el ordenador. En **PowerShell**, pega el hash oficial entre las comillas:
> ```powershell
> (Get-FileHash .\ubuntu-26.04.1-live-server-amd64.iso).Hash -eq "PEGA-AQUI-EL-HASH-OFICIAL"
> ```
> - **`True`** → coinciden: la ISO está íntegra. Puedes usarla.
> - **`False`** → no coinciden: **no la uses**. Bórrala y vuelve a descargarla.
>
> `-eq` no distingue mayúsculas de minúsculas, así que da igual cómo venga escrito el oficial.
>
> En **Git Bash**, con **dos espacios** entre el hash y el nombre:
> ```bash
> echo "PEGA-AQUI-EL-HASH-OFICIAL  ubuntu-26.04.1-live-server-amd64.iso" | sha256sum -c
> ```
> Si coinciden, responde `OK`; si no, `FAILED`.

> [!example] Paso 4 — Documenta el resultado
> Deja constancia en tu entrada: nombre de la ISO, hash oficial, hash calculado y **veredicto** (`True` / `False`).

> [!example] Paso 5 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.4 · Descargar y verificar la ISO (SHA256)`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Descargar la ISO de un sitio no oficial | Puede estar manipulada, y su hash coincidirá igual | Descarga **solo** de la web del fabricante, y el hash también |
> | Saltarse la verificación | Instalas una imagen corrupta | Calcula y compara **siempre** el SHA256 |
> | Comparar los hash "a ojo" | Se cuela un carácter distinto y no lo ves | Usa `-eq` en PowerShell o `sha256sum -c` en Git Bash |
> | Pensar que no coinciden porque uno está en mayúsculas | Descartas una ISO que estaba bien | Las mayúsculas no cuentan: `-eq` ya lo tiene en cuenta |
> | Copiar el hash de la línea de otro archivo en `SHA256SUMS` (Desktop en vez de Server, o `26.04` en vez de `26.04.1`) | Sale `False` con una ISO buena | Busca la línea con **exactamente** el nombre de tu archivo |
> | `Get-FileHash` dice que no encuentra el archivo | No estás en la carpeta de la descarga, o el nombre no es igual | `cd` a la carpeta y escribe el nombre real (pulsa `Tab` para completarlo) |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Has descargado la ISO de la **web oficial**.
> - La comparación ha dado **`True`** (o `OK` en Git Bash).
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué es un **hash SHA256** y qué demuestra que coincida?
> 2. ¿Por qué no basta con descargar de la web oficial? ¿Y por qué no basta con que coincida el hash?
> 3. ¿Qué harías si te sale **`False`**?
> 4. ¿Por qué la ISO de **Windows Server 2025** no se puede verificar como las otras tres? ¿Qué haces con ella?

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
> - Qué es un **hash SHA256** y la diferencia entre **integridad** y **autenticidad**.
> - A calcularlo con **`Get-FileHash`** y **`sha256sum`**, y a compararlo con **`-eq`** en vez de a ojo.
> - Dónde está el hash oficial de **cada ISO del bloque**, y qué hacer con la que no lo tiene.
> - El hábito profesional de **no usar nunca** una ISO sin verificar. Lo repetirás en cada laboratorio.
>
> **Siguiente:** B1.5 — USB booteable con Rufus (y Secure Boot).
