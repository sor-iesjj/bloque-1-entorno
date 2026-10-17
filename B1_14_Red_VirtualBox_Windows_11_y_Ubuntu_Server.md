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
> La **red interna** es lo más parecido a coger un cable y conectar dos equipos: solo están las VM que conectes a ella. **Tu ordenador (el anfitrión) no forma parte de esa red**, así que desde él no harás ping a las VM. No es un fallo: es el diseño.
>
> Y en esa red **no hay nadie que reparta direcciones** (no hay servidor DHCP). Por eso cada máquina tendrá que llevar su IP puesta a mano.
>
> El plan de direcciones, el mismo que usará el Bloque 2:
>
> | Máquina | Papel | IP en `LAB_RED` |
> | :--- | :--- | :--- |
> | Ubuntu Server | Servidor | `10.10.10.10/24` |
> | Windows 11 Pro | Cliente | `10.10.10.20/24` |

> [!warning] El fallo nº1: el cortafuegos de Windows
> Vas a ver una cosa que parece un misterio: **desde Windows el ping a Ubuntu funciona, pero desde Ubuntu a Windows no.** La red está bien. Lo que pasa es que el **Firewall de Windows bloquea todo lo que le llega sin haberlo pedido, salvo que una regla lo permita**. Cuando Windows hace ping, la respuesta sí entra, porque la pidió él. Cuando el ping lo empieza Ubuntu, a Windows le llega una petición que nadie pidió, y la tira.
>
> Ubuntu Server, en cambio, trae su cortafuegos (`ufw`) **desactivado** de serie. Te lo digo ahora para que, cuando pase, sepas que es el firewall y no la red.

> [!tip] Las dos VM tienen la misma IP de NAT, y no pasa nada
> En el adaptador NAT, VirtualBox da a cada VM la dirección `10.0.2.15`. No chocan: **cada VM tiene su propio NAT privado**, como si cada una tuviera su router para ella sola. Por eso, precisamente, el NAT **no sirve** para que las VM se vean entre ellas, y necesitas el adaptador 2.

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
> | Ubuntu | `ls /etc/netplan/` · `sudo cat /etc/netplan/*.yaml` | Ver qué ficheros de red hay y qué dicen |
> | Ubuntu | `sudo netplan try` | Probar la configuración nueva; si no confirmas en 120 s, vuelve atrás sola |
> | Ubuntu | `ping -c 4 <IP>` | Cuatro pings y para |
> | Windows | `Get-NetAdapter` · `ipconfig` | Ver las tarjetas, su MAC y su IP |
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

> [!tip] Timestamps mínimos de esta práctica
> La práctica se graba **entera**, instalaciones incluidas. Para que quien corrige encuentre cada cosa sin ver media hora de barras de progreso, el vídeo lleva **como mínimo** estas marcas (una por paso, más el principio y el final de cada instalación):
> ```
> 00:00 Presentación
> Paso 1 · VM Ubuntu Server y sus dos adaptadores
> Paso 2 · Instalación de Ubuntu Server (inicio)
> Paso 2 · Instalación de Ubuntu Server (fin)
> Paso 3 · Identificar la tarjeta del laboratorio
> Paso 4 · IP fija con netplan
> Paso 5 · VM Windows 11 y sus dos adaptadores
> Paso 5 · Instalación de Windows 11 (inicio)
> Paso 5 · Instalación de Windows 11 (fin)
> Paso 6 · Identificar la tarjeta en Windows
> Paso 7 · IP fija en Windows
> Paso 8 · Ping: el que va y el que no
> Paso 9 · Regla de firewall y ping de vuelta
> Paso 10 · Instantáneas y cierre
> ```
> Cada marca lleva delante **el minuto real** en el que empieza eso en tu vídeo.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio entero, ten a mano las ISO de **Ubuntu Server 26.04 LTS** y **Windows 11** (verificadas, B1.4) y comprueba que la virtualización está activa (B1.9). Crea la entrada de apuntes vacía. Arranca OBS y preséntate.

