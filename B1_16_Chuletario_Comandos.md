---
Documento: Chuletario de comandos B1.16
Bloque: 01_Entorno
Tipo: Chuletario
---

## B1.16 — Chuletario de comandos (Windows y Windows)

> [!abstract] Ficha del documento
> | | |
> | :--- | :--- |
> | **Centro** | IES Jorge Juan (Alicante) |
> | **Curso** | 2026-27 · 1.er trimestre |
> | **Módulo** | SOR · Sistemas Operativos en Red · 2.º SMR (Ciclo Formativo de Grado Medio) |
> | **Bloque** | Bloque 1 · Preparar el entorno |
> | **Prácticas** | B1.16a a B1.16f · Laboratorio Windows y Windows (ediciones Cole y Casa) |
> | **Profesor** | Pedro Navarro Miralles |
> | **Licencia** | © 2026 Pedro Navarro Miralles · [CC BY-NC-SA 4.0](LICENSE): atribución obligatoria, uso no comercial, compartir igual |

**Máquinas:** Servidor = `W11-SRV` (VM `B1-W11-SRV`, IP fija `192.168.100.10`) · Cliente = `W11-CLI` (VM `B1-W11-CLI`, IP por DHCP) · Red NAT `B1_LAB` (`192.168.100.0/24`).
**«Admin»** = PowerShell como administrador. **«Normal»** = PowerShell sin administrador, con la sesión del usuario que toque.

### B1.16a · Red básica

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 1 | Servidor · Admin | `Rename-Computer -NewName "W11-SRV" -Restart` | Cambia el nombre del equipo y reinicia. |
| 2 | Cliente · Admin | `Rename-Computer -NewName "W11-CLI" -Restart` | Cambia el nombre del equipo y reinicia. |
| 3 | Los dos | `hostname` | Muestra el nombre del equipo. |
| 4 | Los dos | `ipconfig /all` | IP, máscara, puerta de enlace, DNS, servidor DHCP y MAC de cada tarjeta. |
| 5 | Cliente | `tracert -d -h 3 1.1.1.1` | Primeros tres saltos hacia Internet. El salto 1 es la puerta de enlace. |
| 6 | Los dos | `nslookup www.google.es` | Pregunta al DNS la IP de un nombre y dice qué DNS contesta. |
| 7 | Los dos | `ping 192.168.100.X` | Prueba la conexión con el otro equipo (cambia `X`). |
| 8 | Los dos | `Get-NetConnectionProfile` | Dice si la red es `Public` o `Private`. |
| 9 | Los dos · Admin | `Set-NetConnectionProfile -InterfaceAlias "Ethernet" -NetworkCategory Private` | Pasa la red a privada. |
| 10 | Los dos · Admin | `New-NetFirewallRule -DisplayName "LAB - Ping entrante (ICMPv4)" -Direction Inbound -Protocol ICMPv4 -IcmpType 8 -Action Allow -Profile Private` | Deja entrar solo el ping, y solo en redes privadas. |
| 11 | Los dos | `arp -a` | Relación IP ↔ MAC de los vecinos con los que has hablado. |
| 12 | Cliente | `ping 192.168.100.10` | Comprueba que la IP fija del servidor está libre (no debe responder). |
| 13 | Los dos · Admin | `Remove-NetFirewallRule -DisplayName "LAB - Ping entrante (ICMPv4)"` | Solo camino A: borra la regla de ping heredada de B1.14b. |

### B1.16b · Carpeta compartida para todos

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 14 | Cliente | `ping -4 W11-SRV` | Comprueba que el cliente encuentra al servidor por su nombre. |
| 15 | Los dos · Admin | `$pw = Read-Host "Contraseña de laboratorio" -AsSecureString` | Pide la contraseña sin mostrarla y la guarda en `$pw`. |
| 16 | Los dos · Admin | `foreach ($u in "juan","pedro","maria","ana") { New-LocalUser -Name $u -Password $pw -PasswordNeverExpires; Add-LocalGroupMember -SID S-1-5-32-545 -Member $u }` | Crea los cuatro usuarios y los mete en *Usuarios*. |
| 17 | Los dos | `Get-LocalUser` | Lista los usuarios del equipo. |
| 18 | Servidor · Admin | `New-Item -Path C:\Compartida -ItemType Directory` y `1..5 \| ForEach-Object { New-Item -Path "C:\Compartida\servidor_$_.txt" -ItemType File -Value "Creado en el servidor" }` | Crea la carpeta y cinco archivos de prueba. |
| 19 | Servidor · Admin | `icacls C:\Compartida /grant "*S-1-5-11:(OI)(CI)M"` | Da *Modificar* a *Usuarios autentificados*. |
| 20 | Servidor | `Get-SmbShareAccess -Name Compartida` | Permisos del recurso compartido. |
| 21 | Servidor | `icacls C:\Compartida` | Permisos NTFS de la carpeta. |
| 22 | Cliente | `net view \\W11-SRV` | Qué comparte el servidor. |
| 23 | Servidor · Admin | `Get-SmbSession` | Quién está conectado al servidor ahora mismo. |
| 24 | Cliente · Normal | `New-Item -Path \\W11-SRV\Compartida\<archivo> -ItemType File -Value "Hola, soy <usuario>"` | Crea un archivo en la carpeta compartida. |
| 25 | Cliente · Normal | `Remove-Item -Path \\W11-SRV\Compartida\<archivo>` | Borra un archivo de la carpeta compartida. **No va a la Papelera.** |
| 26 | Cliente · Normal | `Get-ChildItem \\W11-SRV\Compartida` | Lista la carpeta compartida. |
| 27 | Servidor · Admin | `Get-ChildItem C:\Compartida \| Select-Object Name, @{n='Propietario'; e={ (Get-Acl $_.FullName).Owner }}` | Cada archivo con su propietario. |

