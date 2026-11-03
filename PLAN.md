# PLAN.md — Construcción del libro de laboratorios IDI 3185

**Audiencia de este documento:** ayudante experto en Unity/XR, apoyado por una IA de código (Claude Code, Cursor, Copilot o equivalente), que ejecutará el plan descrito aquí.

**Rol del ayudante experto (constructor del libro):** construir el libro, la infraestructura, los módulos y las soluciones durante nov-dic 2026. **No es la misma persona que el ayudante del laboratorio** (ver sección 2.7).

**Objetivo:** construir un libro de laboratorios prácticos (tutoriales) para el curso **IDI 3185 Realidad Extendida** de la Pontificia Universidad Católica de Chile (DILAB-UC), listo para su primera edición en el semestre 2027-1.

**Ventana de trabajo:** 3 de noviembre al 15 de diciembre de 2026 (6 semanas, 12 horas semanales = 72 horas totales).

**Mantener este documento como fuente de verdad.** Cualquier decisión de diseño que no esté acá debe consultarse con el profesor antes de implementar.

---

## 1. Contexto del curso y propósito del libro

### 1.1. Sobre el curso

IDI 3185 es un curso de posgrado del programa de Diseño/Ingeniería de la PUC que introduce a estudiantes al desarrollo de experiencias de realidad extendida (XR), cubriendo realidad virtual (VR), realidad aumentada (AR) y realidad mixta (MR). El curso combina clases teóricas, clases invertidas conducidas por estudiantes, un proyecto de desarrollo individual (3 hitos) y actividades prácticas complementarias.

Cada edición del curso tiene entre 5 y 20 estudiantes (típicamente 10-15), organizados individualmente para el proyecto principal.

### 1.2. Problema que el libro resuelve

Hasta ahora, el curso no cuenta con material práctico sistemático que acompañe la cátedra. Los estudiantes aprenden a desarrollar XR principalmente a través del proyecto individual, lo que genera una curva de aprendizaje empinada y poca estructura.

El libro de laboratorios busca:

- Proveer tutoriales prácticos autoguiados que acompañen los contenidos teóricos de cátedra.
- Habilitar aprendizaje autónomo con validación objetiva (tests automatizados).
- Distribuir el uso del hardware limitado del laboratorio evitando cuellos de botella.
- Dejar una infraestructura replicable para futuras ediciones del curso.

### 1.3. Hardware disponible en el laboratorio

**Hardware principal (soportado por los módulos):**

- 2 Apple Vision Pro
- 2 Meta Quest 3
- 3 Meta Quest 2
- 1 iPad (compatible con ARKit)

**Hardware alternativo (mencionado en el libro, no es target principal):**

- 1 HTC Vive Pro (requiere PC potente del estudiante; mencionado como alternativa para quienes dispongan de ese setup).
- 1 HoloLens 1 (bonus histórico, documentación limitada).

Los estudiantes pueden usar su propio smartphone (iOS o Android) para el bloque AR como alternativa al iPad del laboratorio. No es obligatorio.

### 1.4. Alineación con cátedra

El curso tiene 15 semanas con el siguiente calendario base (edición 2026-2, referencia):

| Semana | Tema de cátedra |
|---|---|
| 1 | Introducción e Historia |
| 2 | Actividad práctica |
| 3 | Hardware |
| 4 | Interacción (grabada) |
| 5 | Entrega Proyecto 1 |
| — | NO HAY CLASES |
| 6 | Percepción |
| 7 | Calibración, Visión por Computadora para AR (grabada) |
| 8 | Presentación Papers (remota) |
| 9 | Entrega Proyecto 2 |
| 10 | Desarrollo Centrado en el Humano (remota) |
| 11 | Analíticas Inmersivas y Visualización Situada |
| 12 | Efectos Adversos para la Salud y Evaluación en XR |
| 13 | Tracking para VR/AR y Coherencia visual |
| 14 | Examen |
| 15 | Entrega Proyecto 3 |

El libro NO debe referir fechas fijas sino número de semana (el calendario cambia cada edición).

---

## 2. Decisiones de diseño (todas tomadas, no reabrir)

### 2.1. Arquitectura pedagógica

- **Formato del libro:** sitio web generado con MkDocs (tema Material), publicado en GitHub Pages.
- **21 módulos de 1 hora** cada uno, organizados en:
  - **Preludio** (2 módulos obligatorios para todos): M0, M1.
  - **Bloque VR** (6 módulos): V1, V2, V3, V4, V5a, V5b.
  - **Bloque AR** (6 módulos): A1, A2, A3, A4, A5a, A5b.
  - **Bloque MR** (6 módulos): X1, X2, X3, X4, X5a, X5b.
  - **Bonus** (1 módulo opcional): HoloLens 1 con MRTK.

### 2.2. Estructura de obligatoriedad (Opción C: secuencia rotativa + especialización)

Todos los estudiantes pasan por los tres bloques antes de especializarse. Esto garantiza exposición transversal a VR, AR y MR, y distribuye naturalmente la carga sobre el hardware.

**Módulos obligatorios para TODOS los estudiantes:**

1. M0 (IA en XR).
2. M1 (Nivelación Unity + XRI).
3. V1 (Escena VR básica) — muestra del bloque VR.
4. A1 (AR Foundation básico) — muestra del bloque AR.
5. X1 (PolySpatial básico) — muestra del bloque MR.

Total obligatorio: 5 módulos = 50 pts.

**Módulos de especialización (10 pts cada uno):**

Tras completar la muestra de los tres bloques, el estudiante elige en qué bloque profundizar. Puede seguir los módulos del bloque elegido en orden (V2, V3, V4, V5a, V5b, por ejemplo) o mezclar módulos de distintos bloques. Cada módulo aprobado suma 10 pts hasta el máximo del libro.

**Umbral de aprobación:** 60 pts. Puntos sobre 60 son extra en la nota del curso.

**Puntaje máximo:**
- 5 obligatorios × 10 = 50 pts.
- 15 módulos restantes (V2-V5b, A2-A5b, X2-X5b) × 10 = 150 pts máximo teórico.
- Bonus HL = 10 pts.
- En la práctica nadie los hace todos. 60 pts típico, 100 pts aspiracional, >100 opcional.

### 2.3. Ritmo y horario

- **Horario de referencia: la ayudantía semanal (1 hora).** Hay un ayudante del laboratorio presente para apoyar.
- **Un módulo por semana recomendado.** El libro muestra una "semana recomendada" por módulo, alineada con la cátedra.
- **Flexibilidad:** el estudiante que falta a una ayudantía puede recuperar el módulo por su cuenta. No hay sanción por asistencia, sí por módulos no entregados al final del semestre.
- **Avance adelantado permitido:** un estudiante puede ir más rápido que el calendario sugerido, hasta donde el hardware lo permita (ver sección 2.5).

