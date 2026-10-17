---
Práctica: B1.14
Bloque: 01_Entorno
Nivel: 2
Nivel_nombre: Intermedio
RA: RA.01
CE: CE.01.i
Playlist: B1_Entorno
Vídeo: B1.14 · Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server)
---

## B1.14 — Red de laboratorio en VirtualBox: Windows 11 y Ubuntu Server

> [!abstract] Ficha de la práctica
> ### 📌 `B1.14` — Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server)
> - **Bloque 1** (Preparar el entorno) · **Nivel 2** (Intermedio) · **RA.01** · **CE.01.i**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.14 · Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server)`

> [!info] Caso real (contexto profesional)
> Antes de montar un servidor de verdad, un técnico comprueba lo más básico: que el servidor y el equipo cliente **se ven en la red**. Si no hay ping, no habrá dominio, ni carpetas compartidas, ni nada. En una oficina eso es un cable y un switch. Aquí vas a hacer lo mismo **sin cables**: dos máquinas virtuales conectadas por una red que solo existe dentro de VirtualBox.

- **🎯 Objetivo real:** crear una VM **Ubuntu Server** (servidor) y una VM **Windows 11 Pro** (cliente), conectarlas a la misma red de laboratorio y conseguir que **se hagan ping en los dos sentidos**.
- **🧩 Problema que resuelve:** todo lo que harás en el **Bloque 2** parte de aquí. Si hoy entiendes por qué dos máquinas se ven (o no se ven), mañana no perderás una tarde buscando el fallo en el sitio equivocado.

> [!note] Qué NO es esta práctica
> No configuras ningún servicio: ni dominio, ni carpetas compartidas, ni DHCP. **Dos máquinas en la misma red y que se vean. Nada más.** El resto llega en el Bloque 2.

---

## 📚 Fundamento

> [!info] La idea: un cable que no existe
> Cada VM va a tener **dos tarjetas de red**, igual que un portátil con wifi y cable a la vez:
>
> | Tarjeta | Modo en VirtualBox | Para qué | Analogía |
> | :--- | :--- | :--- | :--- |
> | **Adaptador 1** | **NAT** | Salir a Internet (actualizaciones, descargas) | El router de casa: sales, pero nadie de fuera entra |
> | **Adaptador 2** | **Red interna** `LAB_RED` | Que las dos VM se vean entre ellas | Un cable de red entre las dos máquinas, sin nada más enchufado |
>
> La **red interna** es lo más parecido a coger un cable y conectar dos equipos: solo están ellas dos. **Tu ordenador (el anfitrión) no forma parte de esa red**, así que desde él no harás ping a las VM. No es un fallo: es el diseño.
>
> El plan de direcciones, el mismo que usará el Bloque 2:
>
> | Máquina | Papel | IP en `LAB_RED` |
> | :--- | :--- | :--- |
> | Ubuntu Server | Servidor | `10.10.10.10/24` |
> | Windows 11 Pro | Cliente | `10.10.10.20/24` |

> [!warning] El fallo nº1: el cortafuegos de Windows
> Vas a ver una cosa que parece un misterio: **desde Windows el ping a Ubuntu funciona, pero desde Ubuntu a Windows no.** La red está bien. Lo que pasa es que el **Firewall de Windows bloquea por defecto el ping que le llega** (aunque deja salir el suyo y recibir la respuesta). Ubuntu Server, en cambio, trae su cortafuegos (`ufw`) **desactivado** de serie. Te lo digo ahora para que, cuando pase, sepas que es esto y no la red.

> [!tip] Las dos VM tienen la misma IP de NAT, y no pasa nada
> En el adaptador NAT, VirtualBox suele dar a **todas** las VM la dirección `10.0.2.15`. No chocan: **cada VM tiene su propio NAT privado**, aislado de los demás. Por eso, precisamente, el NAT **no sirve** para que las VM se vean entre ellas, y necesitas el adaptador 2.

> [!example] Vocabulario de esta práctica
> - **Red interna (VirtualBox):** red privada solo entre las VM que estén conectadas a ella con **el mismo nombre**. El anfitrión no participa.
> - **Netplan:** el sistema que configura la red en Ubuntu Server, a partir de ficheros YAML en `/etc/netplan/`.
> - **`/24`:** la máscara `255.255.255.0`. Todas las IP `10.10.10.x` están en la misma red.
> - **ICMP / ping:** el mensaje «¿estás ahí?» y su respuesta. Es la prueba de conectividad más básica.
> - **Regla de entrada (firewall):** permiso que deja pasar un tipo de tráfico que **llega** al equipo.

> [!example] Los comandos nuevos
> | Dónde | Comando | Para qué |
> | :--- | :--- | :--- |
> | Ubuntu | `ip -br a` | Ver las tarjetas, su estado y su IP en una línea cada una |
> | Ubuntu | `ip link` | Ver la dirección MAC de cada tarjeta |
> | Ubuntu | `sudo netplan try` | Probar la configuración nueva; si no confirmas en 120 s, vuelve atrás sola |
> | Ubuntu | `ping -c 4 <IP>` | Cuatro pings y para |
> | Windows | `ipconfig` · `Get-NetAdapter` | Ver las tarjetas, su IP y su MAC |
> | Windows | `New-NetIPAddress` | Poner una IP fija desde PowerShell |
> | Windows | `New-NetFirewallRule` | Crear una regla en el cortafuegos |

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-14-red-virtualbox-windows-11-y-ubuntu-server.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura del **Bloque 0 · Fase 0.1.b** y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.14 · Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server)`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `🔗 Enlaces`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

