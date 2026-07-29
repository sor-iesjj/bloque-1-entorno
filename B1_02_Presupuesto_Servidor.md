---
Práctica: B1.2
Bloque: 01_Entorno
Nivel: 2
Nivel_nombre: Intermedio
RA: RA1
CE: 1.a, 1.b
Playlist: B1_Entorno
Vídeo: B1.2 · Presupuesto profesional de un servidor
---

## B1.2 — Elaboración de un presupuesto profesional de servidor

> [!abstract] Ficha de la práctica
> ### 📌 `B1.2` — Presupuesto profesional de un servidor
> - **Bloque 1** (Preparar el entorno) · **Nivel 2** (Intermedio) · **RA1** · **CE 1.a, 1.b**
> - **🎬 Playlist:** `B1_Entorno`
> - **📹 Nombre del vídeo:** `B1.2 · Presupuesto profesional de un servidor`

> [!info] Caso real (contexto profesional)
> Una empresa te pide un **presupuesto técnico-económico** para montar un servidor de altas prestaciones. No vale poner "un ordenador potente": hay que elegir **componentes reales, actuales y compatibles entre sí**, justificarlos y calcular el coste total con una plantilla profesional.

- **🎯 Objetivo real:** especificar y presupuestar un servidor empresarial con componentes de última generación, y presentarlo en un documento profesional con cálculos automáticos.
- **🧩 Problema que resuelve:** sin saber elegir y dimensionar componentes, no se puede asesorar a un cliente ni justificar una inversión.

---

## 📚 Fundamento

> [!info] Antes de empezar: qué lleva un servidor de verdad
> Un servidor no es un PC grande: usa componentes pensados para **funcionar 24/7 y en paralelo**. Placa base de **doble socket**, procesadores **Intel Xeon Scalable** o **AMD EPYC**, memoria **DDR5 ECC** (corrige errores), almacenamiento **SSD NVMe** de alta resistencia y **fuentes redundantes**. Elegir bien es equilibrar rendimiento, fiabilidad y coste.

> [!tip] Idea clave
> **Compatibilidad primero.** El procesador debe encajar en el socket de la placa; la RAM debe ser del tipo que la placa admite (DDR5 ECC RDIMM); el número de módulos debe aprovechar los canales de memoria. Un componente "mejor" pero incompatible no vale nada.

> [!example] Vocabulario de esta práctica
> - **ECC (Error-Correcting Code):** memoria que detecta y corrige errores; obligatoria en servidores.
> - **NVMe:** disco SSD conectado por PCIe, mucho más rápido que SATA.
> - **Fuente redundante:** dos fuentes; si una falla, la otra mantiene el servidor encendido.
> - **Fórmulas en Word:** una tabla de Word puede calcular subtotales y totales automáticamente (campos `=`).
> - **OBS · Playlist · Timestamp:** grabación · playlist `B1_Entorno` · marca de tiempo por paso.

---

## 📹 Grabación de esta práctica

> [!important] Obligaciones de grabación (LÉEME — es igual en TODAS las prácticas del bloque)
> Esta práctica se **graba entera con OBS**, de principio a fin. Aquí necesitas **tres momentos grabados** (búsqueda de componentes, creación de la plantilla, cálculo final).
> 1. **Prepárate primero** (Paso 0): léete el ejercicio y ten a mano OBS y tu identificación. **Crea la entrada de apuntes de esta práctica** en Obsidian: fichero `b1-2-presupuesto-profesional-de-un-servidor.md` dentro de `00_Apuntes/Trimestre_N/B1_Entorno/`, con la estructura de la Fase 0.1 y **vacía**. Rellenarla es cosa tuya, después.
> 2. **Arranca OBS y PRESÉNTATE:** *"Hola, me llamo [Nombre], 2.º SMR, y en este vídeo hago la práctica B1.2 — Presupuesto de servidor."* Muestra tu identidad (Teams o correo `@alu.edu.gva.es`).
> 3. **Timestamps SIEMPRE:** `00:00 Presentación` y uno por paso.
> 4. **Al terminar:** nombra el vídeo **`B1.2 · Presupuesto profesional de un servidor`** y súbelo a la playlist **`B1_Entorno`** (No listado). Y **pega su enlace dentro de tu entrada de apuntes**, en el apartado `Enlace al vídeo explicativo`.
> 5. **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.

---

## 🛠️ Procedimiento

> [!example] Paso 0 — Prepárate y empieza a grabar
> Léete el ejercicio, ten OBS y tu identificación a mano, **arranca la grabación** y **preséntate**.