### 2.4. Validación en dispositivo

Cada módulo tiene dos checkpoints:

- **Checkpoint A — Setup inicial** (5-10 min, simulador o dispositivo).
- **Checkpoint B — Validación de resultado** (10-15 min, simulador o dispositivo).

**Regla obligatoria:** para que los puntos de un bloque (VR/AR/MR) cuenten en su totalidad, al menos UNA validación debe haber sido en dispositivo real (no simulador) durante los módulos de ese bloque. Esto fuerza al estudiante a usar hardware real en algún momento del bloque.

Cuestionarios estandarizados (NASA-TLX corto, SUS adaptado) se usan en los checkpoints con dispositivo real donde la experiencia perceptual sea evaluable.

### 2.5. Stack técnico

- **Motor:** Unity 6 LTS.
- **Toolkits:**
  - VR: XR Interaction Toolkit (XRI). Target principal: Meta Quest 2/3. HTC Vive Pro mencionado como alternativa compatible con el mismo stack (no es target de los tests ni de los builds).
  - AR: AR Foundation (ARKit para iOS, ARCore para Android — rutas paralelas en los módulos AR).
  - MR: PolySpatial (Vision Pro) y XRI con passthrough (Quest 3).
- **Simuladores:**
  - VR: XR Device Simulator (del XRI) y/o Meta XR Simulator.
  - AR: XR Simulation (de AR Foundation).
  - MR: PolySpatial Play to Device para Vision Pro; XR Device Simulator para Quest 3 passthrough.
- **Lenguaje:** C#.
- **Idioma del contenido pedagógico:** español. Código, nombres de clases y comentarios: inglés.
- **Tests automatizados:** Unity Test Framework (NUnit) con tests en EditMode y PlayMode.

### 2.6. Infraestructura

- **Repo principal:** `github.com/leonelmerino/idi3185-xr-labs` (privado inicialmente; puede abrirse al público más adelante).
- **Repo de soluciones:** `github.com/leonelmerino/idi3185-xr-labs-solutions` (privado permanente; acceso bajo demanda vía Issue en el repo principal). Incluye también notas pedagógicas para el ayudante del laboratorio.
- **Modelo de contribución estudiantil:** rama por estudiante en el repo principal (NO fork). Convención: `student/<usuario-github>/<modulo-id>`.
- **CI:** GitHub Actions ejecuta los tests al abrir PR; pass/fail decide si los puntos del módulo cuentan.
- **Builds públicos:** GitHub Releases del repo principal, con tag por módulo (`v1.0-M0`, `v1.0-V1`, etc.). Permiten al estudiante probar la experiencia resuelta sin acceso al código solución.
- **Script generador de edición:** herramienta Python que, dado año y lista de estudiantes, crea nuevo repo de edición, agrega estudiantes como colaboradores, inicializa estructura, configura CI.

### 2.7. Roles

Hay tres roles distintos que no deben confundirse:

1. **Profesor (Leonel Merino).** Dueño de las decisiones pedagógicas. Revisa el módulo piloto como gate. Aprueba la versión final del libro.

2. **Ayudante experto (constructor del libro).** Persona a cargo de construir el libro, la infraestructura, los módulos y las soluciones durante nov-dic 2026. Trabaja con la IA de código. Dedica ~12 h/semana durante 6 semanas. Esta es la audiencia de este `PLAN.md`.

3. **Ayudante del laboratorio (acompaña a los estudiantes en 2027-1).** Persona que estará en la hora semanal de ayudantía para resolver dudas cuando los estudiantes se bloquean. Los estudiantes conducen la actividad por sí mismos; el ayudante interviene cuando se traban. Esta persona también evalúa los PRs y gestiona las solicitudes de acceso a soluciones. **Para esta persona se construye material de apoyo específico en el repo privado de soluciones** (notas por módulo, errores comunes, cómo guiar sin dar la respuesta).

El ayudante experto y el ayudante del laboratorio pueden o no ser la misma persona. El libro y la infraestructura están diseñados para que no lo sean por defecto.

### 2.8. Licencias

- Contenido pedagógico (markdown, imágenes, diagramas del libro): **Creative Commons BY-SA 4.0**.
- Código, scripts, tests: **MIT**.
- Archivo raíz: `LICENSE` con MIT; archivo `LICENSE-CONTENT` con CC BY-SA 4.0; `README.md` explicita el doble esquema.

### 2.9. Modelo de "respuesta correcta"

- Las soluciones viven en el repo privado `idi3185-xr-labs-solutions`.
- Un estudiante que no logra completar un módulo puede abrir un Issue en el repo principal pidiendo acceso a la solución. El ayudante del laboratorio responde otorgándole acceso de solo lectura al repo de soluciones, caso a caso.
- Los builds pre-compilados de las soluciones son PÚBLICOS vía GitHub Releases del repo principal. Cualquiera puede descargarlos y validar la experiencia esperada.

---

## 3. Arquitectura del repositorio principal

### 3.1. Estructura de carpetas

