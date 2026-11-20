# IDI 3185 · Laboratorios de Realidad Extendida

Libro de laboratorios prácticos de VR, AR y MR del curso IDI 3185 de la
Pontificia Universidad Católica de Chile (DILAB-UC).

**Estado:** infraestructura inicial. Hay un índice navegable de 21 módulos;
los proyectos Unity, tutoriales completos, tests y builds siguen pendientes.
El siguiente entregable es el piloto M1, sujeto a revisión del profesor.

Verificación inicial: configuración YAML válida, 28 páginas incluidas en la
navegación, 21 carpetas de módulos y 102 enlaces locales comprobados entre
ambos repositorios. El HTML se generó correctamente con
`python -m mkdocs build --strict`. La publicación en Pages sigue pendiente:
la terminal de esta sesión todavía no puede conectarse a GitHub.

## Ver el libro localmente

CI utiliza Python 3.11. Desde esta carpeta:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements-docs.txt
python -m mkdocs serve
```

Para verificar la documentación:

```bash
python -m mkdocs build --strict
```

El resultado se genera en `site/`, que no se versiona.

## Organización

| Ruta | Contenido |
|---|---|
| [PLAN.md](PLAN.md) | Fuente de verdad y decisiones del proyecto |
| [docs/](docs/index.md) | Libro MkDocs en español |
| [modules/](modules/README.md) | Espacios reservados para los 21 módulos |
| [unity-template/](unity-template/README.md) | Estructura reservada para el proyecto base |
| [scripts/](scripts/README.md) | Estado de las herramientas de gestión |
| [.github/](.github/README.md) | CI y configuración de publicación |

Las soluciones y las notas internas del ayudante viven exclusivamente en
[idi3185-xr-labs-solutions](https://github.com/leonelmerino/idi3185-xr-labs-solutions),
un repositorio privado separado.

## Publicación

El workflow de documentación comprueba PRs a `main` y publica en `gh-pages`
al incorporar cambios en `main`. Hay que configurar GitHub Pages para servir
esa rama: consulta [.github/README.md](.github/README.md).

URL prevista, todavía sin publicación verificada:
<https://leonelmerino.github.io/idi3185-xr-labs/>.

## Contribución y licencias

Consulta [CONTRIBUTING.md](CONTRIBUTING.md) y el
[código de conducta](CODE_OF_CONDUCT.md).

- Código, scripts, tests y snippets: [MIT](LICENSE).
- Contenido pedagógico, imágenes y diagramas originales: [CC BY-SA 4.0](LICENSE-CONTENT).
- Material de terceros: sus respectivas licencias.