> [!example] Paso 1 — Crea la VM del servidor: Ubuntu Server
> Crea la VM `B1-UbuntuServer` como ya sabes (B1.9 y B1.10): tipo **Linux · Ubuntu (64-bit)**, **2 CPU, 2048 MB de RAM, disco de 25 GB**, con la ISO de Ubuntu Server 26.04.
>
> **Desactiva la instalación desatendida.** El asistente de VirtualBox la activa por defecto cuando le das una ISO que la admite. Según tu versión, la casilla dice que **te saltes** la instalación desatendida (márcala) o que **instales con** instalación desatendida (desmárcala). El resultado tiene que ser el mismo: la instalación la haces tú.
>
> **Antes de arrancarla**, ve a **Configuración → Red**:
> - **Adaptador 1:** déjalo como está → **NAT**.
> - **Adaptador 2:** marca **Habilitar adaptador de red** → **Conectado a: Red interna** → **Nombre:** escribe `LAB_RED`.
>
> **Por qué escribes el nombre a mano y con cuidado:** dos VM solo están en la misma red interna si el nombre es **exactamente el mismo**. `LAB_RED` y `lab_red` son dos redes distintas, y no te avisará nadie.
>
> Despliega **Avanzadas** en el adaptador 2, comprueba que **Cable conectado** está marcado y **apunta su dirección MAC**. Te servirá para reconocer la tarjeta dentro de Ubuntu.

> [!example] Paso 2 — Instala Ubuntu Server
> Instálalo con las opciones por defecto. En la pantalla de red verás dos tarjetas:
> - Una (la del NAT) recibe sola una IP `10.0.2.15`.
> - La otra (la de `LAB_RED`) se queda **sin dirección**: el instalador intenta pedir una por DHCP y en esa red no contesta nadie.
>
> **Déjala así.** La configuras después, y a mano: es lo que quieres aprender.
>
> Puede que el primer arranque del sistema instalado tarde un poco más de lo normal en la red: Ubuntu espera un rato a esa tarjeta que pide IP y no la consigue. En el Paso 4 lo arreglas.

> [!example] Paso 3 — Identifica la tarjeta del laboratorio
> Entra en el servidor y ejecuta:
> ```bash
> ip -br a
> ip link
> ```
> Con `ip -br a` ves las tarjetas: una con `10.0.2.15` y otra **sin IPv4**. Con `ip link` compruebas que la MAC de esa tarjeta sin IP coincide con la que apuntaste en el Paso 1. Ojo al formato: VirtualBox la enseña seguida (`080027…`) y Linux con dos puntos (`08:00:27:…`). **Esa es la tuya.**
>
> Lo normal es que se llame `enp0s8`, y así aparece en el resto de la práctica. **Si a ti te sale otro nombre, usa el tuyo en todos los comandos.** No copies un nombre de tarjeta de un tutorial: se mira.

> [!example] Paso 4 — Dale IP fija con netplan
> **Primero, mira lo que dejó el instalador:**
> ```bash
> ls /etc/netplan/
> sudo cat /etc/netplan/*.yaml
> ```
> Verás un fichero que escribió el instalador. Su nombre depende de la versión y de cómo se instaló (por ejemplo `00-installer-config.yaml` o `50-cloud-init.yaml`). **Fíjate en si aparece tu tarjeta del laboratorio con `dhcp4: true`.** Lo normal es que sí: el instalador la dejó pidiendo IP por DHCP, aunque nadie le contestara.
>
> **Ahora crea un fichero nuevo**, solo para el laboratorio:
> ```bash
> sudo nano /etc/netplan/60-laboratorio.yaml
> ```
> Escribe esto, **con espacios y nunca con tabuladores**:
> ```yaml
> network:
>   version: 2
>   ethernets:
>     enp0s8:
>       dhcp4: false
>       addresses:
>         - 10.10.10.10/24
> ```
> **Por qué un fichero nuevo y no editar el del instalador:** netplan lee **todos** los ficheros de `/etc/netplan/` en orden alfabético, y **lo que dice un fichero posterior pisa lo que decía uno anterior** para la misma opción. Tu `60-…` va detrás del `00-…` y del `50-…`, así que manda él. Y tu cambio queda entero en un fichero tuyo: si algo va mal, sabes exactamente qué tocaste.
>
> **Por qué `dhcp4: false`:** si el fichero del instalador dice `dhcp4: true` para esta tarjeta y tú no lo desmientes, la tarjeta seguiría pidiendo IP por DHCP a una red donde nadie reparte, y el arranque seguiría esperándola. Con `false` en tu fichero, el valor del instalador queda pisado.
>
> **Por qué no pones puerta de enlace (`gateway`, `routes`):** la salida a Internet ya la da el NAT. Si le pones otra puerta de enlace a esta tarjeta, el servidor tiene dos caminos para salir a Internet y uno no lleva a ningún sitio: **puedes perder Internet**.
>
> Protege el fichero y prueba la configuración:
> ```bash
> sudo chmod 600 /etc/netplan/60-laboratorio.yaml
> sudo netplan try
> ```
> **Por qué `chmod 600`:** netplan recomienda que sus ficheros solo los pueda leer `root`, porque a veces guardan contraseñas de wifi o claves de VPN. Si lo dejas abierto, te lo recordará con un aviso cada vez.
>
> **Por qué `try` y no `apply`:** `try` aplica la configuración y te pide que pulses **Intro** para confirmarla. Si no la confirmas en **120 segundos** (por ejemplo, porque te has quedado sin red), la deshace sola. Si todo va bien, pulsa **Intro**.
>
> Comprueba:
> ```bash
> ip -br a
> ```
> La tarjeta `enp0s8` tiene que aparecer **UP** con `10.10.10.10/24`.