```
idi3185-xr-labs/
├── README.md                      # Descripción del repo, licencias, cómo empezar
├── LICENSE                        # MIT para código
├── LICENSE-CONTENT                # CC BY-SA 4.0 para contenido
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md                # Cómo contribuir (para estudiantes)
├── .gitignore                     # Unity + Python + MkDocs
├── mkdocs.yml                     # Configuración del libro
├── docs/                          # Fuente del libro MkDocs
│   ├── index.md                   # Portada
│   ├── como-usar-el-libro.md
│   ├── preludio/
│   │   ├── m0-ia-en-xr.md
│   │   └── m1-unity-xri-nivelacion.md
│   ├── bloque-vr/
│   │   ├── v1-escena-basica.md
│   │   ├── v2-interaccion-objetos.md
│   │   ├── v3-ui-espacial.md
│   │   ├── v4-locomocion-avanzada.md
│   │   ├── v5a-mini-experiencia.md
│   │   └── v5b-evaluacion.md
│   ├── bloque-ar/
│   │   ├── a1-ar-foundation-basico.md
│   │   ├── a2-image-tracking.md
│   │   ├── a3-oclusion-iluminacion.md
│   │   ├── a4-mesh-scanning.md
│   │   ├── a5a-mini-experiencia.md
│   │   └── a5b-evaluacion.md
│   ├── bloque-mr/
│   │   ├── x1-polyspatial-basico.md
│   │   ├── x2-mirada-pellizco.md
│   │   ├── x3-anclajes-persistentes.md
│   │   ├── x4-visualizacion-situada.md
│   │   ├── x5a-mini-experiencia.md
│   │   └── x5b-evaluacion.md
│   ├── bonus/
│   │   └── hl-hololens-mrtk.md
│   ├── apendices/
│   │   ├── setup-entorno.md
│   │   ├── uso-de-ia.md
│   │   ├── hardware-alternativo.md     # HTC Vive Pro, PC propio, teléfonos personales
│   │   ├── calendario-sugerido.md      # Semana recomendada por módulo
│   │   └── troubleshooting.md
│   └── assets/
│       ├── images/
│       └── diagrams/
├── unity-template/                # Proyecto Unity base para los módulos
│   ├── Assets/
│   │   ├── Scripts/
│   │   ├── Scenes/
│   │   ├── Prefabs/
│   │   ├── Tests/
│   │   │   ├── EditMode/
│   │   │   └── PlayMode/
│   │   └── Settings/
│   ├── Packages/
│   │   └── manifest.json
│   ├── ProjectSettings/
│   └── README.md
├── modules/                       # Un folder por módulo con material específico
│   ├── m0/
│   │   ├── README.md              # Enunciado del módulo
│   │   ├── acceptance.md          # Criterios de aceptación detallados
│   │   ├── starter/               # Código inicial que el estudiante clona
│   │   ├── tests/                 # Tests que validan la solución
│   │   └── rubric.yml             # Rúbrica estructurada (puntaje por criterio)
│   ├── m1/
│   ├── v1/
│   ├── ...
│   └── hl/
├── scripts/                       # Scripts Python de gestión
│   ├── create_edition.py          # Genera repo de nueva edición
│   ├── add_students.py            # Agrega estudiantes como collaborators
│   ├── grade_dashboard.py         # Dashboard de puntos por estudiante
│   ├── validate_module.py         # Ejecuta tests de un módulo localmente
│   ├── requirements.txt
│   └── README.md
├── .github/
│   ├── workflows/
│   │   ├── mkdocs-deploy.yml      # Publica docs en GitHub Pages
│   │   ├── module-tests.yml       # Corre tests cuando hay PR a rama student/*
│   │   └── release-builds.yml     # Publica builds en Releases al tag v*
│   ├── ISSUE_TEMPLATE/
│   │   ├── solution-request.md    # Pide acceso a solución de un módulo
│   │   ├── bug-report.md
│   │   └── module-feedback.md
│   └── pull_request_template.md
└── PLAN.md                        # Este documento (se queda en el repo)
```

### 3.2. Estructura del repositorio de soluciones

```
idi3185-xr-labs-solutions/
├── README.md                      # Advertencia: no mirar sin haber intentado
├── LICENSE                        # MIT
├── solutions/
│   ├── m0/
│   │   ├── README.md              # Explicación de las decisiones de la solución
│   │   ├── src/                   # Código resuelto
│   │   ├── tests-passed.log       # Evidencia de que la solución pasa los tests
│   │   ├── build-link.md          # Link al build en Releases del repo principal
│   │   └── notes-for-lab-assistant.md   # Material de apoyo para el ayudante del lab
│   ├── m1/
│   ├── v1/
│   ├── ...
│   └── hl/
├── lab-assistant-handbook.md      # Guía general para el ayudante del laboratorio
└── CONTRIBUTING.md                # Cómo mantener soluciones alineadas con el libro
```

**Formato de `notes-for-lab-assistant.md` por módulo:**

```markdown
# Notas de apoyo — <ID> <Título>

## Qué debe entender el estudiante al terminar

<Resumen en 2-3 líneas del aprendizaje esperado.>

## Errores comunes

1. **<Error común 1>.** Síntoma: <X>. Causa típica: <Y>. Pista a dar (sin resolver): <Z>.
2. **<Error común 2>.** ...

## Preguntas típicas y respuestas sugeridas

- "¿Por qué no me detecta el XR Rig?" → Pista sin dar la respuesta.
- ...

## Puntos de bloqueo donde intervenir activamente

<Si el estudiante lleva más de 15 min en X, interviene con esta pista.>

## Qué NO decir todavía

<Conceptos que el estudiante descubrirá en módulos posteriores; no spoilearlos.>
```

---

## 4. Especificación de los 21 módulos

Cada módulo sigue la misma plantilla. **Consulte la sección 5 para la plantilla detallada**.

Las columnas de la tabla:

- **ID:** identificador del módulo.
- **Título:** nombre pedagógico.
- **Nivel:** básico / intermedio / avanzado.
- **Dispositivo:** hardware objetivo (puede validarse en simulador según sec. 2.4).
- **Obligatoriedad:** obligatorio para todos / electivo (ver sec. 2.2).
- **Semana recomendada:** número de semana de cátedra en la que encaja mejor.

### 4.1. Preludio

| ID | Título | Nivel | Dispositivo | Obligatoriedad | Semana |
|---|---|---|---|---|---|
| M0 | Desarrollo asistido por IA en XR | — | Computador propio | Obligatorio | 1 |
| M1 | Nivelación Unity + XRI Simulator | — | Computador propio | Obligatorio | 2 |

**M0 — Desarrollo asistido por IA en XR.** Fundamentos de uso efectivo de asistentes de IA en desarrollo de software: cómo escribir prompts productivos, cómo iterar, cuándo pedir código vs explicación, cómo verificar lo generado, uso responsable (autoría, trazabilidad, no entregar código no comprendido). Herramientas cubiertas: Claude Code o Cursor como asistente principal, Copilot como complemento. Mención breve de MCP y agentes custom con enlace a lectura adicional (no evaluado como contenido del módulo). Ejercicio práctico: resolver un bug intencional en una escena Unity simple usando el asistente, documentando el proceso en un archivo `ai-log.md`.

**M1 — Nivelación Unity + XRI Simulator.** Mínimo indispensable de C# (classes, components, MonoBehaviour lifecycle, eventos, UnityEvents, serialización en inspector) presentado inline a medida que se usa. Creación de un proyecto Unity 6 LTS vacío. Configuración de paquetes básicos. Creación de una escena, instalación del XR Interaction Toolkit, agregar un XR Origin (XR Rig), configuración del XR Device Simulator. Mover el rig con mouse+teclado, hacer un raycast desde el controlador virtual, instanciar un cubo y agarrarlo. Ejercicio final: configurar el proyecto desde cero y pasar los tests que verifican la estructura.

### 4.2. Bloque VR

