# 🧰 Bloque 1 — Preparar el entorno e instalar el SO

> Bloque previo al proyecto **Boochan**: preparar el equipo, crear medios de instalación e instalar sistemas operativos. Todo con herramientas **actuales** (Rufus, Ventoy, iVentoy, GParted) y siguiendo la **metodología de grabación** del curso.

## Metodología (igual que en el resto)
- Cada práctica se **graba entera con OBS**, presentándote y con **timestamps**.
- **Playlist:** `B1_Entorno` · **Vídeo:** `B1.n · título` (No listado) · **una sola entrega**.
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
> | `CE.01.i` | Conectividad servidor–cliente | B1.9b · B1.11 |
> | `CE.05.e` | Automatización de tareas del sistema | B1.12 · B1.13 |
> | `CE.05.f` | Interpretar la configuración del sistema | B1.9b · B1.13 |
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
| B1.8b | [[B1_08b_DISKPART\|Gestión de disco con DISKPART]] *(Windows/CLI)* | Intermedio |
| B1.9 | [[B1_09_Laboratorio_Virtualizacion\|Laboratorio de virtualización (VirtualBox/Hyper-V)]] | Intermedio |
| B1.9b | [[B1_09b_Verificar_Red_con_APIs\|Verificar tu red con APIs públicas]] | Intermedio |
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

## Herramientas del bloque (todas actuales)
CPU-Z · Rufus · Balena Etcher · **Ventoy** · GParted Live · **DISKPART** · VirtualBox/Hyper-V · **iVentoy** · autoinstall/cloud-init · unattend.xml.

> [!note] Descartado por desfasado/nicho (solo se nombra como "legado")
> YUMI · Serva · MultiBootUSB · Belarc · AIDA64 · Hiren's/Mini XP · inetd. Sustituidos por Ventoy, iVentoy y CPU-Z.

## Fuentes
Basado en tu material real del Teams SOR (canales `02.XX`, `t2SOR_Prácticas.pdf`, `01.05`/`01.06`) + aportaciones propias (verificar ISO, requisitos, laboratorio, instalación limpia, desatendida, Secure Boot).