> [!example] Paso 1 — Define los requisitos del servidor
> Tu servidor debe cumplir **como mínimo**:
> - **Placa base** de doble socket, compatible con Intel Xeon Scalable o AMD EPYC, con soporte para ≥ 64 GB DDR5 ECC y ≥ 2 ranuras **PCIe 5.0**.
> - **2 procesadores** de última generación, mínimo 4 núcleos (recomendado 8). *Ejemplo:* AMD EPYC 9124 (8 núcleos, DDR5, PCIe 5.0).
> - **RAM:** mínimo 64 GB DDR5 ECC Registered (p. ej. 4 × 16 GB para aprovechar canales).
> - **Almacenamiento:** SSD NVMe de alta capacidad (p. ej. 4 × Samsung PM9A3 7.68 TB).
> - **Fuente:** redundante 1600 W Platinum.
> - **Refrigeración:** líquida de alto rendimiento (o inmersión, como valor añadido).
> - **GPU (opcional):** NVIDIA RTX A4000 / H100 si se requiere IA o virtualización acelerada.

> [!example] Paso 2 — Busca los componentes en webs oficiales *(grabar — Vídeo 1)*
> Busca **precios reales** en webs de fabricante y tiendas (PCComponentes, Amazon, fabricante). Anota modelo exacto y precio de cada componente.

> [!example] Paso 3 — Crea la plantilla de presupuesto en Word *(grabar — Vídeo 2)*
> Crea una tabla con columnas: **componente · descripción técnica · cantidad · precio unitario · subtotal**. Añade **fórmulas automáticas** para los subtotales y el **total final**. Da estilo corporativo: logotipo, encabezado y pie de página.

> [!example] Paso 4 — Rellena y calcula *(grabar — Vídeo 3)*
> Introduce los datos de los componentes, comprueba que los **subtotales y el total** se calculan solos, y obtén el **coste total** del servidor.

> [!example] Paso 5 — Cierra la grabación y súbela
> Detén OBS, nombra el vídeo **`B1.2 · Presupuesto profesional de un servidor`**, súbelo a **`B1_Entorno`** (No listado) y añade timestamps.

---

## 🚩 Errores y verificación

> [!warning] Errores típicos (evítalos)
> | Error | Qué pasa | Cómo evitarlo |
> | :--- | :--- | :--- |
> | CPU y placa con socket distinto | El presupuesto es inviable | Comprueba que el socket de la CPU coincide con el de la placa. |
> | RAM no ECC en un servidor | No cumple requisitos profesionales | Usa siempre DDR5 **ECC** en servidor. |
> | Total escrito a mano | Errores de cálculo | Usa **fórmulas** en la tabla de Word. |

> [!success] ✅ Verificación: ¿está bien hecho?
> - Todos los componentes son **reales, actuales y compatibles**.
> - La plantilla calcula subtotales y total **automáticamente**.
> - Los 3 vídeos (búsqueda, plantilla, cálculo) están en la playlist `B1_Entorno`.

> [!question] Comprueba que lo has entendido
> 1. ¿Por qué un servidor usa memoria **ECC** y un PC normal no?
> 2. ¿Qué ventaja da una **fuente redundante**?
> 3. ¿Por qué conviene poner **4 módulos** de RAM en vez de 1 del mismo total?

---

## ✅ Entregables y cierre

- **Entregable documento:** presupuesto en **Word** con plantilla, fórmulas y estilo corporativo.
- **Entregable vídeo:** `B1.2 · Presupuesto profesional de un servidor` en la playlist `B1_Entorno` (con los 3 momentos grabados y timestamps). **Se graba una sola vez** (no se duplica casa/centro). **La entrega va por la TAREA de Teams:** abriré una tarea que cubrirá **esta práctica y otras**; te llegará notificación con fecha límite. Ahí pegarás el enlace de tu **repositorio de apuntes** — los vídeos ya están dentro de tus entradas.
- **Criterio de éxito:** componentes compatibles y actuales + total calculado automáticamente + vídeo subido.
- **Entregable apuntes:** `b1-2-presupuesto-profesional-de-un-servidor.md` en `B1_Entorno/`, con la estructura completa, las **respuestas a las preguntas de «Comprueba que lo has entendido»** y el **enlace del vídeo** dentro. Subida al repo con `git add` → `commit` → `push`.

> [!danger] ⚠️ Las respuestas van en la ENTRADA, no sueltas
> Las preguntas de esta práctica no son decorativas: son lo que demuestra que has entendido lo que hiciste, y no solo que supiste seguir los pasos. Se contestan **con tus palabras** en el apartado `Respuesta a las preguntas` de tu entrada.
> Una práctica con el vídeo perfecto y las preguntas en blanco está **incompleta**.

> [!summary] 🎓 Qué has aprendido en este ejercicio
> - A **elegir y justificar** componentes reales de un servidor profesional.
> - A comprobar **compatibilidad** (socket, tipo de RAM, canales).
> - A crear una **plantilla de presupuesto** con cálculos automáticos.
>
> **Siguiente:** B1.3 — Elegir el sistema operativo y comprobar requisitos.
