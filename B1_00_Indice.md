# 🧰 Bloque 1 — Preparar el entorno e instalar el SO

> Bloque previo al proyecto **Boochan**: preparar el equipo, crear medios de instalación e instalar sistemas operativos. Todo con herramientas **actuales** (Rufus, Ventoy, iVentoy, GParted) y siguiendo la **metodología de grabación** del curso.

## Metodología (igual que en el resto)
- Cada práctica se **graba entera con OBS**, presentándote y con **timestamps**.
- **Playlist:** `B1_Entorno` · **Vídeo:** `B1.n · título` (No listado) · **una entrega por práctica**; en los laboratorios con ediciones Cole y Casa (B1.14, B1.15 y B1.16), **un vídeo por edición** (ver secciones F y G).
- Estructura fija: ficha → fundamento → 📹 grabación → procedimiento (Paso 0 + pasos + cierre) → errores/verificación → preguntas → entregables → resumen.


> [!abstract] 📋 Qué RA y CE cubre este bloque
> El bloque trabaja el **`RA.01`** (instalación de sistemas operativos en red) casi en su totalidad, y toca el **`RA.05`** en las prácticas de automatización y verificación.
>
> | CE | Criterio | Dónde |
> | :--- | :--- | :--- |
> | `CE.01.a` | Estudio de compatibilidad del sistema informático | B1.1 · B1.2 · B1.3 · B1.9 |
> | `CE.01.b` | Modos de instalación | B1.4 · B1.5 · B1.6 · B1.7 · B1.10 · B1.11 · B1.13 |
> | `CE.01.c` | Particionado del disco del servidor | B1.5 · B1.8 · B1.8b · B1.10 · B1.13 |
> | `CE.01.d` | Sistemas de archivos | B1.8 · B1.8b · B1.10 |
> | `CE.01.e` | Componentes a instalar | B1.3 · B1.10 |
> | `CE.01.f` | **Automatización de instalaciones** | B1.11 · B1.12 · B1.13 |
> | `CE.01.g` | Preferencias del entorno personal | B1.10 |
> | `CE.01.i` | Conectividad servidor–cliente | B1.9b · B1.11 · B1.14a · B1.14b · B1.14c · B1.15a · B1.15b · B1.16a · B1.16g |
> | `CE.05.e` | Automatización de tareas del sistema | B1.12 · B1.13 |
> | `CE.05.f` | Interpretar la configuración del sistema | B1.9b · B1.13 · B1.16a · B1.16g |
>
> **El laboratorio B1.16 (Windows y Windows) entra además en el `RA.02` y el `RA.04`:**
>
> | CE | Criterio | Dónde |
> | :--- | :--- | :--- |
> | `CE.02.a` | Configurar y gestionar cuentas de usuario | B1.16b |
> | `CE.02.f` | Pertenencia de usuarios a grupos | B1.16f |
> | `CE.04.a` | Diferencia entre permiso y derecho | B1.16f |
> | `CE.04.b` | Recursos que se van a compartir y en qué condiciones | B1.16b |
> | `CE.04.c` | Asignar permisos a los recursos compartidos | B1.16c |
> | `CE.04.d` | Compartir impresoras en red | B1.16d · B1.16e |
> | `CE.04.e` | Entorno gráfico para compartir recursos | B1.16b · B1.16c · B1.16d · B1.16e |
> | `CE.04.f` | Niveles de seguridad en el acceso a recursos compartidos | B1.16c · B1.16e |
>
> **`CE.01.f` solo se cubre aquí.** Ningún otro bloque del módulo trabaja la automatización de instalaciones: si este bloque no se imparte, ese criterio se queda sin evaluar.

## Índice de prácticas

### A · Hardware y requisitos
| # | Práctica | Nivel |
|---|----------|-------|
| B1.1 | [[B1_01_Analisis_de_Hardware\|Análisis de hardware con CPU-Z]] | Básico |
| B1.2 | [[B1_02_Presupuesto_Servidor\|Presupuesto profesional de servidor]] | Intermedio |
| B1.3 | [[B1_03_Elegir_SO_y_Requisitos\|Elegir el SO y comprobar requisitos]] | Básico |

### B · Medios de instalación
| # | Práctica | Nivel |
|---|----------|-------|
| B1.4 | [[B1_04_Descargar_y_Verificar_ISO\|Descargar y verificar la ISO (SHA256)]] | Básico |
| B1.5 | [[B1_05_USB_Booteable_Rufus\|USB booteable con Rufus (+ Secure Boot)]] | Básico |
| B1.6 | [[B1_06_Rufus_vs_Balena\|Comparativa Rufus vs Balena Etcher]] | Intermedio |
| B1.7 | [[B1_07_Multiboot_Ventoy\|Kit multiboot con Ventoy]] | Intermedio |