| ID | Título | Nivel | Dispositivo | Obligatoriedad | Semana |
|---|---|---|---|---|---|
| V1 | Escena VR básica: locomoción, teletransporte, raycast | Básico | Quest 2/3 | Obligatorio (muestra) | 3 |
| V2 | Interacción con objetos: grab, physics, two-hand | Intermedio | Quest 2/3 | Electivo | 6 |
| V3 | UI espacial y feedback multimodal | Intermedio | Quest 2/3 | Electivo | 10 |
| V4 | Locomoción avanzada y mitigación de cibermareo | Avanzado | Quest 2/3 | Electivo | 12 |
| V5a | Mini-experiencia VR: implementación | Avanzado | Quest 2/3 | Electivo | 13 |
| V5b | Mini-experiencia VR: evaluación con usuario | Avanzado | Quest 2/3 | Electivo | 13 |

**V1 — Escena VR básica.** Crear una escena con suelo, obstáculos simples, iluminación por defecto. Agregar un XR Origin con continuous move + teleport provider. Implementar un ray interactor que detecta superficies de teletransporte (marcadas con layer). Validar: el usuario puede moverse continuamente, puede teletransportarse apuntando a zonas marcadas. Tests: existencia de componentes XR, al menos un TeleportationArea, interactor configurado.

**V2 — Interacción con objetos.** Agregar grabbable objects con Rigidbody y XRGrabInteractable. Implementar un objeto que requiere dos manos (two-hand grab) usando los eventos del XRI. Agregar física realista (masa, drag). Validar: usuario puede agarrar objetos con una mano, el objeto two-hand requiere ambos controladores. Tests: componentes correctos, respuesta a eventos de grab.

**V3 — UI espacial y feedback multimodal.** Crear un menú espacial con Canvas en World Space, interactuable con ray o poke. Agregar hover visual (color change), audio feedback en clicks, vibración háptica en interacciones. Validar: menú legible desde distancias razonables, respuesta inmediata a input, feedback multisensorial. Tests: configuración del canvas, hooks de eventos.

**V4 — Locomoción avanzada y mitigación de cibermareo.** Implementar snap turn (en lugar de smooth turn) y vignette durante movimiento continuo. Comparar las dos técnicas en una escena de prueba con túnel y obstáculos. Validar en dispositivo con cuestionario SSQ corto autoreportado. Tests: ambas técnicas presentes, parámetros configurables.

**V5a — Mini-experiencia VR: implementación.** Integrar lo visto (locomoción, grab, UI, feedback) en una mini-experiencia coherente de 3-5 minutos de duración. Debe tener un objetivo claro para el usuario (ej: completar una tarea en un escape room muy simple). Tests: escena integrada, flujo de inicio-fin funcional.

**V5b — Mini-experiencia VR: evaluación con usuario.** Reclutar a un usuario externo (compañero de curso, amigo), aplicar la mini-experiencia, administrar SUS corto y SSQ, documentar observaciones. Entregar: reporte breve markdown con 3 hallazgos y 1 mejora propuesta. Tests: existencia del reporte, estructura mínima.

### 4.3. Bloque AR

Rutas paralelas iOS/Android: el contenido conceptual es el mismo; cambian las instrucciones de build y configuración de ARKit vs ARCore.

| ID | Título | Nivel | Dispositivo | Obligatoriedad | Semana |
|---|---|---|---|---|---|
| A1 | AR Foundation: detección de planos y anclaje | Básico | iPhone/iPad/Android | Obligatorio (muestra) | 7 |
| A2 | Image tracking y objetos sobre marcadores | Intermedio | iPhone/iPad/Android | Electivo | 7 |
| A3 | Oclusión, iluminación estimada y coherencia visual | Intermedio | iPhone 12+/iPad Pro/Android compatible | Electivo | 13 |
| A4 | Mesh scanning y colisiones con el entorno real | Avanzado | iPad Pro con LiDAR / Android compatible | Electivo | 11 |
| A5a | Mini-experiencia AR situada: implementación | Avanzado | iPhone/iPad/Android | Electivo | 12 |
| A5b | Mini-experiencia AR situada: evaluación | Avanzado | iPhone/iPad/Android | Electivo | 12 |

**A1 — AR Foundation: detección de planos y anclaje.** Instalar AR Foundation y los providers (ARKit XR Plugin para iOS, ARCore XR Plugin para Android). Configurar el proyecto para build iOS o Android. Crear una escena con ARSession, ARSessionOrigin, ARPlaneManager. Instanciar un cubo al tocar la pantalla sobre un plano detectado, anclado a ese plano. Validar: cubo aparece sobre el plano y mantiene su posición al mover el dispositivo. Tests: configuración del proyecto, componentes AR presentes, lógica de touch-to-anchor.

**A2 — Image tracking y objetos sobre marcadores.** Agregar ARTrackedImageManager con una Reference Image Library con 2-3 imágenes. Instanciar prefabs distintos sobre cada imagen tracked. Validar: cada imagen activa su objeto, el objeto se mueve con la imagen. Tests: image library configurada, prefabs asociados.

**A3 — Oclusión, iluminación estimada y coherencia visual.** Habilitar AROcclusionManager con depth texture. Usar la iluminación estimada del AREnvironmentProbe para iluminar objetos virtuales con la luz real. Agregar sombras recibidas por el plano virtual sobre el mundo real. Validar: objetos virtuales quedan ocluidos por manos u obstáculos reales, iluminación coincide con la ambiental. Tests: managers configurados, materiales con shader apropiado.

**A4 — Mesh scanning y colisiones con el entorno real.** Habilitar ARMeshManager (requiere LiDAR o depth sensor). Generar un mesh del entorno. Agregar colisiones físicas entre objetos virtuales (ej: pelotas) y el mesh real. Validar: pelota lanzada rebota contra muebles reales. Tests: mesh manager configurado, colliders generados dinámicamente.

**A5a — Mini-experiencia AR situada: implementación.** Combinar lo anterior en una mini-experiencia con un objetivo claro (ej: colocar y organizar objetos virtuales en el espacio del usuario). Tests: escena integrada, flujo completo.

**A5b — Mini-experiencia AR situada: evaluación.** Idem V5b adaptado a AR, con cuestionario propio del contexto (menos SSQ, más SUS y cuestionario de utilidad). Tests: reporte entregado.

### 4.4. Bloque MR

