# Preparar el entorno

!!! warning "Configuración Unity pendiente de validar"
    La versión exacta de Unity 6 LTS y las versiones de paquetes se fijarán
    con el piloto M1. `unity-template/` todavía no es un proyecto Unity válido.

## Herramientas previstas

| Uso | Herramientas |
|---|---|
| Edición de proyectos | Unity Hub y Unity 6 LTS |
| Control de versiones | Git y cuenta GitHub con acceso a la edición |
| VR | XR Interaction Toolkit para Quest 2/3 |
| AR | AR Foundation, ARKit o ARCore según la plataforma |
| MR | PolySpatial para Vision Pro; XRI y passthrough para Quest 3 |
| iOS y visionOS | Mac y Xcode |
| Android | Soporte de compilación Android y SDK/JDK compatibles con el editor |

El piloto documentará la instalación reproducible, los paquetes y la ejecución
de tests. No instales versiones de paquetes al azar para compensar errores.
El acceso de licencia a PolySpatial debe confirmarse antes de preparar la ruta MR.

## Accede al repositorio

Una vez que recibas acceso a la edición del curso, clona su URL e identifica
la rama de trabajo indicada por el equipo docente. No se utilizan forks.

El equipo constructor trabaja sobre `idi3185-xr-labs`; las soluciones se
mantienen por separado en `idi3185-xr-labs-solutions`.

## Preparación del libro para colaboradores

Desde la raíz del repositorio principal:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements-docs.txt
python -m mkdocs serve
```

Abre la URL local que indica MkDocs. Para comprobar el sitio sin iniciar servidor:

```bash
python -m mkdocs build --strict
```

CI utiliza Python 3.11. No es necesario instalar Unity para editar el libro.
