# Resumen del módulo 1

**Proyecto**: despliegue del arnés del curso AI Expert (DevExpert Academy) sobre IDStone Office.
**Tarea de referencia**: OT-867 «Web API IDStone (integración escáner tablas)».
**Sesión**: 001.

Las referencias `D<módulo>.<ordinal>` son las de `decisiones-divergencias-arnes.md`; `MF-n`, las de `mejoras-trabajo-futuro.md`.

## Ámbito de lo que se produjo

**Seis de los siete documentos acotan el componente, no el ERP.** El glosario, el *brief*, el modelo de dominio, el descubrimiento técnico, el modelo de acceso y los riesgos describen la **API de integración de tablas** y lo del ERP que esa API toca; nada más. No son documentación de IDStone Office, y un término, un riesgo o una restricción del ERP que no intervenga en esta integración no está en ellos. **La excepción es el ADR**, cuyo ámbito es el repositorio entero: decide dónde viven los artefactos del arnés, y eso no depende de qué componente se esté construyendo.

El porqué está en **D1.2**, párrafo «Alcance del descubrimiento»: `CONTEXT.md` es *«shared vocabulary for the project»* y el *project* aquí es el componente que `build-brief` descubrió. Un glosario del ERP entero no sería un `CONTEXT.md` más grande: sería otro documento de otro proyecto. La deuda que eso deja —dos glosarios sin árbitro en cuanto una segunda tarea añada su descubrimiento— está recogida en **MF11**.

## Punto de partida

Repositorio de un ERP de ~328.000 líneas en producción, en **Subversion**, sin un solo fichero de contexto para agentes: ni `AGENTS.md`, ni `CONTEXT.md`, ni `.agents/`, ni `.claude/`. Mucho análisis previo escrito —propuesta de arquitectura, análisis de integración, notas internas, borrador v0.5 del contrato— pero **todo fuera del repositorio**, donde ningún agente lo leerá nunca. Sin base de datos de desarrollo, sin proyecto de pruebas *[anotado el 19/11/2026: el proyecto de pruebas apareció el 16/11, en r31949, y es del módulo del ERP. Y donde este resumen decía «sin SQL Server local» la medición era imprecisa: no hay servicio de SQL Server, pero sí LocalDB; lo que falta es la base de datos de desarrollo]*. Nada escrito todavía en el repositorio del producto.

## Cómo se abordó

`build-brief` **sin modificar, en dos pasadas** (**D1.2** = *Decisión* 2 del módulo 1):

   1. **Inspección** de la carpeta de la tarea, el repositorio y el precedente interno.
   2. **Entrevista solo de lo que quedaba abierto**: **una pregunta**, más la confirmación del ADR que exige `build-brief/SKILL.md:150-153`.

## Qué se consiguió, comparado con lo que el curso y la referencia esperaban

Comparación de **estructura**, no de contenido. El producto de la referencia es una tienda con interfaz y el de aquí una API sin ella; eso no entra en la comparación, pero sí explica dos de las filas.

| Lo que prescribe el curso | Proyecto de referencia (`modulo-1`) | Aquí |
|---|---|---|
| **4 documentos obligatorios** —`CONTEXT.md`, `docs/build-brief.md`, `docs/domain-model.md` y `docs/risks-and-open-questions.md`— (`AIExpert.md:251-258` y `:300-311`; `SKILL.md:28-33`) | los 4 | **los 4** ✔ |
| **Esqueleto de secciones fijo** por documento (`references/output-documents.md:17-157`) | cumplido | **cumplido, sección por sección** ✔ |
| `docs/technical-discovery.md`, opcional (`SKILL.md:38`) | creado | **creado** ✔ |
| `docs/user-and-access-model.md`, opcional (`SKILL.md:37`) | **no creado** | **creado** (D1.4) |
| `docs/mvp-scope.md`, opcional (`SKILL.md:39`) | no creado | **no creado**; el corte vive en `## MVP Slice` ✔ |
| `DESIGN.md` (`SKILL.md:40`), y para producto sin interfaz marcar «no aplica» y no crearlo (`SKILL.md:163`) | creado | **no creado, y marcado «no aplica»** (D1.3) — cumple la regla, no la incumple |
| `docs/adr/*.md`, opcional (`SKILL.md:42`) | **no existe en la referencia** | **1 ADR** (D1.1) |
| **6 *skills* en `.agents/skills`** —`build-brief`, `harness-starter`, `feature-spec`, `feature-implementer`, `feature-validator` y `feature-flow`— (`AIExpert.md:284-291`) | las 6 | **las mismas 6**, más el enlace que exige el cliente (D1.5 y D1.8) |
| **Prohibido** crear `AGENTS.md`, `PROGRESS.md` o *backlog* (`SKILL.md:13`) | ninguno | **ninguno** ✔ |
| **Puerta de salida**, 3 comprobaciones (`AIExpert.md:277-282`): producto y dominio · acceso y MVP con sus *non-goals* · incógnitas registradas fuera del hilo | — | **las 3** ✔ |
| **Trabajo del módulo**: 4 tareas (`AIExpert.md:312-322`): elegir una idea · investigarla · diseñar el flujo · ejecutar `build-brief` | las 4 | **solo la 4ª** |

**Resultado**: 7 documentos frente a los 6 de la referencia, con coincidencia en 5 de 6 y las dos diferencias respaldadas cada una por una regla explícita de la propia *skill*.

Y las **dos divergencias estructurales de fondo**, que son lo reutilizable:

   1. **En un repositorio que ya existe, el módulo cambia de peso: inspección en lugar de entrevista.** Tres de las cuatro tareas del módulo (elegir la idea, investigarla con Gemini Notebook, diseñar el flujo con Stitch) presuponen una idea nueva con interfaz; aquí no aplican. Y dentro de `build-brief`, la regla `SKILL.md:16` —inspeccionar antes de preguntar lo que los ficheros responden— pasa de precaución a mecanismo principal: el curso muestra una conversación larga, aquí quedó **una pregunta**. De las ocho decisiones abiertas del análisis previo, **cinco estaban ya respondidas** por los ficheros o el código y las tres restantes no eran del usuario.
   2. **El único artefacto que añadimos sobre la referencia lo pide la plataforma, no el dominio.** El ADR existe porque en Git «el repositorio» y «la línea principal del código» son el mismo sitio y la pregunta de dónde va el arnés no se plantea; en Subversion sí.

## Cambios incorporados después

   * **D1.8 revisada el 16/11**: lo que falla no es el enlace simbólico, es `New-Item -ItemType SymbolicLink` en PowerShell 5.1; `mklink /D` funciona sin elevar. `.claude/skills` es ahora enlace simbólico, con la unión de directorios como alternativa documentada. Y una corrección mayor, ya en `AGENTS.md`: **ningún enlace sobrevive a SVN en Windows**, hay que crearlo en cada copia de trabajo.
   * **MF10** (= *Mejora Futura* 10) nueva: consolidar los dos árboles de OpenSpec, duplicidad que solo tiene este repositorio. Es un hallazgo del descubrimiento, no trabajo del módulo: queda anotada como cuestión abierta, con dueño, en `docs/risks-and-open-questions.md`.
   * Los artefactos se **añadieron a Subversion** (`svn add`, 48 elementos, sin confirmar).
