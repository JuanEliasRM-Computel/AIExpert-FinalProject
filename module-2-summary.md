# Resumen del módulo 2

**Proyecto**: despliegue del arnés del curso AI Expert (DevExpert Academy) sobre IDStone Office.
**Tarea de referencia**: OT-867 «Web API IDStone (integración escáner tablas)».
**Sesión**: 002.

Las referencias `D<módulo>.<ordinal>` son las de `decisiones-divergencias-arnes.md`; `MF-n`, las de `mejoras-trabajo-futuro.md`.

## Punto de partida

El módulo 1 dejó **siete documentos de descubrimiento** en la raíz de la copia de trabajo y las seis *skills* en `.agents/skills/`, con `.claude/skills` como enlace. **Nada confirmado en SVN.** Ningún fichero del arnés existía todavía: ni `AGENTS.md`, ni `init.sh`, ni `PROGRESS.md`, ni `feature_list.json`. Tres asuntos quedaban diferidos a este módulo por nombre: dónde viven las *specs* teniendo OpenSpec en la casa, qué forma y qué contenido honesto tiene la barrera de comprobaciones en Windows, y una colisión sin resolver entre la puerta de salida del módulo y una decisión propia.

## Qué pretendía lograr esta fase

Lo que el curso fija en su §2.8.1 (`AIExpert.md:1219-1252`): **transformar los documentos de descubrimiento en el arnés mínimo operativo**, de forma que una sesión nueva pueda arrancar y continuar el proyecto sin leer ninguna conversación. Cuatro ficheros, ningún código de producto.

## Cómo se abordó

`$harness-starter` **sin modificar**, invocada a través del enlace `.claude/skills`, después de leer su propia lista de entradas (`SKILL.md:27-38`) y de medir el entorno y el proyecto de referencia por etiquetas. Las tres decisiones diferidas se resolvieron **antes** de escribir los ficheros, no después.

Luego `$feature-spec` sobre `api-bootstrap`, que es la segunda mitad de este módulo (§2.8.3-2.8.4). Esa *skill* se ejecuta **en la sesión**, como el ejercicio del curso indica: el papel que exige independencia es el verificador, no el planificador (§3.6.4, `AIExpert.md:2001-2013`). La investigación se hizo contra el repositorio y contra el precedente de la casa, no contra la conversación.

## Qué se consiguió, comparado con lo que el curso y la referencia esperaban

| Lo que prescribe el curso | Proyecto de referencia (`modulo-2`) | Aquí (recuentos medidos a r32034, 19/11/2026) |
|---|---|---|
| **4 ficheros del arnés**, y ninguno más (`AIExpert.md:1231-1236`; `harness-starter/SKILL.md:10-25`) | los 4 | **los 4** ✔ |
| `AGENTS.md` mapa **corto**: qué es, cómo arranco, cómo verifico (`SKILL.md:93`) | 58 líneas | **85 líneas** |
| `init.sh` honesto y provisional si no hay *bootstrap* (`SKILL.md`, §4) | 16 líneas, provisional | **27 líneas, provisional** ✔ |
| `PROGRESS.md` con estado verificado y registro ligero (`:2111`; plantilla en `references/artifact-templates.md:112-140`) | 23 líneas, 1 entrada | **43 líneas, 2 entradas** |
| `feature_list.json` de **12 a 30 *features*** sesionables (`SKILL.md:67-68`, repetido en `:94`) | 19, todas `not_started` | **20**, 19 `not_started` + 1 `blocked` ✔ |
| **Nueve campos** en cada *feature* (`SKILL.md:88`) | los 9 | **los 9** ✔ |
| **Puerta de salida**, 3 comprobaciones (`AIExpert.md:1244-1248`) | — | **las 3** ✔ |
| **Prohibido** `ARCHITECTURE.md`, `CONSTRAINTS.md`, rúbricas, código de producto (`SKILL.md:20`) | ninguno | **ninguno** ✔ |
| `$feature-spec` sobre una *feature*: `docs/specs/<id>.md` (§2.8.3-2.8.4, `AIExpert.md:1256-1291`) | 1 *spec*, `bootstrap-stack`, 183 líneas | **1 *spec***, `api-bootstrap`, 202 líneas ✔ |

**Resultado**: la puerta de salida del módulo se cumple entera, los cuatro ficheros son los cuatro, y la *spec* de la primera *feature* está escrita. **La fase queda cerrada**, con una diferencia de forma: la *spec* de la referencia es de una *feature* de arranque de pila (`bootstrap-stack`: Next.js, TypeScript, SQLite), y la de aquí es de un anfitrión añadido a una solución que ya existe, con el multiobjetivo del repositorio como problema principal.

## Las divergencias, y por qué

