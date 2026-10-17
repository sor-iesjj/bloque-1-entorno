---
Práctica: B1.15
Bloque: 01_Entorno
Nivel: 2
Nivel_nombre: Intermedio
RA: RA.01
CE: CE.01.i
Playlist: B1_Entorno
Vídeo: B1.15 · Red de laboratorio en Hyper-V (Windows 11 y Windows Server)
---

## B1.15 — Red de laboratorio en Hyper-V: Windows 11 y Windows Server

> [!abstract] Ficha de la práctica
> ### 📌 `B1.15` — Red de laboratorio en Hyper-V (Windows 11 y Windows Server)
> - **Bloque 1** (Preparar el entorno) · **Nivel 2** (Intermedio) · **RA.01** · **CE.01.i**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.15 · Red de laboratorio en Hyper-V (Windows 11 y Windows Server)`

> [!info] Caso real (contexto profesional)
> En una empresa que trabaja con Microsoft, el servidor es un **Windows Server** y el hipervisor suele ser **Hyper-V**, que ya viene dentro de Windows. El técnico hace lo mismo que en B1.14: monta el servidor y un puesto cliente, y comprueba que **se ven** antes de configurar nada más. La idea es la misma; cambian las herramientas.

- **🎯 Objetivo real:** crear en **Hyper-V** una VM **Windows Server 2025** (servidor) y una VM **Windows 11 Pro** (cliente), conectadas a una red privada, con ping en los dos sentidos.
- **🧩 Problema que resuelve:** el **Bloque 3** parte de aquí. Y vas a ver que entre dos Windows el ping falla **en los dos sentidos** hasta que tocas el firewall de **cada uno**.

> [!note] Qué NO es esta práctica
> No instalas ningún rol en el servidor: ni Active Directory, ni DNS, ni nada. **Dos máquinas en la misma red y que se vean.** El resto llega en el Bloque 3.

> [!warning] Requisitos del equipo
> - **Windows 11 Pro** (o Enterprise/Education) con **Hyper-V activado**. Windows 11 Home **no tiene Hyper-V** y no se le puede añadir.
> - Permiso para crear conmutadores y máquinas virtuales en Hyper-V. **Si el Administrador de Hyper-V te da error de permisos, avisa al profesor**: no intentes saltártelo.
> - Las dos VM encendidas a la vez piden **8 GB de RAM** solo para ellas.

---

## 📚 Fundamento

> [!info] La idea: el mismo cable, con otro nombre
> Hyper-V no tiene «adaptadores en modo NAT o red interna», como VirtualBox. Tiene **conmutadores virtuales** (*switches*): creas el switch una vez y luego **enchufas** a él las tarjetas de las VM. Es exactamente lo que harías en una oficina: un switch en el armario y cables a cada equipo.
>
> | Lo que quieres | VirtualBox (B1.14) | Hyper-V (esta práctica) |
> | :--- | :--- | :--- |
> | Salir a Internet | Adaptador en **NAT** | Tarjeta en el **Default Switch** (ya viene creado) |
> | Red solo entre VM | **Red interna** `LAB_RED` | Conmutador **Privado** `LAB_RED` |
> | Red entre VM y el anfitrión | Solo-anfitrión | Conmutador **Interno** |
> | La VM en la red real del aula | Puente | Conmutador **Externo** |
>
> Vas a usar las dos primeras filas. El conmutador **privado** es el «cable» entre las dos VM: **tu ordenador no está conectado a él**, así que desde el anfitrión no harás ping. No es un fallo, es el diseño.
>
> El plan de direcciones, el mismo que usa el Bloque 3:
>
> | Máquina | Papel | IP en `LAB_RED` |
> | :--- | :--- | :--- |
> | Windows Server 2025 | Servidor | `10.10.10.10/24` |
> | Windows 11 Pro | Cliente | `10.10.10.20/24` |

> [!warning] El fallo nº1: ahora hay DOS firewalls
> En B1.14 solo había un Windows, y el ping fallaba en un sentido. Aquí **los dos son Windows**, y los dos bloquean por defecto el ping que les llega: **fallará en los dos sentidos**. Tendrás que abrirlo en **cada máquina**. Si solo lo abres en una, solo funciona hacia esa.

> [!tip] Dos redes `LAB_RED` que no se conocen
> Si hiciste B1.14, ahora tienes una `LAB_RED` en VirtualBox y otra en Hyper-V. **No tienen nada que ver**: cada hipervisor tiene las suyas, y una VM de VirtualBox no ve a una de Hyper-V aunque las redes se llamen igual. Y como ninguna de las dos tiene una tarjeta en tu ordenador, **tampoco chocan** con las demás redes del anfitrión.

> [!example] Vocabulario de esta práctica
> - **Conmutador virtual (Hyper-V):** el switch donde se enchufan las tarjetas de las VM.
> - **Conmutador privado:** solo conecta VM entre sí. El anfitrión no participa.
> - **Default Switch:** el conmutador que Hyper-V crea solo para dar Internet por NAT, con IP automática.
> - **Generación 2:** el tipo de VM moderna de Hyper-V (arranque UEFI, arranque seguro, TPM). La que pide Windows 11.
> - **APIPA (`169.254.x.x`):** la dirección que Windows se pone a sí mismo cuando nadie le da IP.

> [!example] Los comandos nuevos
> | Dónde | Comando | Para qué |
> | :--- | :--- | :--- |
> | Anfitrión (PowerShell admin) | `New-VMSwitch -Name "LAB_RED" -SwitchType Private` | Crear el conmutador privado sin pasar por las ventanas |
> | VM Windows | `ipconfig` · `Get-NetAdapter` | Ver las tarjetas y su IP |
> | VM Windows | `New-NetIPAddress` | Poner una IP fija |
> | VM Windows | `New-NetFirewallRule` | Permitir el ping entrante |

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-15-red-hyper-v-windows-11-y-windows-server.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura del **Bloque 0 · Fase 0.1.b** y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.15 · Red de laboratorio en Hyper-V (Windows 11 y Windows Server)`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `🔗 Enlaces`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