> [!tip] Las instalaciones también se graban
> La práctica se graba **entera**, instalaciones incluidas. Para que quien corrige no tenga que ver media hora de barras de progreso, pon un **timestamp al empezar y otro al acabar cada instalación**. Lo que de verdad se evalúa son los pasos de red: que se vean bien.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio entero, ten a mano las ISO de **Ubuntu Server 26.04 LTS** y **Windows 11** (verificadas, B1.4) y comprueba que la virtualización está activa (B1.9). Arranca OBS y preséntate.

> [!example] Paso 1 — Crea la VM del servidor: Ubuntu Server
> Crea la VM `B1-UbuntuServer` como ya sabes (B1.9 y B1.10): **2 CPU, 2048 MB de RAM, disco de 25 GB**, con la ISO de Ubuntu Server 26.04. Si el asistente te ofrece la instalación desatendida, **desactívala**: la instalación la haces tú.
>
> **Antes de arrancarla**, ve a **Configuración → Red**:
> - **Adaptador 1:** déjalo como está → **NAT**.
> - **Adaptador 2:** marca **Habilitar adaptador de red** → **Conectado a: Red interna** → **Nombre:** escribe `LAB_RED`.
>
> **Por qué escribes el nombre a mano y con cuidado:** dos VM solo están en la misma red interna si el nombre es **exactamente el mismo**. `LAB_RED` y `lab_red` son dos redes distintas, y no te avisará nadie.
>
> Despliega **Avanzadas** en el adaptador 2 y **apunta su dirección MAC**. Te servirá para reconocer la tarjeta dentro de Ubuntu.

> [!example] Paso 2 — Instala Ubuntu Server
> Instálalo con las opciones por defecto. En la pantalla de red verás dos tarjetas:
> - Una (`enp0s3`, la del NAT) recibe una IP `10.0.2.15` sola.
> - La otra (`enp0s8`, la de `LAB_RED`) aparece **sin dirección**, porque en esa red no hay nadie que reparta IP.
>
> **Déjala así.** La configuras después, y a mano: es lo que quieres aprender.

> [!example] Paso 3 — Identifica la tarjeta del laboratorio
> Entra en el servidor y ejecuta:
> ```bash
> ip -br a
> ip link
> ```
> Con `ip -br a` ves las tarjetas: una con `10.0.2.15` y otra **sin IP**. Con `ip link` compruebas que la MAC de esa tarjeta sin IP coincide con la que apuntaste en el Paso 1. **Esa es la tuya.** Lo normal es que se llame `enp0s8`. Si se llama de otra forma, usa su nombre en el paso siguiente.

> [!example] Paso 4 — Dale IP fija con netplan
> Crea un fichero **nuevo**, solo para el laboratorio:
> ```bash
> sudo nano /etc/netplan/60-laboratorio.yaml
> ```
> Escribe esto, **con espacios y nunca con tabuladores**:
> ```yaml
> network:
>   version: 2
>   ethernets:
>     enp0s8:
>       addresses:
>         - 10.10.10.10/24
> ```
> **Por qué un fichero nuevo y no editar el que ya hay** (`50-cloud-init.yaml`): ese lo generó el instalador y lo puede regenerar. El tuyo no lo toca nadie. Netplan junta todos los ficheros de la carpeta, así que los dos conviven.
>
> **Por qué no pones puerta de enlace (`gateway`, `routes`):** la salida a Internet ya la da el NAT. Si le pones otra puerta de enlace a esta tarjeta, el servidor no sabrá por dónde salir y **perderás Internet**.
>
> Protege el fichero y prueba la configuración:
> ```bash
> sudo chmod 600 /etc/netplan/60-laboratorio.yaml
> sudo netplan try
> ```
> **Por qué `chmod 600`:** netplan avisa si el fichero lo puede leer cualquiera, porque estos ficheros a veces guardan contraseñas de wifi. **Por qué `try` y no `apply`:** si te equivocas y te quedas sin red, `try` deshace el cambio solo a los 120 segundos. Si todo va bien, pulsa **Intro** para confirmarlo.
>
> Comprueba:
> ```bash
> ip -br a
> ```
> La tarjeta `enp0s8` tiene que aparecer **UP** con `10.10.10.10/24`.

