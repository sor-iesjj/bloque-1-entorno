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
> | **Prácticas** | B1.16a a B1.16g · Laboratorio Windows y Windows (ediciones Cole y Casa) |
> | **Profesor** | Pedro Navarro Miralles |
> | **Licencia** | © 2026 Pedro Navarro Miralles · [CC BY-NC-SA 4.0](LICENSE): atribución obligatoria, uso no comercial, compartir igual |

> [!tip] Esto es el 💻 Plan B
> En las prácticas, el **Plan A** es con ventanas y es el que se espera en el vídeo. Aquí están **los mismos pasos con comandos**, para quien quiera practicar el terminal o por si una ventana no aparece. Los que llevan **💻 Solo con comando** no tienen ventana equivalente: esos sí hay que hacerlos aquí.

**Máquinas:** Servidor = `W11-SRV` (VM `B1-W11-SRV`, IP fija `192.168.100.10`) · Cliente = `W11-CLI` (VM `B1-W11-CLI`, IP por DHCP) · Red NAT `B1_LAB` (`192.168.100.0/24`).
**«Admin»** = PowerShell como administrador. **«Normal»** = PowerShell sin administrador, con la sesión del usuario que toque.

### B1.16a · Red básica

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 1 | Servidor · Admin | `Rename-Computer -NewName "W11-SRV" -Restart` | Cambia el nombre del equipo y reinicia. |
| 2 | Cliente · Admin | `Rename-Computer -NewName "W11-CLI" -Restart` | Cambia el nombre del equipo y reinicia. |
| 3 | Los dos | `hostname` | Muestra el nombre del equipo. |
| 4 | Los dos | `ipconfig /all` | IP, máscara, puerta de enlace, DNS, servidor DHCP y MAC de cada tarjeta. |
| 5 | Los dos | `Get-NetRoute -DestinationPrefix 0.0.0.0/0` | 💻 **Solo con comando.** Ruta por defecto: el `NextHop` es la puerta de enlace. |
| 6 | Los dos | `nslookup www.google.es` | 💻 **Solo con comando.** Pregunta al DNS la IP de un nombre y dice qué DNS contesta. |
| 7 | Los dos | `ping 192.168.100.X` | 💻 **Solo con comando.** Prueba la conexión con el otro equipo (cambia `X`). |
| 8 | Los dos | `Get-NetConnectionProfile` | Dice si la red es `Public` o `Private`. |
| 9 | Los dos · Admin | `Set-NetConnectionProfile -InterfaceAlias "Ethernet" -NetworkCategory Private` | Pasa la red a privada. |
| 10 | Los dos · Admin | `New-NetFirewallRule -DisplayName "LAB - Ping entrante (ICMPv4)" -Direction Inbound -Protocol ICMPv4 -IcmpType 8 -Action Allow -Profile Private` | Deja entrar solo el ping, y solo en redes privadas. |
| 63 | Los dos · Admin | `([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)` | 💻 **Solo con comando.** `True` = la ventana es de administrador. Si sale *«Acceso denegado»* en el 9 o el 10, mira esto primero. |
| 11 | Los dos | `arp -a` | 💻 **Solo con comando.** Relación IP ↔ MAC de los vecinos con los que has hablado. |
| 12 | Cliente | `ping 192.168.100.10` | 💻 **Solo con comando.** Comprueba que la IP fija del servidor está libre (no debe responder). |
| 13 | Base, en modo auditoría | `C:\Windows\System32\Sysprep\sysprep.exe /generalize /oobe /shutdown` | **Sella la base:** le borra el SID (`/generalize`), deja el próximo arranque en la configuración inicial (`/oobe`) y la apaga. Cierra antes la ventana de Sysprep con **Cancelar**. |
| 64 | Servidor · Admin | `$dns = (Get-DnsClientServerAddress -InterfaceAlias "Ethernet" -AddressFamily IPv4).ServerAddresses` y luego `$dns` | Guarda el DNS que dio el DHCP, antes de quitarlo. Del 64 al 15, **en la misma ventana**. |
| 65 | Servidor · Admin | `Set-NetIPInterface -InterfaceAlias "Ethernet" -Dhcp Disabled`, después `Get-NetIPAddress -InterfaceAlias "Ethernet" -AddressFamily IPv4 -ErrorAction SilentlyContinue \| Remove-NetIPAddress -Confirm:$false` y `Get-NetRoute -InterfaceAlias "Ethernet" -DestinationPrefix "0.0.0.0/0" -ErrorAction SilentlyContinue \| Remove-NetRoute -Confirm:$false` | Quita la configuración del DHCP. Sin esto, el 14 dice *«already exists»*. |
| 14 | Servidor · Admin | `New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress 192.168.100.10 -PrefixLength 24 -DefaultGateway 192.168.100.1` | IP fija con su puerta de enlace, la `.1` de la Red NAT. Antes, el 64 y el 65. |
| 15 | Servidor · Admin | `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses $dns` | Pone el DNS que guardaste con el 64. En otra ventana `$dns` está vacía. |
| 56 | Base, consola de `Shift + F10` en la pantalla del país | `C:\Windows\System32\Sysprep\sysprep.exe /audit /reboot` | **Solo si `Ctrl + Shift + F3` no funciona:** reinicia en modo auditoría. La consola tiene que estar en `C:\Windows\system32`; si dice `X:\sources`, sigues en el instalador. |
| 55 | Los dos | `whoami /user` | 💻 **Solo con comando.** Tu usuario y su SID. Los tres números largos del medio son el **SID del equipo**: tienen que ser **distintos** en `W11-SRV` y `W11-CLI`. |
| 62 | Clon, consola de `Shift + F10` en la configuración inicial | `start ms-cxh:localonly` | Abre la ventana para crear un **usuario local**, también sin red. Para cuando te quedas en *«Vamos a conectarte a una red»* (cable sin marcar) o no sale el camino de la cuenta local. |

