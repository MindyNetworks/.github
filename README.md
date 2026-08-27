# .github

Archivos de salud comunitaria por defecto de la organización **MindyNetworks**.

GitHub hereda automáticamente el contenido de este repositorio en cualquier
repo de la organización que no tenga su propia versión de cada archivo. Editar
acá es editar el estándar de todos los repos a la vez, sin copiar nada.

## Qué se hereda desde acá

| Archivo | Qué es |
| -- | -- |
| `CONTRIBUTING.md` | Convenciones de ramas, commits y pull requests |
| `SECURITY.md` | Cómo reportar una vulnerabilidad |
| `.github/PULL_REQUEST_TEMPLATE.md` | Plantilla de descripción de PR |
| `.github/ISSUE_TEMPLATE/` | Formularios de bug y de solicitud de funcionalidad |

## Qué NO se hereda

`CODEOWNERS`, `LICENSE`, `.gitignore`, `dependabot.yml` y los workflows de
GitHub Actions **no se heredan**: cada repositorio necesita los suyos. Para
esos existen las plantillas de repositorio de la organización.

La herencia es todo-o-nada por archivo. Si un repositorio tiene su propio
`.github/ISSUE_TEMPLATE/`, ignora por completo el de acá — no hay mezcla
parcial.

## Este repositorio es público

GitHub **exige** que el repositorio de archivos por defecto sea público; con un
repositorio privado la herencia simplemente no ocurre. Por eso todo lo que se
agregue acá queda legible por cualquiera en internet.

En consecuencia, nada de lo que se escriba en este repositorio puede contener
nombres de hosts, direcciones IP, rutas internas, nombres de clientes o
instituciones, identificadores de proyectos, ni detalles de arquitectura. Las
convenciones de trabajo son genéricas por diseño. Si algo necesita ese nivel de
detalle, va en el repositorio privado que corresponda, no acá.