| ID | Título | Nivel | Dispositivo | Obligatoriedad | Semana |
|---|---|---|---|---|---|
| X1 | PolySpatial básico: escena MR en Vision Pro | Básico | Vision Pro / simulador | Obligatorio (muestra) | 4 |
| X2 | Input por mirada y pellizco; comparativa con Quest 3 passthrough | Intermedio | Vision Pro + Quest 3 | Electivo | 10 |
| X3 | Anclajes persistentes y contenido mixto en el espacio | Intermedio | Vision Pro / Quest 3 | Electivo | 13 |
| X4 | Visualización situada: datos anclados en el espacio físico | Avanzado | Vision Pro / Quest 3 | Electivo | 11 |
| X5a | Mini-experiencia MR: implementación | Avanzado | Vision Pro / Quest 3 | Electivo | 12 |
| X5b | Mini-experiencia MR: evaluación | Avanzado | Vision Pro / Quest 3 | Electivo | 12 |

**X1 — PolySpatial básico.** Instalar PolySpatial y configurar el proyecto para visionOS. Crear una escena bounded (volumen limitado) con un objeto 3D anclado al suelo. Hacer build al Vision Pro Simulator (en Xcode). Validar en el simulador. Tests: configuración del proyecto, PolySpatial presente, escena correcta.

**X2 — Input por mirada y pellizco; comparativa con Quest 3 passthrough.** Implementar interacción por gaze + pinch en Vision Pro (SpatialPointerDevice). Reconstruir la misma escena en Quest 3 con passthrough y hand tracking. Comparar las dos modalidades en un reporte breve (markdown). Tests: ambas escenas presentes, hooks de input configurados.

**X3 — Anclajes persistentes y contenido mixto en el espacio.** Usar World Anchors (ARWorldMap en iOS, PersistentAnchor en Quest). Guardar la posición de objetos entre sesiones. Validar: cerrar la app, reabrir, los objetos están donde se dejaron. Tests: lógica de serialización/deserialización de anchors.

**X4 — Visualización situada: datos anclados en el espacio físico.** Cargar un dataset simple (CSV o JSON incluido en el starter) y visualizarlo como gráfica 3D anclada a una superficie real. Ejemplo: barras verticales con las ventas mensuales de una empresa, flotando sobre una mesa. Tests: carga del dataset, generación correcta de la visualización.

**X5a — Mini-experiencia MR: implementación.** Mini-experiencia que combine anclajes persistentes, visualización situada y interacción natural. Ejemplo: un dashboard de productividad anclado al escritorio del usuario. Tests: escena integrada.

**X5b — Mini-experiencia MR: evaluación.** Evaluación con 1 usuario externo, aplicar SUS y preguntas abiertas sobre utilidad y naturalidad. Tests: reporte entregado.

### 4.5. Bonus

| ID | Título | Nivel | Dispositivo | Obligatoriedad | Semana |
|---|---|---|---|---|---|
| HL | HoloLens 1 con MRTK | Avanzado | HoloLens 1 | Bonus (opcional) | Libre |

**HL — HoloLens 1 con MRTK.** Módulo histórico. Setup del toolchain UWP, instalación de MRTK v2, build y deploy a HoloLens 1. Crear una escena con un objeto manipulable mediante tap y gaze (clásico de HoloLens). Reflexión en el reporte sobre diferencias con las plataformas modernas. Tests: build generado, componentes MRTK presentes.

### 4.6. Calendario sugerido por semana

El libro incluye un apéndice `calendario-sugerido.md` con esta tabla, y cada módulo referencia su semana recomendada en la metadata. El calendario asume la edición 2026-2 como referencia; cada edición lo ajusta vía el script `create_edition.py`.

| Semana | Módulo sugerido | Contexto de cátedra |
|---|---|---|
| 1 | M0 | Introducción e historia |
| 2 | M1 | Actividad práctica |
| 3 | V1 (muestra VR) | Hardware |
| 4 | X1 (muestra MR) | Interacción |
| 5 | (pausa Entrega P1) | Entrega Proyecto 1 |
| 6 | Electivo libre | Percepción |
| 7 | A1 (muestra AR) | Calibración y CV para AR |
| 8 | Electivo libre | Presentación papers |
| 9 | (pausa Entrega P2) | Entrega Proyecto 2 |
| 10 | Electivo libre | Desarrollo Centrado en el Humano |
| 11 | Electivo libre | Analíticas inmersivas y viz situada |
| 12 | Electivo libre | Efectos adversos y evaluación |
| 13 | Electivo libre | Tracking y coherencia visual |
| 14 | (pausa Examen) | Examen |
| 15 | (pausa Entrega P3) | Entrega Proyecto 3 |

Un estudiante que cumple la ruta mínima (5 obligatorios + 1 electivo del bloque elegido) aprueba con 60 pts en ~6 semanas efectivas de ayudantía.

---

## 5. Plantilla por módulo

Cada módulo DEBE seguir esta estructura exacta. Esto permite replicar el patrón para los 21 módulos y mantiene consistencia pedagógica.

### 5.1. Archivo markdown del módulo (`docs/<bloque>/<id>-<slug>.md`)

```markdown
# <ID> — <Título>

!!! info "Metadatos"
    - **Nivel:** <básico/intermedio/avanzado>
    - **Duración estimada:** 60 minutos
    - **Dispositivo:** <nombre> (validable en simulador)
    - **Puntos:** 10
    - **Obligatoriedad:** <obligatorio / electivo / bonus>
    - **Semana recomendada:** <N> — <tema de cátedra>
    - **Prerrequisitos:** <lista de módulos>

## Objetivo

<Un párrafo. Qué aprende el estudiante y por qué importa.>

## Conceptos clave

<Enumeración breve de conceptos técnicos que el módulo introduce o refuerza. Enlace a lecturas de cátedra o referencias externas.>

## Criterios de aceptación

Para que el módulo cuente como aprobado:

1. <Criterio objetivo verificable por test>
2. <Criterio objetivo verificable por test>
3. <Criterio objetivo verificable por test>
4. Al menos un checkpoint validado en dispositivo real (ver sección Validación).

## Setup

Instrucciones concretas para preparar el entorno:

- Clonar el starter: `git clone ... && cd modules/<id>/starter`
- Abrir con Unity 6 LTS.
- Verificar paquetes...

## Guía paso a paso

### Paso 1 — <Título breve>

<Descripción. Pseudocódigo o snippet corto. NUNCA solución completa.>

### Paso 2 — ...

...

## Validación

### Checkpoint A — Setup inicial

<Qué debe funcionar antes de empezar. 5-10 min.>

### Checkpoint B — Resultado

<Qué debe funcionar al terminar. 10-15 min.>

**Cuestionario (solo si validaste en dispositivo real):** <enlace o preguntas inline>

## Tests automatizados

Ejecutar con:

    cd modules/<id>
    ./run-tests.sh

O desde Unity: Window → General → Test Runner.

## Guía de uso de IA sugerida

Para este módulo, el asistente de IA es útil para:

- <Qué sí preguntar>

Y NO deberías delegar:

- <Qué debes entender tú>

Si pediste ayuda a la IA, documenta brevemente en `ai-log.md` (en tu rama) qué preguntaste y qué usaste.

## Si te traba

Opciones en orden recomendado:

1. Revisar el apéndice de troubleshooting.
2. Preguntar al ayudante del laboratorio en la hora de ayudantía.
3. Abrir un Issue en el repo con el label `help-wanted`.
4. Como último recurso, pedir acceso a la solución abriendo un Issue con el template "Solution Request".

## Entregable

- Commit en tu rama `student/<usuario>/<id>` con el código funcional.
- PR a `main` con el label `module:<id>`.
- Si validaste en dispositivo real, archivo `validation.md` en tu PR con el cuestionario completado.

## Puntos y rúbrica

| Criterio | Puntos |
|---|---|
| Tests pasando | 6 |
| Validación en dispositivo (al menos una vez en el bloque) | 2 |
| Cuestionario completado (si aplica) | 1 |
| Documentación `ai-log.md` | 1 |
| **Total** | **10** |
```