> [!example] Paso 5 — Crea la VM del cliente: Windows 11 Pro
> Crea la VM `B1-Win11`: **2 CPU, 4096 MB de RAM, disco de 64 GB**, con la ISO de Windows 11. Elige el tipo **Windows 11 (64-bit)**. VirtualBox activa así el arranque EFI, el arranque seguro y el **TPM 2.0** que pide Windows 11. Sin ellos, el instalador dice que el equipo «no cumple los requisitos».
>
> En **Configuración → Red**, **igual que en el servidor**:
> - **Adaptador 1:** **NAT**.
> - **Adaptador 2:** **Red interna** → `LAB_RED`, el mismo nombre, letra a letra.
>
> Si el asistente te ofrece la instalación desatendida, **desactívala**, igual que con el servidor. Instala **Windows 11 Pro**: crear e instalar una VM ya lo sabes hacer. Aquí lo que importa es la red.

> [!example] Paso 6 — Identifica la tarjeta del laboratorio en Windows
> Abre **PowerShell como administrador** y ejecuta:
> ```powershell
> Get-NetAdapter
> ipconfig
> ```
> Verás dos tarjetas, normalmente `Ethernet` y `Ethernet 2`:
> - La del **NAT** tiene `10.0.2.15`.
> - La de **`LAB_RED`** tiene una IP rara que empieza por **`169.254`**. Esa es una dirección que Windows se pone a sí mismo cuando **no encuentra a nadie que le dé IP**. Por eso la reconoces enseguida.
>
> Confírmalo con la MAC: la de `Get-NetAdapter` tiene que coincidir con la del adaptador 2 en VirtualBox. Allí sale sin guiones (`080027…`) y en Windows con guiones (`08-00-27-…`).

> [!example] Paso 7 — Dale IP fija a Windows
> Con el nombre que te haya salido (aquí `Ethernet 2`):
> ```powershell
> New-NetIPAddress -InterfaceAlias "Ethernet 2" -IPAddress 10.10.10.20 -PrefixLength 24
> ```
> Sin `-DefaultGateway`, **por la misma razón que en Ubuntu**: Internet ya sale por el NAT.
>
> *Si lo prefieres con ratón:* `Win + R` → `ncpa.cpl` → clic derecho en `Ethernet 2` → **Propiedades** → **Protocolo de Internet versión 4 (TCP/IPv4)** → **Usar la siguiente dirección IP**. Dirección `10.10.10.20`, máscara `255.255.255.0`, puerta de enlace **vacía**.
>
> Si Windows te pregunta si quieres que el equipo sea visible en la red, contesta **No**. La red queda como **pública**, y eso es justo lo que hace que el siguiente paso falle.

> [!example] Paso 8 — El ping: primero el que funciona, luego el que falla
> **Desde Windows hacia el servidor:**
> ```powershell
> ping 10.10.10.10
> ```
> ✅ Responde. **Desde el servidor hacia Windows:**
> ```bash
> ping -c 4 10.10.10.20
> ```
> ❌ **100 % de paquetes perdidos.** Graba este momento. La red está bien, porque el primer ping ha ido. Lo que bloquea es el **Firewall de Windows**, que no contesta al ping que le llega de fuera.

> [!example] Paso 9 — Abre el ping en el firewall de Windows
> En PowerShell como administrador:
> ```powershell
> New-NetFirewallRule -DisplayName "LAB - Ping entrante (ICMPv4)" -Direction Inbound -Protocol ICMPv4 -IcmpType 8 -Action Allow
> ```
> **Qué hace cada parte:**
> - `-Direction Inbound`: tráfico que **entra**.
> - `-Protocol ICMPv4 -IcmpType 8`: solo la **petición de eco**, es decir, el ping. Nada más.
> - `-Action Allow`: déjalo pasar.
>
> **Abres exactamente el ping, no apagas el firewall.** Apagarlo «para que funcione» es lo que hace la gente que luego tiene problemas. Te lo digo claro: **no lo apagues nunca**.
>
> Vuelve al servidor y repite:
> ```bash
> ping -c 4 10.10.10.20
> ```
> ✅ **0 % de paquetes perdidos.**