### B1.16b · Carpeta compartida para todos

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 16 | Cliente | `ping -4 W11-SRV` | 💻 **Solo con comando.** Comprueba que el cliente encuentra al servidor por su nombre. |
| 17 | Los dos · Admin | `$pw = Read-Host "Contraseña de laboratorio" -AsSecureString` | Pide la contraseña sin mostrarla y la guarda en `$pw`. |
| 18 | Los dos · Admin | `foreach ($u in "juan","pedro","maria","ana") { New-LocalUser -Name $u -Password $pw -PasswordNeverExpires; Add-LocalGroupMember -SID S-1-5-32-545 -Member $u }` | Crea los cuatro usuarios y los mete en *Usuarios*. |
| 19 | Los dos | `Get-LocalUser` | Lista los usuarios del equipo. |
| 20 | Servidor · Admin | `New-Item -Path C:\Compartida -ItemType Directory` y `1..5 \| ForEach-Object { New-Item -Path "C:\Compartida\servidor_$_.txt" -ItemType File }` | Crea la carpeta y cinco archivos de prueba. |
| 21 | Servidor · Admin | `New-SmbShare -Name Compartida -Path C:\Compartida -FullAccess Todos` | Comparte la carpeta con *Todos* en control total. |
| 22 | Servidor · Admin | `icacls C:\Compartida /grant "*S-1-5-11:(OI)(CI)M"` | Da *Modificar* a *Usuarios autentificados*. |
| 23 | Servidor · Admin | `Get-SmbShareAccess -Name Compartida` | Permisos del recurso compartido. |
| 24 | Servidor · Admin | `icacls C:\Compartida` | Permisos NTFS de la carpeta. |
| 25 | Cliente | `net view \\W11-SRV` | Qué comparte el servidor. |
| 26 | Servidor · Admin | `Get-SmbSession` | Quién está conectado al servidor ahora mismo. |
| 27 | Cliente · Normal | `net use S: \\W11-SRV\Compartida /persistent:yes` | Conecta la unidad de red `S:` y la recuerda para el próximo inicio de sesión. |
| 28 | Cliente · Normal | `New-Item -Path S:\<archivo> -ItemType File` | Crea un archivo en `S:`. |
| 29 | Cliente · Normal | `Remove-Item -Path S:\<archivo>` | Borra un archivo de `S:`. **No va a la Papelera.** |
| 30 | Cliente · Normal | `Get-ChildItem S:\` | Lista `S:`. |
| 31 | Servidor · Admin | `Get-ChildItem C:\Compartida \| Select-Object Name, @{n='Propietario'; e={ (Get-Acl $_.FullName).Owner }}` | Cada archivo con su propietario. |

### B1.16c · Permisos por usuario

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 32 | Servidor · Admin | `icacls C:\Compartida /grant:r "*S-1-5-32-544:(OI)(CI)F" "*S-1-5-18:(OI)(CI)F" "juan:(OI)(CI)M" "pedro:(OI)(CI)M" "maria:(OI)(CI)RX"` | Administradores y SYSTEM: control total · juan y pedro: modificar · maria: lectura. |
| 33 | Servidor · Admin | `icacls C:\Compartida /inheritance:r` | Corta la herencia y quita lo heredado. |
| 34 | Servidor · Admin | `icacls C:\Compartida /remove "*S-1-5-11"` | Quita a *Usuarios autentificados* (lo puesto a mano en B1.16b). |
| 35 | Servidor · Admin | `icacls C:\Compartida\pedro_2.txt` | Permisos de un archivo: deben salir heredados `(I)`. |
| 36 | Cliente · Normal | `Get-Content S:\pedro_2.txt` | Lee un archivo de `S:`. |

### B1.16d y B1.16e · Impresora compartida

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 37 | Servidor · Admin | `New-Item -Path C:\Impresiones -ItemType Directory` | Crea la carpeta donde caen los PDF. **No se comparte.** |
| 38 | Servidor · Admin | `icacls C:\Impresiones /grant "*S-1-5-11:(OI)(CI)M"` | Permite escribir en ella a quien imprime. |
| 39 | Servidor · Admin | `Add-PrinterPort -Name "C:\Impresiones\LAB-PDF.pdf"` y `Add-Printer -Name LAB-PDF -DriverName "Microsoft Print To PDF" -PortName "C:\Impresiones\LAB-PDF.pdf" -Shared -ShareName LAB-PDF` | Crea el puerto archivo y la impresora, ya compartida. |
| 40 | Servidor | `Get-Printer -Name LAB-PDF \| Format-List Name, DriverName, PortName, Shared, ShareName` | Controlador, puerto y si está compartida. |
| 41 | Servidor · Admin | `Set-Printer -Name LAB-PDF -KeepPrintedJobs $true` | La cola conserva los trabajos ya impresos. |
| 42 | Servidor | `"Prueba desde el servidor W11-SRV" \| Out-Printer -Name LAB-PDF` | Imprime una línea en local. |
| 43 | Servidor | `Rename-Item C:\Impresiones\LAB-PDF.pdf impreso_por_<quien>.pdf` | Guarda el PDF con otro nombre antes del siguiente trabajo. |
| 44 | Cliente · Normal | `Add-Printer -ConnectionName \\W11-SRV\LAB-PDF` | Conecta la impresora compartida para ese usuario. |
| 45 | Cliente · Normal | `"Hola, soy <usuario> e imprimo desde W11-CLI" \| Out-Printer -Name \\W11-SRV\LAB-PDF` | Imprime en la impresora compartida. |
| 46 | Servidor · Admin | `Get-PrintJob -PrinterName LAB-PDF \| Select-Object Id, UserName, DocumentName, SubmittedTime` | Quién imprimió qué y cuándo. |
| 47 | Servidor | `Get-ChildItem C:\Impresiones` | Lista los PDF generados. |

### B1.16f · Escritorio remoto

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 48 | Cliente | `Test-NetConnection W11-SRV -Port 3389` | 💻 **Solo con comando.** ¿Hay red (`PingSucceeded`)? ¿Alguien atiende en el 3389 (`TcpTestSucceeded`)? |
| 49 | Servidor · Admin | `Add-LocalGroupMember -SID S-1-5-32-555 -Member juan, pedro` | Mete a juan y pedro en *Usuarios de escritorio remoto*. |
| 50 | Servidor | `Get-LocalGroupMember -SID S-1-5-32-555` | Quién está en *Usuarios de escritorio remoto*. |
| 51 | Cliente | `mstsc /v:W11-SRV` | Abre el escritorio remoto contra el servidor. Usuario: `W11-SRV\<usuario>`. |
| 52 | Dentro de la sesión remota | `hostname` y `whoami` | Demuestra en qué equipo y con qué usuario estás. |
| 53 | Dentro de la sesión remota | `quser` | Sesiones abiertas en el equipo, delante (`console`) o remotas (`rdp-tcp`). |

### Solo en tu ordenador: quitar la tortuga verde de VirtualBox (B1.16a, errores)

Todo en tu **Windows físico**, no en la VM, en PowerShell **como administrador** y **solo si eres el administrador del equipo**. Deja el equipo menos protegido, y el Laboratorio 3 (Hyper-V) necesita deshacerlo. Lee antes el cuadro «La tortuga verde» de B1.16a.

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 57 | Tu Windows físico · Admin | `(Get-CimInstance Win32_ComputerSystem).HypervisorPresent` | 💻 **Solo con comando.** `True` = el hipervisor de Windows está encendido (tortuga). `False` = apagado. |
| 58 | Tu Windows físico · Admin | `bcdedit /set hypervisorlaunchtype off` | Que el hipervisor no arranque con Windows. Se deshace con `auto`. |
| 59 | Tu Windows físico · Admin | `Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All,VirtualMachinePlatform,HypervisorPlatform -NoRestart` | Apaga Hyper-V, la Plataforma de máquina virtual (WSL2, Docker) y la Plataforma del hipervisor. |
| 60 | Tu Windows físico · Admin | `reg add "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard\Scenarios\HypervisorEnforcedCodeIntegrity" /v Enabled /t REG_DWORD /d 0 /f` | Apaga la integridad de memoria (lo mismo que el interruptor de Seguridad de Windows). |
| 61 | Tu Windows físico · Admin | `reg add "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v EnableVirtualizationBasedSecurity /t REG_DWORD /d 0 /f` | Apaga la seguridad basada en virtualización (VBS). Después, **Reiniciar** (no Apagar) y repetir el 57. |