### 5.2. Carpeta del módulo (`modules/<id>/`)

```
modules/<id>/
├── README.md              # Copia resumida del enunciado (para quien clona solo esta carpeta)
├── acceptance.md          # Criterios de aceptación en detalle, formato machine-readable
├── starter/               # Proyecto Unity base (puede ser un paquete .unitypackage o carpeta Assets)
│   ├── Assets/
│   │   ├── Scenes/
│   │   │   └── Starter.unity
│   │   └── Scripts/
│   └── README.md
├── tests/                 # Tests Unity que el starter debe pasar al completarse
│   ├── EditMode/
│   │   └── <ID>Tests.cs
│   └── PlayMode/
│       └── <ID>PlayTests.cs
├── rubric.yml             # Rúbrica estructurada
└── run-tests.sh           # Script bash que corre los tests headless
```

Ejemplo de `rubric.yml`:

```yaml
module_id: V1
title: "Escena VR básica"
total_points: 10
criteria:
  - id: tests_passing
    description: "Todos los tests unitarios y de PlayMode pasan"
    points: 6
    automated: true
  - id: device_validation
    description: "Al menos una validación en dispositivo real en el bloque"
    points: 2
    automated: false
    self_declared: true
  - id: questionnaire
    description: "Cuestionario de validación completado (si aplica)"
    points: 1
    automated: false
  - id: ai_log
    description: "Archivo ai-log.md presente y no vacío"
    points: 1
    automated: true
```

### 5.3. Carpeta de solución (`idi3185-xr-labs-solutions/solutions/<id>/`)

```
solutions/<id>/
├── README.md                          # Explicación de las decisiones de diseño, trade-offs
├── src/                               # Código resuelto completo
│   ├── Assets/
│   └── ...
├── tests-passed.log                   # Output de la última ejecución de tests exitosa
├── build-link.md                      # Link al Release del repo principal con el build
└── notes-for-lab-assistant.md         # Notas internas para el ayudante del laboratorio
```

El archivo `notes-for-lab-assistant.md` sigue el formato de la sección 3.2.

---

## 6. Scripts Python

### 6.1. `scripts/create_edition.py`

**Propósito:** generar un nuevo repo para una edición específica del curso.

**Uso:**

    python scripts/create_edition.py --year 2027 --semester 1 --students students.yaml

**Comportamiento:**

1. Lee `students.yaml` con la lista de estudiantes (nombre + usuario GitHub).
2. Crea un nuevo repo privado `idi3185-xr-labs-2027-1` en la cuenta `leonelmerino` (vía `gh` CLI o GitHub API).
3. Clona el repo-template actual y hace push al nuevo repo como estado inicial.
4. Para cada estudiante en `students.yaml`, lo agrega como colaborador con permiso de write.
5. Crea una rama inicial `student/<usuario>` por cada estudiante.
6. Habilita GitHub Pages para publicar el libro de la edición.
7. Actualiza `docs/apendices/calendario-sugerido.md` con las semanas de cátedra reales de esta edición si se provee un calendario.
8. Imprime resumen: URL del repo, URL del libro, lista de colaboradores agregados.

**Dependencias:** `PyGithub`, `click` o `argparse`, `pyyaml`, `rich` (para output amigable).

Formato de `students.yaml`:

```yaml
edition:
  year: 2027
  semester: 1
  course_code: IDI3185
students:
  - name: "Nombre Apellido"
    github: "usuario-github"
    email: "correo@uc.cl"
  - ...
```

### 6.2. `scripts/add_students.py`

**Propósito:** agregar estudiantes a una edición existente (si se inscriben tarde o se agregan ayudantes).

**Uso:**

    python scripts/add_students.py --repo idi3185-xr-labs-2027-1 --students new_students.yaml

### 6.3. `scripts/grade_dashboard.py`

**Propósito:** generar un dashboard de puntos por estudiante consultando el estado de PRs y resultados de CI.

**Uso:**

    python scripts/grade_dashboard.py --repo idi3185-xr-labs-2027-1 --output dashboard.html

**Comportamiento:**

1. Para cada estudiante en la edición, consulta sus PRs mergeados.
2. Para cada PR mergeado con label `module:<id>`, chequea que los tests de CI hayan pasado.
3. Agrega puntos del módulo si el PR cumple criterios automatizados.
4. Marca los criterios no automatizados (validación en dispositivo, cuestionario) como "pendiente de revisión manual" en una columna aparte.
5. Genera un HTML con una tabla: estudiantes en filas, módulos en columnas, puntos en celdas, totales y aprobación por estudiante.

### 6.4. `scripts/validate_module.py`

**Propósito:** permitir al estudiante correr los tests de un módulo localmente antes de hacer PR.

**Uso:**

    python scripts/validate_module.py --module V1

**Comportamiento:**

1. Invoca Unity en modo batch (`-batchmode -runTests`) sobre el proyecto Unity del módulo.
2. Parsea el resultado y muestra pass/fail por test.
3. Genera `tests-passed.log` si todos pasan.

---

## 7. GitHub Actions (CI/CD)

### 7.1. `mkdocs-deploy.yml`

Trigger: push a `main` que modifique `docs/`, `mkdocs.yml`.
Pasos:
1. Setup Python 3.11.
2. `pip install mkdocs mkdocs-material`.
3. `mkdocs gh-deploy --force`.