> [!example] Paso 10 — Guarda el estado y cierra la grabación
> Apaga las dos VM y haz una **instantánea** de cada una con el nombre `B1.14 · Red OK`, como aprendiste en B1.9. **El servidor lo vas a reutilizar en B1.14b.**
>
> Detén OBS, nombra el vídeo **`B1.14 · Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server)`**, súbelo a **`B1_Entorno`** y añade los timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Nombre de red interna distinto en cada VM (`LAB_RED` / `lab_red` / `LAB RED`) | Cada VM está en su propia red: no hay ping en ningún sentido | Copia el nombre letra a letra en las dos VM |
> | Adaptador 2 sin habilitar, o sin la casilla **Cable conectado** en *Avanzadas* | La tarjeta sale `DOWN` o `NO-CARRIER` en `ip -br a` | Revisa los dos detalles en Configuración → Red |
> | Tabuladores o sangría mal hecha en el YAML | `netplan try` da error de sintaxis y no aplica nada | Solo espacios, dos por nivel, alineados como en el ejemplo |
> | IP puesta en la tarjeta del NAT (`enp0s3` / `Ethernet`) en lugar de la del laboratorio | Te quedas sin Internet y el ping sigue sin ir | Identifica la tarjeta por la MAC antes de tocar nada |
> | Poner puerta de enlace en la tarjeta del laboratorio | La VM pierde Internet: tiene dos salidas y elige la que no lleva a ningún sitio | La tarjeta de `LAB_RED` no lleva puerta de enlace |
> | Apagar el Firewall de Windows en vez de crear la regla | Funciona, pero has dejado el equipo abierto a todo | Regla de entrada solo para ICMPv4 tipo 8 |
> | Intentar hacer ping desde tu ordenador a `10.10.10.10` | No responde | Es lo esperado: el anfitrión no está en una red interna |
> | VirtualBox muy lento y una **tortuga verde** abajo a la derecha de la VM | Hyper-V está activado en el equipo y VirtualBox funciona por encima de él | No es un fallo de la práctica: funciona igual, solo más lento. Coméntalo con el profesor si molesta |

> [!success] ✅ Verificación: ¿está bien hecho?
> - En el servidor, `ip -br a` muestra `enp0s8` **UP** con `10.10.10.10/24`.
> - En Windows, `ipconfig` muestra `10.10.10.20` en la tarjeta del laboratorio, **sin puerta de enlace** en ella.
> - `ping 10.10.10.10` desde Windows: **0 % perdidos**.
> - `ping -c 4 10.10.10.20` desde el servidor: **0 % perdidos**.
> - **Internet sigue funcionando en las dos:** en el servidor `sudo apt update` descarga sin errores; en Windows abre cualquier web.
> - Las dos VM tienen la instantánea `B1.14 · Red OK`.

> [!question] Comprueba que lo has entendido
> 1. Explica **con tus palabras** por qué el ping de Windows a Ubuntu funcionaba desde el principio y el de Ubuntu a Windows no.
> 2. Las dos VM tenían la IP `10.0.2.15` en el NAT y no ha habido conflicto. ¿Por qué? ¿Y por qué eso mismo impide usar el NAT para que se vean entre ellas?
> 3. Si en el servidor hubieras puesto la IP en `enp0s3` en lugar de en `enp0s8`, ¿qué dos cosas habrían dejado de funcionar?
> 4. Pon un ejemplo **tuyo, del mundo real**, de algo que se parezca a una red interna de VirtualBox.

---

## ✅ Entregables y cierre

- **Entregable:** VM `B1-UbuntuServer` y VM `B1-Win11` en `LAB_RED`, con ping en los dos sentidos y la instantánea `B1.14 · Red OK` (evidenciado en el vídeo).
- **Entregable vídeo:** `B1.14 · Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server)` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** ping en los dos sentidos con **0 % de pérdida**, Internet funcionando en las dos VM y **el firewall de Windows encendido**.
- **Entregable apuntes:** `b1-14-red-virtualbox-windows-11-y-ubuntu-server.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A conectar dos VM con una **red interna**: el «cable» que solo existe dentro de VirtualBox.
> - A poner una **IP fija** en Ubuntu Server con **netplan** y en Windows con **PowerShell**.
> - Que cuando un ping falla en un sentido y no en el otro, el culpable casi siempre es un **cortafuegos**, no la red. Y a abrir **solo** lo necesario.
>
> **Siguiente:** B1.14b — El mismo servidor, ahora con un cliente **Ubuntu Desktop**.