> [!example] Paso 5 — Crea la VM del cliente: Windows 11 Pro
> Crea la VM `B1-Win11` y elige el tipo **Windows 11 (64-bit)**. Con ese tipo, VirtualBox deja preparados el arranque **EFI**, el **arranque seguro** y un **TPM 2.0**, que es lo que exige Windows 11. Si eliges otro tipo, el instalador dirá que el equipo «no cumple los requisitos».
>
> Recursos: **2 CPU** (Windows 11 pide 2 núcleos como mínimo), **4096 MB de RAM** y **disco de 64 GB** (el mínimo que pide Windows 11; si VirtualBox te propone más, puedes dejarlo).
>
> **Desactiva la instalación desatendida**, igual que con el servidor.
>
> En **Configuración → Red**, **igual que en el servidor**:
> - **Adaptador 1:** **NAT**.
> - **Adaptador 2:** **Red interna** → `LAB_RED`, el mismo nombre, letra a letra. Comprueba **Cable conectado** y apunta su **MAC**.
>
> Instala **Windows 11 Pro**: crear e instalar una VM ya lo sabes hacer. Aquí lo que importa es la red.

> [!warning] La configuración inicial de Windows 11 Pro te va a pedir Internet y una cuenta
> Al terminar de instalar, Windows 11 Pro pide conexión a Internet y, para uso personal, una **cuenta Microsoft**. Internet ya lo tienes: es el adaptador NAT.
>
> **No metas tu cuenta personal en una VM de prácticas.** En Windows 11 Pro suele haber un camino para crear una **cuenta local**: elegir que el equipo es **para el trabajo o el centro educativo**, entrar en las **opciones de inicio de sesión** y escoger **unirse a un dominio en su lugar**. Eso no une nada a ningún dominio: solo te deja crear un usuario local con contraseña.
>
> **Si en tu versión no aparece ese camino, para y avisa al profesor.** No te quedes atascado buscando trucos por internet: Microsoft los va quitando de una versión a otra.

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
> Confírmalo con la MAC: la que enseña `Get-NetAdapter` tiene que coincidir con la del adaptador 2 en VirtualBox. Allí sale seguida (`080027…`) y en Windows con guiones (`08-00-27-…`).

> [!example] Paso 7 — Dale IP fija a Windows
> Con el nombre que te haya salido a ti (aquí `Ethernet 2`):
> ```powershell
> New-NetIPAddress -InterfaceAlias "Ethernet 2" -IPAddress 10.10.10.20 -PrefixLength 24
> ```
> **Qué hace:** pone la dirección `10.10.10.20` con máscara `/24` en esa tarjeta. Como la tarjeta estaba en DHCP, al ponerle una IP a mano Windows **le quita el DHCP solo**, y la `169.254…` desaparece.
>
> Sin `-DefaultGateway`, **por la misma razón que en Ubuntu**: Internet ya sale por el NAT.
>
> *Si lo prefieres con ratón:* `Win + R` → `ncpa.cpl` → clic derecho en la tarjeta del laboratorio → **Propiedades** → **Protocolo de Internet versión 4 (TCP/IPv4)** → **Propiedades** → usar una dirección IP fija: dirección `10.10.10.20`, máscara `255.255.255.0`, puerta de enlace **vacía**.
>
> Si Windows te pregunta si quieres que el equipo sea visible para otros de la red, contesta **No**. La red se queda como **pública**, el perfil más estricto. No importa para lo que viene: la regla que crearás en el Paso 9 vale para cualquier perfil.