### B1.16c · Permisos por usuario

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 28 | Servidor · Admin | `icacls C:\Compartida /grant:r "*S-1-5-32-544:(OI)(CI)F" "*S-1-5-18:(OI)(CI)F" "juan:(OI)(CI)M" "pedro:(OI)(CI)M" "maria:(OI)(CI)RX"` | Administradores y SYSTEM: control total · juan y pedro: modificar · maria: lectura. |
| 29 | Servidor · Admin | `icacls C:\Compartida /inheritance:r` | Corta la herencia y quita lo heredado. |
| 30 | Servidor · Admin | `icacls C:\Compartida /remove "*S-1-5-11"` | Quita a *Usuarios autentificados* (lo puesto a mano en B1.16b). |
| 31 | Servidor | `icacls C:\Compartida\pedro_2.txt` | Permisos de un archivo: deben salir heredados `(I)`. |
| 32 | Cliente · Normal | `Get-Content \\W11-SRV\Compartida\pedro_2.txt` | Lee un archivo de la carpeta compartida. |

### B1.16d y B1.16e · Impresora compartida

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 33 | Servidor · Admin | `New-Item -Path C:\Impresiones -ItemType Directory` | Crea la carpeta donde caen los PDF. **No se comparte.** |
| 34 | Servidor · Admin | `icacls C:\Impresiones /grant "*S-1-5-11:(OI)(CI)M"` | Permite escribir en ella a quien imprime. |
| 35 | Servidor | `Get-Printer -Name LAB-PDF \| Format-List Name, DriverName, PortName, Shared, ShareName` | Controlador, puerto y si está compartida. |
| 36 | Servidor · Admin | `Set-Printer -Name LAB-PDF -KeepPrintedJobs $true` | La cola conserva los trabajos ya impresos. |
| 37 | Servidor | `"Prueba desde el servidor W11-SRV" \| Out-Printer -Name LAB-PDF` | Imprime una línea en local. |
| 38 | Servidor | `Rename-Item C:\Impresiones\LAB-PDF.pdf impreso_por_<quien>.pdf` | Guarda el PDF con otro nombre antes del siguiente trabajo. |
| 39 | Cliente · Normal | `Add-Printer -ConnectionName \\W11-SRV\LAB-PDF` | Conecta la impresora compartida para ese usuario. |
| 40 | Cliente · Normal | `"Hola, soy <usuario> e imprimo desde W11-CLI" \| Out-Printer -Name \\W11-SRV\LAB-PDF` | Imprime en la impresora compartida. |
| 41 | Servidor · Admin | `Get-PrintJob -PrinterName LAB-PDF \| Select-Object Id, UserName, DocumentName, SubmittedTime` | Quién imprimió qué y cuándo. |
| 42 | Servidor | `Get-ChildItem C:\Impresiones` | Lista los PDF generados. |
| 49 | Cliente · Admin | `rundll32 printui.dll,PrintUIEntry /ga /n\\W11-SRV\LAB-PDF` | **Solo si falla el 39:** conecta la impresora para todos los usuarios del equipo. Reinicia después. |

### B1.16f · Escritorio remoto

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 43 | Cliente | `Test-NetConnection W11-SRV -Port 3389` | ¿Hay red (`PingSucceeded`)? ¿Alguien atiende en el 3389 (`TcpTestSucceeded`)? |
| 44 | Servidor · Admin | `Add-LocalGroupMember -SID S-1-5-32-555 -Member juan, pedro` | Mete a juan y pedro en *Usuarios de escritorio remoto*. |
| 45 | Servidor | `Get-LocalGroupMember -SID S-1-5-32-555` | Quién está en *Usuarios de escritorio remoto*. |
| 46 | Cliente | `mstsc /v:W11-SRV` | Abre el escritorio remoto contra el servidor. Usuario: `W11-SRV\<usuario>`. |
| 47 | Dentro de la sesión remota | `hostname` y `whoami` | Demuestra en qué equipo y con qué usuario estás. |
| 48 | Dentro de la sesión remota | `quser` | Sesiones abiertas en el equipo, delante (`console`) o remotas (`rdp-tcp`). |

> [!warning] Ojo
> - Usa el nombre real de tu tarjeta (`Ethernet` es el habitual).
> - **Nunca apagues el firewall.** Solo se abre lo necesario, y solo en redes privadas.
> - Los SID (`S-1-5-32-544`, `-545`, `-555`, `S-1-5-11`, `S-1-5-18`) son los mismos en cualquier Windows, en cualquier idioma. Por eso se usan en vez de los nombres de los grupos.
> - `Tab` completa nombres y rutas; la flecha ↑ repite el último comando.

**Vuelve a las prácticas:** [B1.16a](B1_16.a_Red_Basica_Dos_Windows_11.md) · [B1.16b](B1_16.b_Carpeta_Compartida_Para_Todos_Windows.md) · [B1.16c](B1_16.c_Permisos_por_Usuario_Windows.md) · [B1.16d](B1_16.d_Impresora_PDF_Compartida_Windows.md) · [B1.16e](B1_16.e_Impresora_Solo_para_Pedro_Windows.md) · [B1.16f](B1_16.f_Escritorio_Remoto_Windows.md).
