---
Práctica: B1.3
Bloque: 01_Entorno
Nivel: 1
Nivel_nombre: Básico
RA: RA1
CE: 1.a, 1.b
Playlist: B1_Entorno
Vídeo: B1.3 · Elegir el SO y comprobar requisitos
---

## B1.3 — Elegir el sistema operativo y comprobar requisitos

> [!abstract] Ficha de la práctica
> ### 📌 `B1.3` — Elegir el SO y comprobar requisitos
> - **Bloque 1** (Preparar el entorno) · **Nivel 1** (Básico) · **RA1** · **CE 1.a, 1.b**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.3 · Elegir el SO y comprobar requisitos`

> [!info] Caso real (contexto profesional)
> Con el hardware ya inventariado (B1.1), toca decidir **qué sistema operativo servidor** instalar en cada equipo: **Windows Server** o **Ubuntu Server**, y en qué edición. La decisión no es de gusto: depende de los requisitos, del papel del servidor y del presupuesto de licencias.

- **🎯 Objetivo real:** elegir el SO servidor adecuado y comprobar que el equipo cumple sus requisitos mínimos.
- **🧩 Problema que resuelve:** instalar un SO que el equipo no mueve, o pagar licencias que no hacen falta.

---

## 📚 Fundamento

> [!info] Antes de empezar: Windows Server vs Ubuntu Server
> - **Windows Server 2025:** de pago (licencia por núcleos + CALs). Muy usado en empresas con Active Directory nativo. Dos modos: **Server Core** (solo terminal, ligero, más seguro) y **con Experiencia de Escritorio** (interfaz gráfica, más consumo).
> - **Ubuntu Server 24.04 LTS:** gratuito, sin interfaz gráfica por defecto (requisitos mínimos), soporte LTS de años. Ideal para servicios Linux, contenedores y como controlador de dominio con Samba.

> [!tip] Idea clave
> **El SO se elige por el trabajo, no por la moda.** Un servidor de archivos con AD nativo pide Windows Server; un servidor de servicios Linux o de bajo coste pide Ubuntu Server. Y **Server Core** casi siempre es mejor que la GUI en producción: menos recursos y menos superficie de ataque.

> [!example] Vocabulario de esta práctica
> - **Edición / SKU:** variante del SO (Standard, Datacenter…).
> - **Server Core vs Escritorio:** sin GUI (terminal) vs con GUI.
> - **LTS (Long Term Support):** versión con soporte prolongado (Ubuntu).
> - **Requisitos mínimos:** CPU, RAM y disco que el SO necesita para arrancar.
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> 1. **Paso 0:** léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-3-elegir-el-so-y-comprobar-requisitos.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura de la Fase 0.1 y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE** mostrando tu identidad (Teams o correo `@alu.edu.gva.es`). Di qué vas a hacer.
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.3 · Elegir el SO y comprobar requisitos`** y súbelo a **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `Enlace al vídeo explicativo`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, arranca OBS y preséntate.

> [!example] Paso 1 — Consulta los requisitos oficiales
> Busca en las webs oficiales los **requisitos mínimos** de:
> - **Windows Server 2025** (microsoft.com).
> - **Ubuntu Server 24.04 LTS** (ubuntu.com).
> Anota CPU, RAM y disco de cada uno.

> [!example] Paso 2 — Compara con tu inventario (B1.1)
> Coge la **tabla de inventario** de la práctica B1.1 y comprueba, para tu equipo, si cumple los requisitos de cada SO. Marca ✅/❌.

> [!example] Paso 3 — Decide edición y modo
> Justifica en un breve informe:
> - ¿Windows Server o Ubuntu Server? ¿Por qué (papel del servidor, coste)?
> - Si Windows: ¿**Server Core** o Escritorio? ¿Standard o Datacenter?
> - Si Ubuntu: ¿versión LTS concreta?

> [!example] Paso 4 — Elabora la tabla de decisión
> | SO candidato | Requisitos que pide | ¿El equipo cumple? | Decisión y motivo |
> | :--- | :--- | :--- | :--- |
> | Windows Server 2025 | … | ✅/❌ | … |
> | Ubuntu Server 24.04 | … | ✅/❌ | … |

> [!example] Paso 5 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.3 · Elegir el SO y comprobar requisitos`**, súbelo a **`B1_Entorno`** y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | Elegir GUI "por comodidad" en un servidor | Más consumo y menos seguridad | Valora **Server Core** salvo que necesites la GUI. |
> | Ignorar el coste de licencias | Presupuesto irreal | Windows Server se paga por núcleos + CALs. |
> | No comprobar el disco mínimo | La instalación falla | Compara el disco del inventario con el requisito. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Tienes una **tabla de decisión** con requisitos, cumplimiento y motivo.
> - Sabes justificar **por qué** ese SO y esa edición/modo.
> - El vídeo está en la playlist `B1_Entorno` con timestamps.

> [!question] Comprueba que lo has entendido
> 1. ¿Qué ventajas tiene **Server Core** frente a la Experiencia de Escritorio?
> 2. ¿Por qué Ubuntu Server pide menos requisitos que Windows Server?
> 3. ¿De qué depende que elijas un SO u otro?

---

## ✅ Entregables y cierre

- **Entregable documento:** informe con la **tabla de decisión** de SO.
- **Entregable vídeo:** `B1.3 · Elegir el SO y comprobar requisitos` en `B1_Entorno`. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** decisión justificada + comprobación de requisitos contra el inventario.
- **Entregable apuntes:** `b1-3-elegir-el-so-y-comprobar-requisitos.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A diferenciar **Windows Server** y **Ubuntu Server** y sus ediciones/modos.
> - A comprobar **requisitos mínimos** contra el hardware real.
> - A **justificar** una elección técnica.
>
> **Siguiente:** B1.4 — Descargar y verificar la ISO (SHA256).
