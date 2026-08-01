---
Práctica: B1.9b
Bloque: 01_Entorno
Nivel: 2
Nivel_nombre: Intermedio
RA: RA1, RA5
CE: 1.b, 1.i, 5.a
Playlist: B1_Entorno
Vídeo: B1.9b · Verificar tu red con APIs públicas
---

## B1.9b — Verificar tu red con APIs públicas

> [!abstract] Ficha de la práctica
> ### 📌 `B1.9b` — Verificar tu red con APIs públicas
> - **Bloque 1** (Entorno) · **Nivel 2** (Intermedio) · **RA1, RA5** · **CE 1.b, 1.i, 5.a**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.9b · Verificar tu red con APIs públicas`
> - **⏱️ Tiempo estimado:** ~45 min · **Requisitos:** la B1.9 hecha (laboratorio de virtualización con NAT y Host-Only)

> [!info] Caso real
> Acabas de montar el laboratorio de la B1.9: una máquina virtual con dos tarjetas de red, una en NAT y otra en Solo-Anfitrión. Funciona… **eso crees**. Porque hasta ahora lo único que has hecho es mirar la ventana de configuración de VirtualBox y confiar en que dice la verdad.
>
> Un técnico no confía: **comprueba**. Y no comprueba desde dentro de su propia máquina, porque su propia máquina puede estar mintiéndole. Comprueba **desde fuera**.

- **🎯 Objetivo real:** verificar, con fuentes externas e independientes, que tu red está como tú crees que está.
- **🧩 Problema que resuelve:** el `ipconfig` te dice lo que tu equipo cree de sí mismo. No te dice **qué ve Internet de ti**, ni si tu cálculo de subred es correcto. Para eso hace falta alguien de fuera.

---

## 📚 Fundamento

> [!info] Qué es una API (y por qué te importa a ti, que vas a administrar servidores)
> Una **API** (*Application Programming Interface*) es **una web pensada para que la consulte un programa en vez de una persona**. Nada más. Y nada menos.
>
> Cuando abres `elpais.com` recibes una página con colores, menús y anuncios: está hecha para tus ojos. Cuando consultas una API recibes **datos limpios**, normalmente en formato **JSON**, sin adornos: está hecha para que la lea otro programa.
>
> | | Web normal | API |
> | :--- | :--- | :--- |
> | Para quién | Una persona con un navegador | Un programa, un script |
> | Qué devuelve | HTML: colores, botones, publicidad | **JSON**: solo los datos |
> | Cómo se consulta | Haciendo clic | Con una **URL** y un comando |

> [!important] Por qué esto es de SOR y no de programación
> Podrías pensar que las APIs son cosa de programadores. **No.** Un administrador de sistemas las usa todos los días, y casi siempre para lo mismo: **comprobar desde fuera algo que desde dentro no puede ver**.
>
> - ¿Mi servidor se ve desde Internet? Se lo preguntas a un servicio externo.
> - ¿Con qué IP pública sale mi red? Tu equipo no lo sabe: hay que preguntárselo a alguien de fuera.
> - ¿El certificado de mi web caduca pronto? Lo consultas a un verificador externo.
>
> **La idea de fondo, y es la que quiero que te lleves: una comprobación hecha desde el propio equipo que estás comprobando no vale gran cosa.** Es como preguntarle a alguien si dice la verdad.

> [!abstract] La herramienta: `curl`
> Ya la conoces del `curl google.com` de otras prácticas. **`curl` es un navegador sin ventana**: pide una URL y te escupe la respuesta en la terminal, tal cual llega.
>
> - Está **ya instalado** en Windows 10/11, en Linux y en macOS. No hay que instalar nada.
> - Es la herramienta estándar de un administrador para hablar con un servicio web.
>
> ```bash
> curl "https://api.ipify.org?format=json"
> ```
> Eso es todo. Sin programar, sin librerías, sin Python.

> [!warning] El fallo nº1: creerse el `ipconfig`
> `ipconfig` (o `ip a` en Linux) te da la IP **que tu equipo tiene asignada en su red local**: `192.168.1.47`, `10.10.10.10`… Esa dirección **no existe en Internet**: es privada, se repite en millones de casas y ningún servidor de fuera puede alcanzarla.
>
> La IP con la que tú sales al mundo es **otra**, la de tu router, y **tu ordenador no la conoce**. Por eso hay que preguntar fuera. En esta práctica lo vas a ver con tus ojos, y ahí es donde se entiende el **NAT** de verdad.

> [!example] Vocabulario de esta práctica
> - **API:** una web hecha para que la consulte un programa. Devuelve datos, no páginas.
> - **JSON:** el formato en que responden. Texto con `{ "clave": "valor" }`.
> - **`curl`:** comando que consulta una URL desde la terminal.
> - **IP privada:** la de tu red local (`192.168.x.x`, `10.x.x.x`). No se ve desde Internet.
> - **IP pública:** con la que sale tu red al exterior. Es la del router, la comparten todos los equipos de casa.
> - **AS (Sistema Autónomo):** el número que identifica a un operador grande en Internet. Google es el `AS15169`.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-9b-verificar-tu-red-con-apis-publicas.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura de la Fase 0.1 y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.9b · Verificar tu red con APIs públicas`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `Enlace al vídeo explicativo`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio entero, crea tu entrada de apuntes, arranca OBS y preséntate. Ten la **VM de la B1.9 encendida** y una terminal abierta en tu equipo anfitrión.

