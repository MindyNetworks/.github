# Guía de contribución

Convenciones de trabajo para los repositorios de MindyNetworks. Aplican por
defecto a todos; si un repositorio necesita algo distinto, lo documenta en su
propio `CONTRIBUTING.md`, que reemplaza a este.

## Ramas

La rama default es **siempre `main`**. No usamos `master`.

| Rama | Propósito |
| -- | -- |
| `main` | Código de referencia del proyecto. Protegida: no se hace push directo. |
| `feat/<descripción-corta>` | Nueva funcionalidad. Sale de `main`. |
| `fix/<descripción-corta>` | Corrección de bug. Sale de `main`. |
| `chore/<descripción-corta>` | Configuración, dependencias, herramientas, CI. |

El flujo base es **`main` más ramas de trabajo de vida corta**. No hay una rama
de integración obligatoria: si un proyecto justifica agregar `development`,
`staging` o similar, queda a criterio de quien lo mantiene, y en ese caso
conviene documentarlo en el `README.md` del repositorio para que el resto del
equipo y los agentes sepan a qué rama apuntar.

Las ramas se borran automáticamente al mergear. No hace falta limpiarlas a
mano.

## Commits

Seguimos [Conventional Commits](https://www.conventionalcommits.org/).

```
<tipo>[ámbito opcional]: <descripción>

[cuerpo opcional]

[pie opcional]
```

| Tipo | Cuándo usarlo |
| -- | -- |
| `feat` | Nueva funcionalidad |
| `fix` | Corrección de bug |
| `docs` | Solo cambios en documentación |
| `style` | Formato, sin cambio de lógica |
| `refactor` | Reestructuración sin feature ni fix |
| `test` | Agregar o corregir pruebas |
| `chore` | Build, herramientas, dependencias |
| `ci` | Configuración de CI/CD |
| `perf` | Mejora de rendimiento |

Ejemplos:

```
feat(auth): agregar login con OAuth2
fix(api): manejar respuesta nula del endpoint de pagos
chore: actualizar Node a v22
docs: actualizar instrucciones de setup en el README
```

Para un cambio que rompe compatibilidad, `!` después del tipo y un pie
`BREAKING CHANGE:`:

```
feat!: rediseñar el formato de respuesta de la API

BREAKING CHANGE: el envelope de respuesta cambió de `data` a `result`
```

## Pull requests

Todo cambio a la rama default entra por pull request. El push directo está
bloqueado por una regla de la organización, y eso incluye el force-push y el
borrado de la rama.

1. Ramificar desde la rama default
2. Un tema por PR — si el PR hace dos cosas, son dos PRs
3. Completar la plantilla del PR
4. Esperar que el CI esté verde antes de pedir revisión
5. **Merge por squash.** Es el único método habilitado: el historial de la rama
   default es lineal, un commit por PR

No se exige aprobación de un revisor, porque hay repositorios con una sola
persona trabajando. Eso no es permiso para saltarse la revisión: si hay alguien
más en el proyecto, pídela.

## Documentación

Toda la documentación del proyecto vive en el directorio `docs/` de la raíz del
repositorio, y se escribe en Markdown (`.md`). No se dejan documentos sueltos en
la raíz ni repartidos por otras carpetas: si es documentación, va en `docs/`.

El `README.md` es la excepción: se queda en la raíz, porque es lo primero que se
ve al abrir el repositorio. Todo lo demás —guías, notas técnicas, decisiones,
instrucciones de setup— va en `docs/`, con nombre en minúsculas y palabras
unidas por guiones (`docs/deploy-a-staging.md`, no `docs/Deploy Staging.md`).

## Registro de cambios

Cada repositorio lleva un `CHANGELOG.md` en la raíz, en formato
[Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/), con una sección
`## [No publicado]` arriba.

**Todo PR que cambie comportamiento agrega su entrada ahí**, en la misma rama
del cambio. Los PRs que solo tocan configuración, dependencias o CI no
necesitan entrada.

El `git log` ya dice *qué* cambió: con merge por squash y Conventional Commits,
cada commit de `main` es un PR. Lo que no dice es *por qué*, y eso es
precisamente lo que se pierde cuando el diff lo redactó un agente. La entrada
del changelog es para la persona que va a leer esto en seis meses.

Escribe la entrada pensando en quien usa el proyecto, no en quien lo programó:

```markdown
## [No publicado]

### Agregado
- Login con OAuth2 para el panel de administración

### Corregido
- El endpoint de pagos devolvía 500 cuando el monto venía nulo
```

En los repositorios donde está activado release-please, las entradas se mueven
a una versión numerada de forma automática al liberar. En los demás, la sección
`No publicado` es el registro y basta.

## Revisión de código

- Aprobar solo si leíste y entendiste el diff
- Pedir cambios con retroalimentación específica y accionable
- Prefijar con `nit:` lo que no es bloqueante

## Seguridad

Cada push y cada PR pasan por un escaneo automático de secretos y de patrones
de código inseguro. Si el escaneo marca un hallazgo, **no lo silencies para que
pase el CI**: confirma primero si es real.

Si un secreto llegó a un commit, rotarlo es lo primero y lo urgente. Quitarlo
del historial no lo invalida: cualquiera que haya clonado el repositorio antes
ya lo tiene. Rotar la credencial, y después limpiar el historial.

Nunca commitear archivos `.env`, llaves privadas, certificados ni tokens.
Cuando un proyecto necesita variables de entorno, versiona un `.env.example`
con los nombres de las variables y sin ningún valor real.

Para reportar una vulnerabilidad, ver [SECURITY.md](SECURITY.md).

## Trabajo con agentes de IA

Los repositorios llevan un `AGENTS.md` en la raíz con el contexto que un agente
necesita para trabajar en ese proyecto. Si trabajas con un agente y notas que
le falta contexto, o que se equivoca siempre en lo mismo, la corrección va en
ese archivo — no en el prompt de cada sesión.

Un cambio escrito por un agente entra por PR igual que cualquier otro, con las
mismas convenciones de commit, y con alguien que lo leyó y responde por él.