### C · Disco e instalación
| # | Práctica | Nivel |
|---|----------|-------|
| B1.8 | [[B1_08_Particiones_GParted\|Particiones MBR/GPT con GParted]] *(Linux/Live)* | Intermedio |
| B1.8b | [[B1_08.b_DISKPART\|Gestión de disco con DISKPART]] *(Windows/CLI)* | Intermedio |
| B1.9 | [[B1_09_Laboratorio_Virtualizacion\|Laboratorio de virtualización (VirtualBox/Hyper-V)]] | Intermedio |
| B1.9b | [[B1_09.b_Verificar_Red_con_APIs\|Verificar tu red con APIs públicas]] | Intermedio |
| B1.10 | [[B1_10_Instalacion_Limpia\|Instalación limpia de un SO]] | Intermedio |

### D · Despliegue en red
| # | Práctica | Nivel |
|---|----------|-------|
| B1.11 | [[B1_11_Red_iVentoy\|Instalación por red con iVentoy]] | Avanzado |
| B1.12 | [[B1_12_Instalacion_Desatendida\|Instalación desatendida]] *(opcional)* | Avanzado |

### E · Cierre
| # | Práctica | Nivel |
|---|----------|-------|
| B1.13 | [[B1_13_Proyecto_Final\|Proyecto final de integración]] | Integrador |

### F · Laboratorio de servicios de red: Windows y Windows (B1.16) · Laboratorio 1
**Dos Windows 11 Pro clonados de una máquina base sellada con Sysprep (cada uno con su propio SID), en la Red NAT `B1_LAB` (`192.168.100.0/24`, con DHCP).** Servidor `W11-SRV` con IP fija `192.168.100.10`; cliente `W11-CLI` por DHCP. Cada clon con su usuario de la configuración inicial (`b1w11srv` y `b1w11cli`). Usuarios `juan`, `pedro`, `maria` y `ana`, creados en los dos equipos con la misma contraseña. Cada práctica parte de la instantánea de la anterior.

> [!important] Cole y Casa en B1.16: con una apruebas, con las dos subes nota
> Cada práctica de B1.16 tiene **una sola ficha** con dos ediciones. La **Cole** es la mínima: con ella entregada y bien hecha, la práctica está aprobada. La **Casa** repite el ejercicio entero en tu ordenador, desde cero, y **sube nota**. Si en el aula no te da tiempo, entregar solo la de Casa también vale. Cada edición lleva su vídeo (`B1.16a Cole · …` / `B1.16a Casa · …`) y su entrada (`-cole.md` / `-casa.md`), en la misma playlist `B1_Entorno`.

| # | Práctica | Nivel |
|---|----------|-------|
| B1.16a Básico | [[B1_16.a_Red_Basica_Dos_Windows_11_Basico\|Red básica entre dos Windows 11: importar las dos máquinas de `Limpio`, SID, IP, máscara, puerta de enlace y DNS]] · **obligatoria** | Intermedio |
| B1.16a Avanzado | [[B1_16.a_Red_Basica_Dos_Windows_11_Avanzado\|Lo mismo, fabricando tú las máquinas: base sellada con Sysprep y clones]] · **para subir nota** | Avanzado |
| B1.16b | [[B1_16.b_Carpeta_Compartida_Para_Todos_Windows\|Carpeta compartida para todos]] | Intermedio |
| B1.16c | [[B1_16.c_Permisos_por_Usuario_Windows\|Permisos por usuario en la carpeta compartida]] | Intermedio |
| B1.16d | [[B1_16.d_Impresora_PDF_Compartida_Windows\|Impresora PDF compartida]] | Intermedio |
| B1.16e | [[B1_16.e_Impresora_Solo_para_Pedro_Windows\|Impresora solo para Pedro]] | Intermedio |
| B1.16f | [[B1_16.f_Escritorio_Remoto_Windows\|Escritorio remoto]] | Intermedio |
| B1.16g | [[B1_16.g_Base_Sellada_SID_y_Clonado_Seguro_Windows\|Base sellada, SID y clonado seguro]] | Intermedio |
| — | [[B1_16_Chuletario_Comandos\|Chuletario de comandos de B1.16]] | — |