> [!example] Paso 1 — Lo que tu equipo cree de sí mismo
> En tu **equipo anfitrión** (el real, no la VM), abre la terminal y mira tu IP local:
> ```bash
> ipconfig          # Windows
> ip a              # Linux
> ```
> **Anota tu IPv4.** Será algo como `192.168.1.47` o `10.0.2.15`. Dila en voz alta.

> [!example] Paso 2 — Lo que Internet ve de ti (aquí cae el NAT)
> Ahora pregúntaselo a alguien de fuera:
> ```bash
> curl "https://api.ipify.org?format=json"
> ```
> Sale algo como `{"ip":"88.20.134.7"}`.
>
> > [!danger] 🤔 Para y piénsalo antes de seguir
> > **No es la misma IP que la del Paso 1.** Ni se parece.
> > Explica en el vídeo, con tus palabras, **por qué**. ¿Dónde está esa segunda dirección? ¿De quién es? ¿Por qué tu ordenador no la conoce?
> >
> > *(Pista: es la misma que le saldría a tu hermano desde su móvil conectado al mismo wifi. Pruébalo si puedes.)*

> [!example] Paso 3 — Todo lo que se sabe de ti sin que se lo digas
> Una API más completa, del propio Cloudflare:
> ```bash
> curl "https://www.cloudflare.com/cdn-cgi/trace"
> ```
> Devuelve algo así:
> ```
> ip=88.20.134.7      loc=ES        colo=MAD
> http=http/2         tls=TLSv1.3   uag=curl/8.7.1
> ```
> **Explica cada campo en el vídeo:**
>
> | Campo | Qué es |
> | :--- | :--- |
> | `ip` | Tu IP pública |
> | `loc` | El país desde el que sales |
> | `colo` | **El centro de datos que te está atendiendo** (`MAD` = Madrid) |
> | `http` | La versión del protocolo HTTP que ha usado tu `curl` |
> | `tls` | La versión de cifrado de la conexión |
> | `uag` | Tu *user agent*: le has dicho que eres `curl`, no un navegador |
>
> Fíjate en que **no le has dado ni un dato**: todo eso lo deduce de tu propia conexión.

> [!example] Paso 4 — Comprueba tu cálculo de subred
> En la B1.9 configuraste la red Solo-Anfitrión. Vamos a verificar que la entiendes.
>
> **Primero, a mano y sin ayuda.** Para la red `10.10.10.0/26`, escribe en tu entrada de apuntes:
> - La máscara en formato decimal
> - La dirección de red y la de broadcast
> - Cuántos hosts asignables hay
> - El primero y el último
>
> **Ahora compruébalo:**
> ```bash
> curl "https://networkcalc.com/api/ip/10.10.10.0/26"
> ```
> ```json
> "subnet_mask": "255.255.255.192",   "broadcast_address": "10.10.10.63",
> "assignable_hosts": 62,             "first_assignable_host": "10.10.10.1"
> ```
>
> > [!success] Compara y explica
> > **¿Coincide con lo tuyo?** Si sí, dilo. Si no, **no borres tu respuesta**: déjala en la entrada y explica en el vídeo **dónde te equivocaste**. Eso vale más que acertar a la primera.
> >
> > Repítelo con **la red de tu propio laboratorio** (`/24`) y compara: ¿cuántos hosts caben en una `/24` frente a una `/26`?

