# CI y publicación del libro

`workflows/mkdocs-deploy.yml` comprueba el sitio con `mkdocs build --strict`
en PRs a `main`, pushes relevantes a `main` y ejecución manual. Conserva el
HTML generado como artefacto del job de comprobación. Los PRs no reciben
permisos de escritura para publicar.

Después de un build correcto en `main`, el job de publicación usa
`mkdocs gh-deploy --force --strict` para actualizar exclusivamente `gh-pages`.
Los tests de módulos Unity y los builds de Releases se configurarán en sus
etapas correspondientes; todavía no hay validación automática de entregas.

## Habilitar GitHub Pages

**Estado actual:** workflow preparado localmente; todavía no ejecutado en
GitHub. La publicación y la URL del sitio no están verificadas.

1. Incorporar esta infraestructura en `main` mediante revisión del equipo.
2. Permitir GitHub Actions y ejecutar el workflow para crear `gh-pages`.
3. En **Settings → Pages → Build and deployment**, seleccionar
   **Deploy from a branch**, rama **gh-pages**, carpeta **/(root)**.
4. Verificar el despliegue y abrir la URL del libro indicada por GitHub.

El token automático necesita permiso de escritura de contenidos para el job
de publicación. No se requiere un token personal almacenado como secreto.
Pages desde un repositorio privado depende del plan de la cuenta propietaria;
confirmar disponibilidad antes de modificar la visibilidad del repositorio.

## Pendientes de coordinación

- Confirmar acceso de publicación y soporte de Pages en la cuenta propietaria.
- Resolver cómo distribuir builds públicos mientras el repositorio sea privado.
- Validar con M1 el flujo de entregas y la aplicación de rúbricas.
- Ajustar las atribuciones heredadas del plan a las herramientas realmente usadas.

No hay templates de entrega ni labels automáticos activos hasta el piloto M1.