### 7.2. `module-tests.yml`

Trigger: PR a `main` desde ramas `student/*`.
Pasos:
1. Detectar el módulo a partir del label `module:<id>`.
2. Setup Unity 6 LTS via `game-ci/unity-test-runner` action.
3. Correr tests EditMode y PlayMode del módulo.
4. Reportar resultados en el PR.
5. Añadir label `tests-passing` o `tests-failing`.

### 7.3. `release-builds.yml`

Trigger: tag `v*-<ID>`.
Pasos:
1. Setup Unity 6 LTS.
2. Build para el target del módulo (StandaloneWindows, Android, iOS según corresponda).
3. Crear GitHub Release con el binario adjunto.

---

## 8. Plan de trabajo (6 semanas, 72 h totales)

El ayudante experto trabaja ~12 h/semana. La IA de código ejecuta la mayor parte del tecleo bajo supervisión del ayudante.

### Semana 1 (3-9 nov) — Infraestructura base (12 h)

**Objetivo:** repo con estructura, MkDocs funcionando, CI básico.

- Clonar `idi3185-xr-labs` localmente.
- Crear estructura de carpetas según sección 3.1.
- Agregar `README.md`, `LICENSE` (MIT), `LICENSE-CONTENT` (CC BY-SA 4.0), `.gitignore`, `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`.
- Configurar `mkdocs.yml` con tema Material y navegación por bloques.
- Crear `docs/index.md`, `docs/como-usar-el-libro.md`, `docs/apendices/setup-entorno.md`, `docs/apendices/calendario-sugerido.md`, `docs/apendices/hardware-alternativo.md`.
- Configurar GitHub Action `mkdocs-deploy.yml`.
- Habilitar GitHub Pages (branch `gh-pages`).
- Verificar que el libro vacío se publica correctamente en `https://leonelmerino.github.io/idi3185-xr-labs/`.
- Clonar `idi3185-xr-labs-solutions`, estructura mínima, LICENSE MIT, README con advertencia, esqueleto de `lab-assistant-handbook.md`.
- Commit: "Infraestructura inicial del repo y libro MkDocs".

**Checkpoint semana 1:** sitio MkDocs navegable publicado con índice de los 21 módulos (sin contenido todavía) y la tabla de calendario sugerido.

### Semana 2 (10-16 nov) — Unity template + módulo piloto (12 h)

**Objetivo:** proyecto Unity template funcional y UN módulo completo como gate obligatorio.

- Crear proyecto Unity 6 LTS en `unity-template/`.
- Instalar XR Interaction Toolkit, AR Foundation (ARKit + ARCore providers), PolySpatial.
- Configurar `.gitignore` apropiado para Unity (ignorar Library/, Temp/, Logs/, etc.).
- Configurar Test Framework.
- Crear escena placeholder y asegurar que el proyecto abre y corre.
- **Construir el módulo piloto completo: M1 (nivelación Unity + XRI).**
  - Markdown del módulo (`docs/preludio/m1-unity-xri-nivelacion.md`).
  - Carpeta `modules/m1/` con starter, tests, rubric.yml, run-tests.sh.
  - Solución en `idi3185-xr-labs-solutions/solutions/m1/` incluyendo `notes-for-lab-assistant.md`.
  - Build pre-compilado publicado en Release `v1.0-M1`.
  - Issue templates y pull request template.
- Configurar GitHub Action `module-tests.yml` apuntando al módulo piloto.
- Hacer PR interno simulando ser estudiante, verificar que CI corre y aprueba.

**Checkpoint semana 2 — GATE OBLIGATORIO:** el profesor revisa M1 completo (markdown, starter, tests, solución, notas para el ayudante del lab, build, flujo de PR). Si aprueba, el patrón se replica. Si pide cambios, se iteran antes de seguir.

### Semana 3 (17-23 nov) — Scripts + resto del preludio y muestras de bloques (12 h)

**Objetivo:** scripts Python funcionales y los 5 módulos obligatorios completos.

- Implementar `scripts/create_edition.py`, `scripts/add_students.py`, `scripts/validate_module.py`.
- Pruebas de los scripts creando un repo de prueba descartable.
- Construir **M0** (IA en XR).
- Construir **V1, A1, X1** (los tres de muestra obligatorios).
- Cada módulo con markdown, starter, tests, solución, notas para ayudante del lab, build.

**Checkpoint semana 3:** preludio completo + los tres módulos obligatorios de muestra publicados. Un estudiante ya puede cumplir los 50 pts obligatorios con lo publicado.

### Semana 4 (24-30 nov) — Electivos intermedios de los 3 bloques (12 h)

**Objetivo:** ampliar oferta de electivos para que los estudiantes puedan superar los 60 pts de aprobación cómodamente.

- Construir **V2, V3** (electivos intermedios VR).
- Construir **A2, A3** (electivos intermedios AR, con rutas iOS/Android).
- Construir **X2, X3** (electivos intermedios MR).

**Checkpoint semana 4:** cada bloque tiene 3 módulos publicados (muestra + 2 electivos intermedios). Un estudiante que elige profundizar en un bloque tiene suficiente ruta de aprobación.

### Semana 5 (1-7 dic) — Módulos avanzados (12 h)

**Objetivo:** cubrir módulos avanzados de los 3 bloques.

- Construir **V4, V5a, V5b**.
- Construir **A4, A5a, A5b**.
- Construir **X4, X5a, X5b**.

**Checkpoint semana 5:** los 20 módulos de los bloques completos. Solo falta el bonus HoloLens y pulido.

### Semana 6 (8-15 dic) — Bonus, pulido y dashboard (12 h)

**Objetivo:** cerrar el libro y preparar lanzamiento 2027-1.

- Construir **HL** (bonus HoloLens).
- Implementar `scripts/grade_dashboard.py`.
- Configurar `release-builds.yml` para generar builds automáticamente al tag.
- Escribir apéndices: `uso-de-ia.md`, `hardware-alternativo.md` (completar con HTC Vive Pro, PC propio, smartphones), `troubleshooting.md`.
- Completar `lab-assistant-handbook.md` en el repo de soluciones.
- Revisión de consistencia de todos los módulos (tono, formato, rúbrica).
- Verificar que el libro completo renderiza bien en MkDocs.
- Verificar que todos los tests pasan en CI.
- Verificar que todos los builds están publicados en Releases.
- Hacer un dry-run completo: usar `create_edition.py` para generar una edición de prueba.
- Documentar en el README del repo el estado final y cómo usarlo.