> [!example] Paso 8 — El ping: primero el que funciona, luego el que falla
> **Desde Windows hacia el servidor:**
> ```powershell
> ping 10.10.10.10
> ```
> ✅ Responde. **Desde el servidor hacia Windows:**
> ```bash
> ping -c 4 10.10.10.20
> ```
> ❌ Lo normal es **100 % de paquetes perdidos.** Graba este momento. La red está bien, porque el primer ping ha ido. Lo que bloquea es el **Firewall de Windows**, que no contesta al ping que le llega sin haberlo pedido.
>
> *Si en tu equipo este ping ya funciona*, no te lo inventes: dilo en el vídeo y apúntalo. Significa que alguna regla de fábrica ya deja pasar el ping en el perfil de red que tienes. Crea igualmente tu regla en el paso siguiente.

> [!example] Paso 9 — Abre el ping en el firewall de Windows
> En PowerShell como administrador:
> ```powershell
> New-NetFirewallRule -DisplayName "LAB - Ping entrante (ICMPv4)" -Direction Inbound -Protocol ICMPv4 -IcmpType 8 -Action Allow
> ```
> **Qué hace cada parte:**
> - `-DisplayName`: el nombre con el que la verás en la lista de reglas.
> - `-Direction Inbound`: tráfico que **entra**.
> - `-Protocol ICMPv4 -IcmpType 8`: solo la **petición de eco**, es decir, el ping. Nada más.
> - `-Action Allow`: déjalo pasar.
>
> Como no le dices perfil, la regla vale para **todos** (dominio, privado y público), y nace **activada**.
>
> **Abres exactamente el ping, no apagas el firewall.** Apagarlo «para que funcione» es lo que hace la gente que luego tiene problemas. La propia Microsoft recomienda no desactivarlo. Te lo digo claro: **no lo apagues nunca**.
>
> Vuelve al servidor y repite:
> ```bash
> ping -c 4 10.10.10.20
> ```
> ✅ **0 % de paquetes perdidos.**

> [!example] Paso 10 — Guarda el estado y cierra la grabación
> Antes de guardar, comprueba que tu IP del servidor **sobrevive a un reinicio**:
> ```bash
> sudo reboot
> ```
> Al volver, `ip -br a` tiene que seguir enseñando `enp0s8` **UP** con `10.10.10.10/24`.
>
> Apaga las dos VM y haz una **instantánea** de cada una con el nombre `B1.14 · Red OK`, como aprendiste en B1.9. **El servidor lo vas a reutilizar en B1.14b.**
>
> Detén OBS, nombra el vídeo **`B1.14 · Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server)`**, súbelo a **`B1_Entorno`** (No listado) y añade los timestamps. Pega su enlace en tu entrada de apuntes.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Nombre de red interna distinto en cada VM (`LAB_RED` / `lab_red` / `LAB RED`) | Cada VM está en su propia red: no hay ping en ningún sentido | Copia el nombre letra a letra en las dos VM |
> | Adaptador 2 sin habilitar, o sin la casilla **Cable conectado** en *Avanzadas* | La tarjeta sale `DOWN` o `NO-CARRIER` en `ip -br a` | Revisa los dos detalles en Configuración → Red |
> | Tabuladores o sangría mal hecha en el YAML | `netplan try` da error y no aplica nada | Solo espacios, dos por nivel, alineados como en el ejemplo |
> | Copiar `enp0s8` sin mirar el nombre real de tu tarjeta | netplan configura una tarjeta que no existe y la tuya sigue sin IP | Identifica la tarjeta por la MAC (Paso 3) y usa su nombre |
> | Olvidar `dhcp4: false` | La IP fija sale, pero la tarjeta sigue pidiendo DHCP y el arranque espera por ella | Pon `dhcp4: false` en tu fichero `60-laboratorio.yaml` |
> | Dejar el fichero con permisos abiertos | netplan avisa de que la configuración es demasiado accesible | `sudo chmod 600 /etc/netplan/60-laboratorio.yaml` |
> | IP puesta en la tarjeta del NAT (`enp0s3` / `Ethernet`) en lugar de la del laboratorio | Te quedas sin Internet y el ping sigue sin ir | Identifica la tarjeta por la MAC antes de tocar nada |
> | Poner puerta de enlace en la tarjeta del laboratorio | La VM puede perder Internet: tiene dos salidas y una no lleva a ningún sitio | La tarjeta de `LAB_RED` no lleva puerta de enlace |
> | Repetir `New-NetIPAddress` sobre la misma tarjeta | Error de que esa dirección **ya existe** | No pasa nada: la IP ya estaba puesta. Compruébalo con `ipconfig` |
> | Apagar el Firewall de Windows en vez de crear la regla | Funciona, pero has dejado el equipo abierto a todo | Regla de entrada solo para ICMPv4 tipo 8 |
> | Intentar hacer ping desde tu ordenador a `10.10.10.10` | No responde | Es lo esperado: el anfitrión no está en una red interna |
> | VirtualBox muy lento y una **tortuga verde** abajo a la derecha de la ventana de la VM | Hyper-V está activado en el equipo y VirtualBox funciona por encima de él | No es un fallo de la práctica: funciona igual, solo más lento. Coméntalo con el profesor si molesta |