> [!tip] Las instalaciones también se graban
> La práctica se graba **entera**, instalaciones incluidas. Para que quien corrige no tenga que ver media hora de barras de progreso, pon un **timestamp al empezar y otro al acabar cada instalación**. Lo que de verdad se evalúa son los pasos de red: que se vean bien.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Ten a mano las ISO de **Windows Server 2025** (la versión de evaluación de 180 días, descarga oficial de Microsoft) y de **Windows 11** (verificadas, B1.4). Abre el **Administrador de Hyper-V**. Arranca OBS y preséntate.

> [!example] Paso 1 — Crea el conmutador privado
> En el Administrador de Hyper-V: **Acciones → Administrador de conmutadores virtuales → Nuevo conmutador de red virtual → Privado → Crear conmutador virtual**. Nombre: `LAB_RED` → **Aceptar**.
>
> *Lo mismo en PowerShell como administrador, en el anfitrión:*
> ```powershell
> New-VMSwitch -Name "LAB_RED" -SwitchType Private
> ```
> **Por qué privado y no interno:** con **interno**, Hyper-V crearía también una tarjeta en tu ordenador, y tendrías que darle una IP sin que choque con nada más. Con **privado** solo están las dos VM, como dos equipos unidos por un cable.

> [!example] Paso 2 — Crea la VM del servidor: Windows Server 2025
> **Acciones → Nuevo → Máquina virtual**:
> - **Nombre:** `B1-WinServer`.
> - **Generación 2.**
> - **Memoria:** `4096` MB.
> - **Red:** `Default Switch`. Esta es la tarjeta de Internet.
> - **Disco:** nuevo, de 64 GB.
> - **Instalación:** desde la ISO de Windows Server 2025.
>
> **Antes de arrancarla**, en **Configuración**:
> - **Procesador:** `2` procesadores virtuales. Hyper-V pone 1 por defecto, y el sistema va a ir justo.
> - **Agregar hardware → Adaptador de red → Agregar → Conmutador virtual: `LAB_RED`** → **Aceptar**. Esta es la segunda tarjeta, la del laboratorio.

