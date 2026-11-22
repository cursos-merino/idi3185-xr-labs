# Contribuir

## Equipo constructor

El plan (`PLAN.md`, en el repo privado de soluciones) es la fuente de verdad. Los cambios pedagógicos o de arquitectura
requieren revisión del profesor; no se modifican las decisiones de su sección 2
como parte de una tarea de infraestructura.

Trabaja en una rama y abre un PR a `main`. Para módulos usa
`module/<id>-<descripcion>` y para correcciones `fix/<descripcion>`.
El código, las clases y sus comentarios se escriben en inglés; el contenido
pedagógico se escribe en español.

Comprueba la documentación con `python -m mkdocs build --strict`.
Los proyectos Unity deben conservar los archivos `.meta` y excluir sus cachés.
Nunca agregues soluciones, credenciales ni listados reales de estudiantes
al repositorio principal.

## Estudiantes

El plan establece ramas `student/<usuario-github>/<modulo-id>` en el repositorio
de la edición, sin forks, y un PR a `main` con etiqueta `module:<id>`.
El procedimiento operativo se validará con M1 antes de habilitar entregas.
Incluye el registro de IA y las evidencias de validación cuando correspondan.

## Commits y revisión

Usa `<tipo>(<alcance>): <descripción>` en español, con tipos `feat`, `fix`,
`docs`, `refactor`, `test` o `chore`. Describe en el PR qué cambió, por qué y
cómo se verificó. Las convenciones de autoría del plan deben reflejar la
herramienta y sesión reales; no copies atribuciones de una sesión ajena.

El formato completo se replicará después de la aprobación del piloto M1.