### Solo si algo falla

| Nº | Dónde | Comando | Qué hace |
| :--- | :--- | :--- | :--- |
| 54 | Cliente · Admin | `rundll32 printui.dll,PrintUIEntry /ga /n\\W11-SRV\LAB-PDF` | **Solo si falla la conexión a la impresora en B1.16d:** la conecta para todos los usuarios del equipo. Reinicia después. |

> [!warning] Ojo
> - Usa el nombre real de tu tarjeta (`Ethernet` es el habitual).
> - **Nunca apagues el firewall.** Solo se abre lo necesario, y solo en redes privadas.
> - El 55 va en la tabla de B1.16a: es la comprobación del SID del Paso 4.3.
> - Los SID de **grupo** (`S-1-5-32-544`, `-545`, `-555`, `S-1-5-11`, `S-1-5-18`) son los mismos en cualquier Windows, en cualquier idioma: por eso se usan en vez de los nombres de los grupos. El SID del **equipo**, en cambio, es único de cada instalación: por eso se comprueba con el 55. El 21 usa `Todos`, que es el nombre en un Windows en español; en inglés sería `Everyone`.
> - `Tab` completa nombres y rutas; la flecha ↑ repite el último comando.

**Vuelve a las prácticas:** [B1.16a Básico](B1_16.a_Red_Basica_Dos_Windows_11_Basico.md) · [B1.16a Avanzado](B1_16.a_Red_Basica_Dos_Windows_11_Avanzado.md) · [B1.16b](B1_16.b_Carpeta_Compartida_Para_Todos_Windows.md) · [B1.16c](B1_16.c_Permisos_por_Usuario_Windows.md) · [B1.16d](B1_16.d_Impresora_PDF_Compartida_Windows.md) · [B1.16e](B1_16.e_Impresora_Solo_para_Pedro_Windows.md) · [B1.16f](B1_16.f_Escritorio_Remoto_Windows.md) · [B1.16g](B1_16.g_Base_Sellada_SID_y_Clonado_Seguro_Windows.md).