> [!example] Paso 3 — Instala Windows Server
> Arranca la VM y **pulsa una tecla en cuanto veas «Press any key to boot from CD or DVD…»**. Si no llegas a tiempo, la VM intenta arrancar por red y se queda colgada: apágala y vuelve a encenderla.
>
> Elige **Windows Server 2025 Standard Evaluation (Experiencia de escritorio)**: la versión con escritorio, la misma que usa el Bloque 3. Pon una contraseña al `Administrador` y **apúntala**.

> [!example] Paso 4 — Dale IP fija al servidor
> En el servidor, abre **PowerShell como administrador**:
> ```powershell
> ipconfig
> ```
> Verás dos tarjetas:
> - La del **Default Switch** tiene una IP automática que suele empezar por `172.`. Es la de Internet.
> - La de **`LAB_RED`** tiene una **`169.254.x.x`**: nadie le ha dado IP. **Esa es la tuya.**
>
> Mira cómo se llama (normalmente `Ethernet 2`) y ponle la IP:
> ```powershell
> New-NetIPAddress -InterfaceAlias "Ethernet 2" -IPAddress 10.10.10.10 -PrefixLength 24
> ```
> Sin puerta de enlace: Internet ya sale por el Default Switch.

> [!example] Paso 5 — Crea la VM del cliente: Windows 11 Pro
> **Nuevo → Máquina virtual**:
> - **Nombre:** `B1-Win11-HV`.
> - **Generación 2.**
> - **Memoria:** `4096` MB, **sin** marcar la memoria dinámica, para que el instalador vea siempre los 4 GB.
> - **Red:** `Default Switch`.
> - **Disco:** nuevo, de 64 GB.
> - **Instalación:** desde la ISO de Windows 11.
>
> **Antes de arrancarla**, en **Configuración**:
> - **Seguridad → Habilitar el Módulo de plataforma segura (TPM).** Sin TPM, el instalador de Windows 11 dice que el equipo «no cumple los requisitos».
> - **Procesador:** `2`. **Windows 11 exige 2 núcleos como mínimo**; con 1 no se instala.
> - **Agregar hardware → Adaptador de red → `LAB_RED`.**
>
> Instala **Windows 11 Pro**. Recuerda pulsar una tecla al arrancar desde el DVD.

> [!example] Paso 6 — Dale IP fija al cliente
> Igual que en el servidor: localiza con `ipconfig` la tarjeta que tiene `169.254.x.x` y ejecuta, en PowerShell como administrador:
> ```powershell
> New-NetIPAddress -InterfaceAlias "Ethernet 2" -IPAddress 10.10.10.20 -PrefixLength 24
> ```
> Si Windows pregunta si quieres que el equipo sea visible en la red, contesta **No**.

> [!example] Paso 7 — El ping: falla en los dos sentidos
> **Desde el cliente:** `ping 10.10.10.10` → ❌ **Tiempo de espera agotado.**
> **Desde el servidor:** `ping 10.10.10.20` → ❌ **Tiempo de espera agotado.**
>
> Grábalo. La red está bien montada. Lo que pasa es que **cada Windows tiene su firewall** y **cada uno** bloquea el ping que le llega.

> [!example] Paso 8 — Abre el ping en el servidor… y solo en el servidor
> En el **servidor**, PowerShell como administrador:
> ```powershell
> New-NetFirewallRule -DisplayName "LAB - Ping entrante (ICMPv4)" -Direction Inbound -Protocol ICMPv4 -IcmpType 8 -Action Allow
> ```
> Repite los dos pings:
> - Cliente → servidor: ✅ **funciona.**
> - Servidor → cliente: ❌ **sigue fallando.**
>
> **Esto es lo que tienes que ver con tus propios ojos:** la regla solo deja entrar el ping **en la máquina donde la creas**.

> [!example] Paso 9 — Abre el ping en el cliente
> En el **cliente**, la misma orden:
> ```powershell
> New-NetFirewallRule -DisplayName "LAB - Ping entrante (ICMPv4)" -Direction Inbound -Protocol ICMPv4 -IcmpType 8 -Action Allow
> ```
> Repite los dos pings: ✅ **los dos con 0 % de pérdida.**
>
> Abres **solo el ping** y **no apagas el firewall**, por lo mismo que en B1.14.

