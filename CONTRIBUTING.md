# Guía de contribución

Convenciones de trabajo para los repositorios de MindyNetworks. Aplican por
defecto a todos; si un repositorio necesita algo distinto, lo documenta en su
propio `CONTRIBUTING.md`, que reemplaza a este.

## Ramas

| Rama | Propósito |
| -- | -- |
| rama default (`main` o `master`) | Código de referencia del proyecto. Protegida: no se hace push directo. |
| `feat/<descripción-corta>` | Nueva funcionalidad. Sale de la rama default. |
| `fix/<descripción-corta>` | Corrección de bug. Sale de la rama default. |
| `chore/<descripción-corta>` | Configuración, dependencias, herramientas, CI. |

El flujo base es **rama default más ramas de trabajo de vida corta**. No hay
una rama de integración obligatoria: si un proyecto justifica agregar
`development`, `staging` o similar, queda a criterio de quien lo mantiene, y en
ese caso conviene documentarlo en el `README.md` del repositorio para que el
resto del equipo y los agentes sepan a qué rama apuntar.

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