> [!example] Paso 5 — ¿De quién es una IP? (bonus)
> ```bash
> curl "http://ip-api.com/json/8.8.8.8?fields=query,country,isp,as"
> ```
> ```json
> {"query":"8.8.8.8","country":"United States","isp":"Google LLC","as":"AS15169 Google LLC"}
> ```
> Pruébalo con **tu propia IP pública** (la del Paso 2): saldrá **tu operador** — Movistar, Vodafone, Orange… y su número de AS.
>
> Esto es lo que hace un administrador cuando ve una IP rara en los registros de su servidor: **averiguar de quién es antes de bloquearla.**

> [!example] Paso 6 — Cierra el vídeo y súbelo
> Detén la grabación, nombra el vídeo `B1.9b · Verificar tu red con APIs públicas`, súbelo a `B1_Entorno` (No listado) con timestamps:
> ```
> 00:00 Presentacion
> 00:30 Paso 1 - Mi IP local segun mi equipo
> 01:10 Paso 2 - Mi IP publica segun Internet
> 02:20 Paso 3 - Cloudflare Trace campo a campo
> 03:40 Paso 4 - Subred a mano y comprobacion
> 05:10 Paso 5 - De quien es una IP
> 06:00 Paso 6 - Repaso final
> ```

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | `curl: command not found` | Estás en un Windows antiguo o en un `cmd` raro | Usa **PowerShell** o **Git Bash**. En Windows 10/11 `curl` viene de serie |
> | La URL se parte y falla | La terminal se come el `?` o el `&` | **Pon la URL entre comillas dobles**, siempre |
> | Sale la misma IP en el Paso 1 y el 2 | No estás detrás de un router NAT (raro en un aula) | Coméntalo: es un caso interesante, no un fallo |
> | `curl` se queda colgado | El cortafuegos del centro bloquea la salida | Prueba con otra API. Si ninguna responde, avísame |
> | El JSON sale en una línea ilegible | Es lo normal, `curl` no lo formatea | Añade `| python -m json.tool` al final, o léelo tal cual |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Sabes decir tu **IP privada** y tu **IP pública**, y por qué son distintas.
> - Has explicado los seis campos de Cloudflare Trace.
> - Has calculado una subred **a mano** y la has contrastado con la API.
> - Sabes averiguar de quién es una IP cualquiera.

> [!question] Comprueba que lo has entendido
> Responde en tu entrada de apuntes, con tus palabras:
> 1. ¿Qué diferencia hay entre una **web** y una **API**? Pon un ejemplo de cada una.
> 2. ¿Por qué tu ordenador **no puede** decirte tu IP pública él solo?
> 3. Tu compañero de al lado hace el Paso 2 en el mismo aula. ¿Le saldrá **la misma** IP pública que a ti? **¿Por qué?**
> 4. En el Paso 4, ¿acertaste a la primera? Si no, **¿en qué te equivocaste exactamente?**
> 5. ¿Por qué una comprobación hecha desde el propio equipo que estás comprobando vale menos que una hecha desde fuera?
> 6. 🔬 **Reto:** consulta la IP pública **desde dentro de la VM** con el adaptador NAT activo. ¿Es la misma que la del anfitrión? Explica el resultado — y ahí tienes el NAT explicado por ti mismo.

---

## ✅ Entregables y cierre

- **Entregable vídeo:** `B1.9b · Verificar tu red con APIs públicas` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Entregable apuntes:** `b1-9b-verificar-tu-red-con-apis-publicas.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.
- **Criterio de éxito:** sabes explicar la diferencia entre IP privada y pública **con tus propios datos en pantalla**, y verificas un cálculo de subred contra una fuente externa.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste copiar comandos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!note] 📌 Sobre las APIs que has usado
> Las cuatro son **públicas y gratuitas**, y ninguna pide registro ni clave. Están sacadas de un catálogo abierto de más de 1.600 APIs.
> Dos advertencias de administrador, que valen para siempre:
> - **Una API puede caerse o desaparecer** sin avisar. Si el día de la práctica una no responde, no es culpa tuya: dímelo y seguimos con otra.
> - **Nunca metas una clave o contraseña tuya en un comando que vayas a subir a GitHub.** Aquí no hace falta ninguna, y por eso he elegido estas.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - Qué es una **API** y en qué se diferencia de una web normal.
> - A usar **`curl`** para consultar un servicio desde la terminal, sin programar.
> - La diferencia real entre **IP privada y pública**, viéndola en tu propia pantalla — y con ella, el **NAT**.
> - A **verificar tus cálculos de subred** contra una fuente externa.
> - Y lo más importante para lo que viene: **comprobar desde fuera lo que desde dentro no se puede ver.** Eso lo harás con tus servidores durante todo el curso.
>
> **Siguiente:** B1.10 — Instalación limpia de un sistema operativo.