> [!success] ✅ Verificación: ¿está bien hecho?
> - En el servidor, `ip -br a` muestra `enp0s8` **UP** con `10.10.10.10/24`, **también después de reiniciar**.
> - En Windows, `ipconfig` muestra `10.10.10.20` en la tarjeta del laboratorio, **sin puerta de enlace** en ella.
> - `ping 10.10.10.10` desde Windows: **0 % perdidos**.
> - `ping -c 4 10.10.10.20` desde el servidor: **0 % perdidos**.
> - **Internet sigue funcionando en las dos:** en el servidor `sudo apt update` descarga sin errores; en Windows abre cualquier web.
> - El **firewall de Windows sigue activado**.
> - Las dos VM tienen la instantánea `B1.14 · Red OK`.

> [!question] Comprueba que lo has entendido
> 1. Explica **con tus palabras** por qué el ping de Windows a Ubuntu funcionaba desde el principio y el de Ubuntu a Windows no.
> 2. Las dos VM tenían la IP `10.0.2.15` en el NAT y no ha habido conflicto. ¿Por qué? ¿Y por qué eso mismo impide usar el NAT para que se vean entre ellas?
> 3. Si en el servidor hubieras puesto la IP en `enp0s3` en lugar de en `enp0s8`, ¿qué dos cosas habrían dejado de funcionar?
> 4. Tu fichero `60-laboratorio.yaml` dice `dhcp4: false` y el del instalador dice `dhcp4: true` para la misma tarjeta. ¿Cuál gana y por qué?
> 5. Pon un ejemplo **tuyo, del mundo real**, de algo que se parezca a una red interna de VirtualBox.

---

## ✅ Entregables y cierre

- **Entregable:** VM `B1-UbuntuServer` y VM `B1-Win11` en `LAB_RED`, con ping en los dos sentidos y la instantánea `B1.14 · Red OK` (evidenciado en el vídeo).
- **Entregable vídeo:** `B1.14 · Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server)` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** ping en los dos sentidos con **0 % de pérdida**, IP del servidor que sobrevive a un reinicio, Internet funcionando en las dos VM y **el firewall de Windows encendido**.
- **Entregable apuntes:** `b1-14-red-virtualbox-windows-11-y-ubuntu-server.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A conectar dos VM con una **red interna**: el «cable» que solo existe dentro de VirtualBox.
> - A poner una **IP fija** en Ubuntu Server con **netplan** (y por qué tu fichero pisa al del instalador) y en Windows con **PowerShell**.
> - Que cuando un ping falla en un sentido y no en el otro, el culpable casi siempre es un **cortafuegos**, no la red. Y a abrir **solo** lo necesario.
>
> **Siguiente:** B1.14b — El mismo servidor, ahora con un cliente **Ubuntu Desktop**.