> [!example] Paso 10 — Guarda el estado y cierra la grabación
> Apaga las dos VM y crea un **punto de control** de cada una: clic derecho → **Punto de control**. En Hyper-V, las instantáneas se llaman así. Renómbralo `B1.15 · Red OK`. **El servidor lo vas a reutilizar en B1.15b.**
>
> Detén OBS, nombra el vídeo **`B1.15 · Red de laboratorio en Hyper-V (Windows 11 y Windows Server)`**, súbelo a **`B1_Entorno`** y añade los timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | No pulsar una tecla al arrancar desde el DVD | La VM intenta arrancar por red y se queda en una pantalla negra con mensajes de PXE | Apágala, enciéndela y pulsa una tecla en cuanto lo pida |
> | VM de Windows 11 sin TPM o con 1 procesador | El instalador dice que el equipo no cumple los requisitos | TPM activado en Seguridad y 2 procesadores, **antes** de arrancar |
> | Conectar la segunda tarjeta al `Default Switch` en vez de a `LAB_RED` | Las dos tarjetas reciben IP `172.x` y no hay red de laboratorio | Comprueba en Configuración a qué conmutador va cada tarjeta |
> | Conmutador **Interno** en lugar de **Privado** | Aparece una tarjeta nueva en tu ordenador que nadie ha configurado | Usa **Privado**: el anfitrión no pinta nada en esta red |
> | Poner la IP en la tarjeta del Default Switch | Te quedas sin Internet y el ping no va | La del laboratorio es la que tenía `169.254.x.x` |
> | Crear la regla de firewall solo en una máquina | El ping va hacia esa y no hacia la otra | Una regla en **cada** Windows |
> | Apagar el firewall «para que funcione» | Funciona, pero has abierto el equipo a todo | Regla solo para ICMPv4 tipo 8 |
> | Error de permisos al crear el conmutador o la VM | El Administrador de Hyper-V no deja continuar | Avisa al profesor; no lo intentes por otra vía |

> [!success] ✅ Verificación: ¿está bien hecho?
> - `ipconfig` en el servidor: `10.10.10.10` en la tarjeta de `LAB_RED`, **sin puerta de enlace** en ella.
> - `ipconfig` en el cliente: `10.10.10.20` en la tarjeta de `LAB_RED`, **sin puerta de enlace** en ella.
> - `ping 10.10.10.10` desde el cliente y `ping 10.10.10.20` desde el servidor: **0 % perdidos** los dos.
> - **Internet sigue funcionando en las dos:** abre una web en cada una.
> - El **firewall sigue activado** en las dos.
> - Las dos VM tienen el punto de control `B1.15 · Red OK`.

> [!question] Comprueba que lo has entendido
> 1. Con tus palabras: ¿por qué aquí el ping fallaba en los dos sentidos y en B1.14 solo en uno?
> 2. Después del Paso 8, el ping cliente → servidor funcionaba y el servidor → cliente no. ¿Qué te dice eso sobre **dónde** actúa una regla de entrada?
> 3. ¿Qué diferencia hay entre un conmutador **privado** y uno **interno**? ¿Por qué has usado el privado?
> 4. Haz una tabla de dos columnas, VirtualBox y Hyper-V, con lo que has usado en B1.14 y aquí para lo mismo.

---

## ✅ Entregables y cierre

- **Entregable:** conmutador privado `LAB_RED`, VM `B1-WinServer` y VM `B1-Win11-HV` con ping en los dos sentidos y el punto de control `B1.15 · Red OK` (evidenciado en el vídeo).
- **Entregable vídeo:** `B1.15 · Red de laboratorio en Hyper-V (Windows 11 y Windows Server)` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** ping en los dos sentidos con **0 % de pérdida**, Internet en las dos VM y **los dos firewalls encendidos**.
- **Entregable apuntes:** `b1-15-red-hyper-v-windows-11-y-windows-server.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - Que en Hyper-V la red se monta con **conmutadores virtuales**, y cuál equivale a cada modo de VirtualBox.
> - A preparar una VM de **Generación 2** para Windows 11: TPM y 2 procesadores.
> - Que **cada Windows tiene su firewall**, y que una regla de entrada solo abre la máquina donde la creas.
>
> **Siguiente:** B1.15b — El mismo Windows Server, ahora con un cliente **Ubuntu Desktop**.