### G · Laboratorios de red (prólogo de los Bloques 2 y 3) · Laboratorios 2 y 3
**B1.14a prepara una sola VM Ubuntu Server y el acceso SSH desde Windows físico. B1.14b y B1.14c reutilizan ese servidor y añaden un cliente virtual.** En las prácticas de dos VM: crear las máquinas, conectarlas a una red privada del hipervisor, poner IP fija y comprobar el ping en los dos sentidos. **Sin dominio ni servicios de red adicionales al SSH de B1.14a**: eso llega en los Bloques 2 y 3. Plan de red común: servidor `10.10.10.10/24`, cliente `10.10.10.20/24`, red `LAB_RED`.

> [!important] Todos los laboratorios se hacen dos veces: Cole y Casa
> B1.14a, B1.14b, B1.14c, B1.15a y B1.15b tienen una **edición Cole** (equipo del aula) y una **edición Casa** (tu ordenador): son **diez ejercicios distintos**, con la configuración hecha en cada ordenador. **Excepción: Ubuntu Server se instala una sola vez**: en B1.14a Cole se exporta a `B1-UbuntuServer_base.ova` y en B1.14a Casa se importa desde un disco externo (con todas las MAC, disco en exFAT o NTFS y VirtualBox de casa igual o más nuevo). Los clientes se instalan en cada ordenador. Cada ejercicio lleva **su vídeo** (`B1.14a Cole · …`, `B1.14a Casa · …`, etc.) y **su entrada** de apuntes (terminada en `-cole.md` o `-casa.md`). Todos los vídeos van a la **misma playlist**, `B1_Entorno`. Cada práctica continúa la de **esa misma edición**: B1.14b y B1.14c reutilizan el servidor de B1.14a, y B1.15b el de B1.15a, en el mismo ordenador.

| # | Práctica | Nivel |
|---|----------|-------|
| B1.14a Cole | [[B1_14.a_Ubuntu_Server_y_SSH_desde_Windows_Fisico_Cole\|Ubuntu Server y SSH desde Windows físico (prólogo) · Cole]] | Intermedio |
| B1.14a Casa | [[B1_14.a_Ubuntu_Server_y_SSH_desde_Windows_Fisico_Casa\|Ubuntu Server y SSH desde Windows físico (prólogo) · Casa]] | Intermedio |
| B1.14b Cole | [[B1_14.b_Red_VirtualBox_Windows_11_y_Ubuntu_Server_Cole\|Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server) · Cole]] | Intermedio |
| B1.14b Casa | [[B1_14.b_Red_VirtualBox_Windows_11_y_Ubuntu_Server_Casa\|Red de laboratorio en VirtualBox (Windows 11 y Ubuntu Server) · Casa]] | Intermedio |
| B1.14c Cole | [[B1_14.c_Red_VirtualBox_Ubuntu_Desktop_y_Ubuntu_Server_Cole\|Red de laboratorio en VirtualBox (Ubuntu Desktop y Ubuntu Server) · Cole]] | Intermedio |
| B1.14c Casa | [[B1_14.c_Red_VirtualBox_Ubuntu_Desktop_y_Ubuntu_Server_Casa\|Red de laboratorio en VirtualBox (Ubuntu Desktop y Ubuntu Server) · Casa]] | Intermedio |
| B1.15a Cole | [[B1_15.a_Red_HyperV_Windows_11_y_Windows_Server_Cole\|Red de laboratorio en Hyper-V (Windows 11 y Windows Server) · Cole]] | Intermedio |
| B1.15a Casa | [[B1_15.a_Red_HyperV_Windows_11_y_Windows_Server_Casa\|Red de laboratorio en Hyper-V (Windows 11 y Windows Server) · Casa]] | Intermedio |
| B1.15b Cole | [[B1_15.b_Red_HyperV_Ubuntu_Desktop_y_Windows_Server_Cole\|Red de laboratorio en Hyper-V (Ubuntu Desktop y Windows Server) · Cole]] | Intermedio |
| B1.15b Casa | [[B1_15.b_Red_HyperV_Ubuntu_Desktop_y_Windows_Server_Casa\|Red de laboratorio en Hyper-V (Ubuntu Desktop y Windows Server) · Casa]] | Intermedio |

## Herramientas del bloque (todas actuales)
CPU-Z · Rufus · Balena Etcher · **Ventoy** · GParted Live · **DISKPART** · VirtualBox/Hyper-V · **iVentoy** · autoinstall/cloud-init · unattend.xml.

> [!note] Descartado por desfasado/nicho (solo se nombra como "legado")
> YUMI · Serva · MultiBootUSB · Belarc · AIDA64 · Hiren's/Mini XP · inetd. Sustituidos por Ventoy, iVentoy y CPU-Z.

## Fuentes
Material basado en el curso SOR del centro y en aportaciones propias del profesor (verificar ISO, requisitos, laboratorio, instalación limpia, desatendida, Secure Boot).