**Checkpoint semana 6 — ENTREGA FINAL:** libro completo publicado, 21 módulos funcionales, scripts probados, manual del ayudante del laboratorio listo, listo para 2027-1.

### 8.1. Buffer y manejo de atrasos

Si una semana se atrasa:
- Priorizar siempre los 5 módulos obligatorios (M0, M1, V1, A1, X1) sobre los electivos.
- Entre electivos, priorizar los intermedios (V2-V3, A2-A3, X2-X3) sobre los avanzados.
- Dejar HoloLens como el primer corte si falta tiempo.
- Es preferible entregar 15 módulos sólidos que 21 a medio hacer.

---

## 9. Convenciones

### 9.1. Nombres de ramas

- `main` — rama protegida, solo PRs mergeados.
- `student/<usuario-github>/<id-modulo>` — rama de trabajo del estudiante.
- `module/<id>-<descripcion>` — rama de trabajo del ayudante experto construyendo un módulo.
- `fix/<descripcion>` — correcciones pequeñas.

### 9.2. Mensajes de commit (en español)

Formato: `<tipo>(<alcance>): <descripción>`

Tipos: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`.

Ejemplos:
- `feat(v1): escena VR básica con teleport funcional`
- `docs(m0): guía de uso de IA en desarrollo XR`
- `test(a2): tests de image tracking`
- `chore(ci): workflow de deploy mkdocs`

Terminar cada commit con:

    Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>
    Claude-Session: https://claude.ai/code/session_0132KarG5hqYHUduHMhyeC7z

### 9.3. Pull requests

Título: igual que el commit principal.

Descripción: template en `.github/pull_request_template.md` con secciones Qué, Por qué, Checklist.

Terminar cada PR con:

    🤖 Generated with [Claude Code](https://claude.com/claude-code)

    https://claude.ai/code/session_0132KarG5hqYHUduHMhyeC7z

### 9.4. Issues

Labels principales:
- `module:<id>` — issue relacionado a un módulo específico.
- `bug` — error en el libro, starter o tests.
- `enhancement` — mejora propuesta.
- `help-wanted` — estudiante atascado pidiendo ayuda.
- `solution-request` — estudiante pide acceso a solución.
- `question` — pregunta general.

### 9.5. Tags de release

- `v1.0-<ID>` — build de solución del módulo `<ID>` para la versión 1.0 del libro.
- `v1.0` — tag de la versión completa del libro (al final de semana 6).

---

## 10. Requisitos para el ayudante experto

### 10.1. Habilidades

- Experiencia media/alta con Unity (idealmente con XR, aunque la IA puede cubrir gaps).
- C# funcional.
- Git/GitHub fluido.
- Capacidad de supervisar y revisar código generado por IA.
- Español nativo o fluido para redactar el contenido pedagógico.

### 10.2. Acceso

- Cuenta GitHub con permiso de colaborador en los dos repos.
- Acceso físico al laboratorio DILAB-UC para probar en dispositivos reales:
  - Meta Quest 2 (3 unidades).
  - Meta Quest 3 (2 unidades).
  - Apple Vision Pro (2 unidades).
  - iPad con ARKit (1 unidad).
  - HoloLens 1 (1 unidad).
  - HTC Vive Pro (1 unidad, opcional, para validar la alternativa del apéndice).
- Mac disponible para builds de iOS y visionOS (coordinar con Leonel).
- Suscripción Unity (Personal es suficiente para este proyecto).

### 10.3. Entorno de desarrollo

- Unity 6 LTS instalado.
- Xcode instalado en Mac (para iOS y visionOS).
- Android Studio con SDK (para builds Android).
- `gh` CLI autenticado con la cuenta del ayudante.
- Python 3.11 con `pip install -r scripts/requirements.txt`.
- Asistente de IA preferido: Claude Code recomendado por su integración con el flujo de git y su capacidad de contexto largo.

---

## 11. Criterios de calidad para cada módulo

Antes de considerar un módulo "terminado", debe cumplir:

- [ ] Markdown del módulo en `docs/<bloque>/<id>-<slug>.md` con la plantilla completa.
- [ ] Carpeta `modules/<id>/` con starter, tests, rubric.yml, run-tests.sh.
- [ ] Solución completa en `idi3185-xr-labs-solutions/solutions/<id>/`.
- [ ] `notes-for-lab-assistant.md` del módulo redactado (errores comunes, preguntas típicas, puntos de bloqueo).
- [ ] Build pre-compilado publicado como GitHub Release `v1.0-<ID>` con binario adjunto.
- [ ] Tests pasan en CI.
- [ ] Guía de uso de IA incluida con qué sí y qué no delegar.
- [ ] Checkpoint A y B definidos con instrucciones claras.
- [ ] Rúbrica estructurada en `rubric.yml`.
- [ ] Enlaces internos entre módulos relacionados funcionan.
- [ ] Markdown renderiza correctamente en MkDocs (verificar `mkdocs serve` localmente).

---

## 12. Qué NO hacer

- NO crear fechas fijas en el contenido del libro (cambian por edición; usar número de semana).
- NO asumir que todos los estudiantes tienen smartphone compatible (es opcional en el bloque AR).
- NO publicar las soluciones en el repo público.
- NO escribir contenido pedagógico que lea las láminas de cátedra (son complementos, no reemplazo).
- NO sobrecargar los módulos: 1 hora significa 1 hora. Si no cabe, acotar alcance.
- NO delegar a la IA el diseño pedagógico sin revisión. El tono, la secuencia y la elección de ejemplos requieren criterio humano.
- NO modificar las decisiones de la sección 2 sin consultar con Leonel.
- NO confundir los roles: el ayudante experto construye el libro (nov-dic 2026); el ayudante del laboratorio acompaña a los estudiantes (semestre 2027-1).

---

## 13. Primeros pasos para el ayudante experto

1. Clonar los dos repos localmente.
2. Leer completo este `PLAN.md`.
3. Leer las láminas de cátedra en Google Drive del curso (Leonel comparte acceso).
4. Instalar Unity 6 LTS si no está.
5. Verificar acceso al laboratorio y a los dispositivos.
6. Comenzar la Semana 1 según el plan de trabajo.
7. Checkpoint semanal con Leonel (reunión corta de 15-30 min, día a convenir).

---

## 14. Contacto

- **Leonel Merino** — leonel.merino@uc.cl — Profesor del curso, dueño de la decisión final sobre todo lo pedagógico y de arquitectura.
- **DILAB-UC** — dilab.ing.uc.cl — laboratorio donde ocurre el trabajo físico.

---

**Última actualización de este plan:** 3 de noviembre de 2026.