| # | Divergencia | Por qué |
|---|---|---|
| **D2.1** | `docs/specs/` y `openspec/` conviven, separados por unidad y por vida | La casa dirige el desarrollo con OpenSpec, pero la ruta `docs/specs/` está escrita dentro de **cuatro** *skills* del ciclo: moverla las rompe. La *feature* que cambie una capacidad del ERP abre además su cambio en el `openspec/` de la raíz, nunca en `trunk/openspec/`. Coste escrito, y mitigación en MF12 |
| **D2.6** | `feature_list.json` lleva la lista de trabajo entera, 20 entradas, no las cuatro del alcance entregado | Los dos documentos no estaban en conflicto: la puerta de salida mide **la lista**, D2.2 mide **el alcance entregado**. Cuatro entradas serían la lista de hitos que la *skill* rechaza, y harían invisible el aplazamiento. El alcance se expresa en qué entradas llegan a `accepted` |
| **D2.8** | `init.sh` en bash, no en PowerShell, aunque la casa es PowerShell | Tres motivos medidos: el intérprete no aporta nada funcional —`dotnet` se escribe igual—, la *skill* prohíbe un quinto fichero, y la política de ejecución de PowerShell es `Restricted` por omisión en Windows cliente. Los dos primeros caducan en el módulo 3; el tercero no. Forma final: `init.ps1` como barrera e `init.sh` reducido a ejecutarla (MF7) |
| **D2.9** | `PROGRESS.md` se escribe para el agente siguiente: ninguna referencia al curso ni etiqueta que no se resuelva dentro del repositorio | Es un fichero del arnés que mantendrá cada agente que llegue, y ese agente no sabe que existe un curso. La traza por módulos vive en los dos entregables. **Sustituye a D2.4 en la forma del fichero**, que había convertido el registro en guion del vídeo |
| **D2.7** | Encabezados: `AGENTS.md` y `PROGRESS.md` en español; claves y estados de `feature_list.json` en inglés | Es la misma línea que traza la referencia, fichero a fichero, y coincide con **quién lee el encabezado**: lo que parsea una *skill* es un contrato, no un encabezado |
| **D1.8** | `AGENTS.md` lleva las órdenes `mklink /D` y `/J` que recrean `.claude/skills` | Ningún enlace sobrevive a Subversion en Windows (medido, cliente 1.14.2: `E145001`), así que una copia de trabajo nueva se queda sin *skills* en silencio. Es el bloque que explica casi íntegramente las 85 líneas de `AGENTS.md` frente a las 58 de la referencia: sigue muy por debajo del techo de 150 |
| **D2.5** | El punto de restauración es una **revisión anotada**, no una etiqueta | Este repositorio no tiene `tags/`, y ningún proyecto de la casa etiqueta. Estrenar la convención en un repositorio compartido lo decide su responsable |
| — | Una *feature* en estado `blocked` | La *skill* prefiere todas `not_started`; aquí hay un bloqueo externo real —el 19/11/2026 se corrigió su motivo: la base de datos de desarrollo existe y responde; lo que falta es decidir con qué cuenta la usa esta API— y las que dependen de ella heredan el bloqueo por `depends_on`, sin marcarlas una a una |
| — | La *spec* no abre cambio en `openspec/` | `api-bootstrap` no añade ni cambia ninguna capacidad del ERP: crea el anfitrión que las publicará. La regla de D2.1 se aplica, y da **no**; los cambios de capacidad empiezan con el registro de imágenes y la operación de acabado |

## El *handoff* escrito: ¿fue una buena decisión?

El criterio: sí solo si ceñirse al simulador —«usa `$harness-starter` para preparar el repositorio a partir del *discovery*»— habría dado peor resultado. Lo contesta, entonces, lo que el agente no habría podido resolver solo.

**Una sola cosa: el bloque del enlace de `.claude/skills` en `AGENTS.md`.** No hay rastro de él en los documentos del descubrimiento, el enlace ya funcionaba en esta copia y `svn status` devuelve `I .claude`, que se lee como «ignorado a propósito». Saber que ningún enlace sobrevive a Subversion en Windows exige intentar confirmarlo y ver fallar el `commit`: no se deduce, se mide, y ya estaba medido en otra sesión. Sin ese bloque, una copia de trabajo nueva se queda sin *skills* en silencio.

El resto era recuperable, así que **compró tiempo, no acierto, salvo en ese punto**. Y tiene un coste: su §4 justificaba `init.sh` con «que siga siendo comparable con la referencia»; el argumento se heredó y no se sostenía, y D2.8 acabó reescrita con tres motivos medidos.

El curso **no tiene *handoffs* entre módulos** —sus cinco menciones son del traspaso entre papeles del flujo—, así que la frontera de sesión es nuestra (DM.1) y esto es el parche de lo que esa frontera rompe.

> **Regla reutilizable**: lo que no se puede volver a deducir hay que escribirlo; lo deducible, no. Y su sitio es el repositorio, no una carpeta de al lado: es a donde se llegó retirando los *handoffs* (MF8) y limpiando el registro (D2.9).

## Lo que queda abierto

- **Implementar `api-bootstrap`** con `$feature-implementer`, y validarlo después con `$feature-validator` **en una sesión independiente**, que es quien concede la aceptación. Es el módulo 3.
- **Sin restaurar ni compilar nada desde la línea de comandos** en este repositorio. Compilar en Visual Studio no lo demuestra: la barrera se ejecuta en un terminal, y la restauración de la solución pasa por el *feed* privado de la organización (`Computel.CertUtil`, que referencia `IDStone Office.Module`), cuya credencial gestiona Visual Studio de forma interactiva. Desde un terminal hace falta `GITHUB_ACTOR` y `GITHUB_TOKEN`.
- **Nada confirmado en SVN**: 52 adiciones preparadas, pendientes de la orden del usuario. La `M` de `trunk\IDStone Office.Web\obj\...` es ajena y queda fuera.
- **La cuenta con la que esta API usa la base de datos de desarrollo**, sin decidir, lo que retrasa la prueba de concepto pero no a `api-bootstrap`. *[Corregido el 19/11/2026: no es que falte la base de datos —`IDSTONE_DESARROLLO_RC_12` existe en `VDEVELOPMENT01` y responde—, es que falta la identidad.]*
- **Los dos árboles de OpenSpec**, que decide el responsable del repositorio (MF10).
- **DM.4**, en estado *Propuesta*: si `build-brief` se reejecuta con cada tarea nueva. Pregunta redactada para los tutores.
- **MF4**, proyecto de pruebas del componente: es lo que convierte la barrera en una de verdad.
