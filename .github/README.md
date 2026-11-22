# CI y publicación del libro

`workflows/mkdocs-deploy.yml` comprueba el sitio con `mkdocs build --strict`
en PRs a `main`, pushes relevantes a `main` y ejecución manual. Conserva el
HTML generado como artefacto del job de comprobación. Los PRs no reciben
permisos de escritura para publicar.

Después de un build correcto en `main`, el job de publicación usa
`mkdocs gh-deploy --force --strict` para actualizar exclusivamente `gh-pages`.
Los tests de módulos Unity y los builds de Releases se configurarán en sus
etapas correspondientes; todavía no hay validación automática de entregas.

## GitHub Pages

Publicado desde la rama `gh-pages`, carpeta `/(root)`:
<https://leonelmerino.github.io/idi3185-xr-labs/>.

El token automático necesita permiso de escritura de contenidos para el job
de publicación. No se requiere un token personal almacenado como secreto.

## Pendientes

- Validar con M1 el flujo de entregas y la aplicación de rúbricas.

No hay templates de entrega ni labels automáticos activos hasta el piloto M1.
