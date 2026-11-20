# Decisiones de adaptación del arnés: divergencias con el curso

**Proyecto**: despliegue del arnés del curso AI Expert (DevExpert Academy) sobre IDStone Office. **Tarea de referencia**: OT-867 «Web API IDStone (integración escáner tablas)». **Documento hermano**: `mejoras-trabajo-futuro.md`, que recoge lo que se deja fuera a propósito.

## 0. Para qué sirve este documento

Para dos lectores a la vez, y ninguno es secundario: **la evaluación del curso**, que necesita ver que cada desvío respecto al material es una decisión razonada y no un descuido; y **los demás repositorios de la casa**, todos con la misma característica —empezaron hace años, no son productos nuevos—, donde cada decisión debe poder aplicarse leyendo solo este documento. Una decisión que sirva a un lector y no al otro está mal escrita.

## 1. Cómo se lee

**Nomenclatura**: `D<módulo>.<ordinal>` = **Decisión**. `DM.n` para las de método, que no pertenecen a ningún módulo, y `D0.n` para lo anterior al módulo 1. El número dice a qué módulo se refiere y en qué orden se tomó dentro de él, así que el documento se lee de principio a fin. Una decisión superada conserva su número y se marca *Sustituida*, porque el valor está en el rastro.

**Ficha fija**: Estado · Contexto · El curso · Aquí · Por qué · Coste · Regla reutilizable. Cada una se escribe antes de pasar al módulo siguiente, no al final del proyecto.

| Estado | Significado |
|---|---|
| **Acordada** | Decidida y confirmada |
| **Aplicada** | Acordada y ya materializada en el repositorio |
| **Propuesta** | Decidida por el agente, pendiente de confirmación |
| **Candidata a ADR** | Cumple los tres requisitos de `build-brief` §8: difícil de revertir, un mantenedor futuro se preguntaría por qué, había alternativas reales con contrapartidas |
| **Diferida** | Identificada, con el módulo que la resolverá |

### Resumen: las veintisiete decisiones de un vistazo

Cada fila es una ficha de más abajo. Con esta tabla se puede leer el documento a dos profundidades: la tabla da el recorrido completo; la ficha da la medición, el coste y la regla reutilizable.

| | El curso | Aquí |
|---|---|---|
| **DM.1** Un módulo por sesión | Sesiones de tamaño libre | Una sesión es un módulo, y se cierra con la ficha escrita |
| **DM.2** Dos entregables en paralelo | No los pide | Decisiones y trabajo futuro se escriben a la vez que se avanza |
| **DM.3** El arnés es del repositorio | Un producto, un arnés | El arnés es del repositorio; las tareas nuevas entran como *features* |
| **DM.4** ¿Un `build-brief` por tarea? | Demuestra un solo ciclo y no llega a la pregunta | Umbral de cinco criterios, y **pregunta abierta a los tutores** |
| **D0.1** La traza empieza antes del módulo 2 | `PROGRESS.md` nace en el módulo 2 | Fichero externo para los módulos 0 y 1, recuperado y cerrado en el 2 |
| **D1.1** Artefactos en la raíz | Raíz del repositorio Git | Raíz de la copia de trabajo, junto al `openspec/` que ya existía |
| **D1.2** `build-brief` sin modificar | Entrevista desde una idea difusa | La misma *skill*, en dos pasadas: inspeccionar y luego entrevistar |
| **D1.3** Sin `DESIGN.md` | Lo tiene, con imagen | No se crea, y se marca «no aplica», como la *skill* exige |
| **D1.4** Modelo de acceso aparte | No lo tiene | Se separa: los permisos son un riesgo ya materializado en producción |
| **D1.5** *Skills* desde el módulo 1 | El enlace aparece en el módulo 6 | Seis de las siete, desde el módulo 1; `github-flow` no se instala |
| **D1.6** Idioma | No lo decide: obliga a preguntarlo | Español en todo, incluido el arnés |
| **D1.7** Encabezados en inglés | Estructura en inglés, contenido en español | Lo mismo, en los seis documentos y en el ADR |
| **D1.8** El enlace de `.claude/skills` | Enlace simbólico versionado en Git | `mklink /D` sin elevar; ningún enlace viaja por Subversion |
| **D1.9** Cada documento declara su ámbito | Un producto y un descubrimiento: la pregunta no surge | La línea en el documento y la regla en `AGENTS.md`; la *skill*, intacta |
| **D2.1** OpenSpec y `docs/specs/` | Mecanismo propio, sin SDD de terceros | Conviven, separados por unidad y por vida, con la frontera escrita |
| **D2.2** Alcance entregado | Seis módulos sobre 19 *features* | Cuatro *features*, un módulo cada una; el 5 y el 6 especificados |
| **D2.3** Qué es una *feature* | Cortes de una sesión, verificables | Lo mismo: la tarea no es una *feature*, es la lista de trabajo |
| **D2.4** El reparto entre los tres documentos | Solo tiene `PROGRESS.md`: «qué pasó y por dónde seguir» | El avance ahí; el porqué de apartarse y lo que queda fuera, en los dos entregables |
| **D2.5** Puntos de restauración | Una etiqueta de Git por módulo | No hay `tags/` en esta casa: una revisión anotada por módulo |
| **D2.6** La lista de trabajo completa | 19 *features* de una vez, y exige de 12 a 30 | 20, la tarea entera; el alcance se expresa en qué llega a `accepted` |
| **D2.7** Idioma de los encabezados del arnés | Traduce dos ficheros y no traduce otros dos | La misma línea, fichero a fichero: quién lee el encabezado decide |
| **D2.8** La barrera de comprobaciones | `init.sh` con *lint*, tipos, *tests* y compilación | `init.sh` que solo compila, y que dice lo que no puede comprobar |
| **D2.9** `PROGRESS.md` es del repositorio | Plantilla de dos secciones, sesiones tituladas por *feature* | Lo mismo: fuera la línea `Módulo:` y las etiquetas que no se resuelven dentro |
| **D3.1** Una *feature* se confirma entera | Un solo *commit* con el código y el arnés de la *feature* | Lo mismo, con la lista que escribe la *spec*; y nada ajeno a la unidad |
| **D3.2** Un hecho medido lleva su revisión | Repositorio de una sola persona: la pregunta no surge | Repositorio compartido: cada hecho con su revisión, y se recomprueba al abrir la sesión |
| **D4.1** Sin *pull requests* ni CI remota | `gh pr` y GitHub Actions | No existen sobre Subversion: se conserva el mecanismo, no la plataforma |
| **D4.2** Ejercitar la API sin interfaz | Conecta un MCP de terceros, no lo construye | Lo mismo: puente OpenAPI → MCP, más la interfaz de exploración |

## 2. Vocabulario del curso

Términos que el curso usa en inglés y que todo el documento emplea. Dos pares se parecen lo bastante para confundirse.

| Término | Qué significa | Uso aquí |
|---|---|---|
| ***harness*** | El marco que rodea al agente: contexto, capacidades y control | **arnés** |
| ***gate*** | La **barrera de comprobaciones automáticas** que un cambio debe superar: compila, *lint*, tipos, *tests*. En el proyecto de referencia es `init.sh` | **barrera de comprobaciones** |
| **puerta de salida** | Cosa distinta: la **condición de cierre de una *skill***, lo que debe ser verdad para que esa fase termine | **puerta de salida** |
| ***passing*** | El implementador acabó y se autoverificó | *passing* |
| ***accepted*** | Un validador independiente lo contrastó con evidencia. No es lo mismo que *passing* | *accepted* |
| ***split*** | La regla de `build-brief` que dice cuándo un documento opcional **se separa** del conjunto compacto | **separar un documento** |
| ***MVP slice*** | El camino vertical de punta a punta que atraviesa todas las capas y demuestra el comportamiento arriesgado | ***slice*** |
| ***feature*** | Cosa distinta del *slice*: cada **trozo de una sesión** en que se parte ese *slice*. Es una entrada de `feature_list.json` | ***feature*** |

«Corte» se reserva para dos cosas que no son una *feature*: la **línea de corte** del alcance entregado y el **corte de piedra** del dominio.

---

# Decisiones de método

## DM.1 · Un módulo por sesión, con relevo escrito

**Estado**: Acordada

**Contexto.** La sesión de preparación consumió unos 50.000 *tokens* solo en leer el material del curso y explorar el repositorio. Cada módulo es una unidad de trabajo con artefactos y puerta de salida propios: es la frontera natural de una sesión.

**Aquí.** El agente de cada sesión escribe el relevo de la siguiente como último acto. **Con fecha de caducidad**: desde el momento en que existe `PROGRESS.md` —módulo 2— ese papel pasa a `PROGRESS.md`, que vive en el repositorio, donde los agentes sí lo leen, y la serie de relevos externos se detiene.

**Por qué.** No se construye un sistema de relevos paralelo al que el curso ya tiene.

> **Regla reutilizable**: la frontera de una sesión es el módulo, y el relevo entre sesiones es provisional. En cuanto el arnés tenga su propio registro de estado dentro del repositorio, el relevo externo desaparece.

## DM.2 · Los dos entregables se escriben en paralelo a cada módulo

**Estado**: Acordada

**Aquí.** Cada sesión cierra escribiendo, antes de pasar al módulo siguiente, este documento —toda divergencia con el curso, con su por qué y su coste— y `mejoras-trabajo-futuro.md` —lo que se deja fuera a propósito y lo que vendría después—.

**Por qué.** Escritos al final, los dos documentos serían una reconstrucción de memoria: perderían la evidencia medida y el motivo real de cada desvío, que es justamente lo que los dos lectores del §0 necesitan.

## DM.3 · El arnés es del repositorio, no de la tarea; las tareas nuevas se añaden como *features*

**Estado**: Acordada

**Contexto.** Un arnés por tarea no se transpone a nivel de producto: se multiplica. Si el arnés fuera de la tarea, el objetivo del §0 —desplegarlo en las demás soluciones de la casa— no significaría nada, porque no se despliega algo que nace y muere con una tarea.

**El curso.** Un producto, un arnés, una lista. En el proyecto de referencia `AGENTS.md`, `init.sh`, `PROGRESS.md` y `feature_list.json` están en la raíz y describen **el producto**, no una tarea del producto. `$feature-spec` toma la primera *feature* lista por dependencias de esa lista, y no existe un segundo `feature_list.json` en ninguna etiqueta.

**Aquí.** Lo mismo, y comprobado artefacto por artefacto en lugar de afirmado:

| Artefacto | ¿Es del repositorio? |
|---|---|
| `.agents/skills/` (6 *skills*), `.claude/skills` (enlace), `AGENTS.md`, `init.sh`, `PROGRESS.md` | Sí |
| `feature_list.json` | El fichero sí; su contenido es hoy la lista de trabajo de OT-867 |
| `CONTEXT.md` | El fichero sí; su contenido es hoy el glosario del componente (MF11) |
| `docs/build-brief.md` y los demás documentos del módulo 1 | Son documentos **de un descubrimiento**, y los descubrimientos son por componente |

Ninguno de los artefactos del arnés es de la tarea: están todos una sola vez, en la raíz de la copia de trabajo, por encima de `trunk/` (D1.1). Lo que es de la tarea es **el contenido** de dos de ellos, y eso no se arregla con otro arnés: se arregla haciendo crecer los que hay.

> **Regla reutilizable**: cuando entre una tarea nueva, **no se monta un arnés**. Si llega al umbral de DM.4 se ejecuta `build-brief` sobre esa funcionalidad, que produce su descubrimiento; y en cualquier caso sus *features* se **añaden** al `feature_list.json` que ya existe, con `depends_on` hacia lo que haya; su progreso se añade al `PROGRESS.md` que ya existe; y los términos que compartan dos componentes suben al `CONTEXT.md` de producto (MF11). `AGENTS.md`, `init.sh` y las *skills* no se tocan, salvo para corregirlos. Si al llegar la segunda tarea aparece la tentación de crear un segundo `feature_list.json`, un segundo `AGENTS.md` o un segundo `PROGRESS.md`, el arnés estaba mal colocado desde el principio.

---

## DM.4 · ¿Se vuelve a ejecutar `build-brief` con cada tarea nueva? El curso no lo contesta; la *skill* sí

**Estado**: **Propuesta**, pendiente de preguntar a los tutores del curso. Es la única decisión de este documento que se deja abierta a propósito

**Contexto.** DM.3 fija que el arnés es del repositorio y que las tareas nuevas entran como *features*. Queda una pregunta distinta: **¿esa tarea nueva trae su propio `build-brief`?** Aquí la *skill* se ejecutó sobre el componente, no sobre IDStone Office entero.

**El curso demuestra un ciclo, y solo uno.** Medido, no opinado. `build-brief` solo aparece en el módulo 1, con una única referencia hacia atrás desde el módulo 2. En el proyecto de referencia, `CONTEXT.md` tiene **un solo *commit*** en toda su historia; la lista de *features* tiene **19 entradas en `modulo-2` y las mismas 19 en `modulo-6`**, sin una sola diferencia de `id`; el módulo 6 rotula el arnés «✓ No cambia»; y el ejercicio del módulo 4 añade funcionalidad a un proyecto ya hecho **sin ningún paso de descubrimiento**. El curso nunca llega al escenario «la lista se agotó y entra trabajo nuevo» porque en la tienda **la lista es el producto**. No lo esconde: no le hace falta.

**Pero la *skill* es material del curso, y su ficha sí contesta.** Su título cubre *«significant features, or product changes»*; su `description`, *«a replacement for an existing system»*; y su regla de `SKILL.md:16` —*«If a repository or existing docs exist, inspect them before asking questions that the files can answer»*— **solo tiene sentido si se admite ejecutarla sobre un repositorio que ya existe**. Ejecutar `build-brief` sobre una funcionalidad significativa está dentro de su **alcance documentado**; lo que el curso no hace es ejercitarlo así.

**Aquí: un umbral, no una norma general.** No se ejecuta con cada tarea —para corregir un cálculo o añadir una columna, el descubrimiento es el papeleo que la propia *skill* prohíbe—. Se ejecuta cuando la tarea cumple **al menos dos** de estos cinco criterios:

   1. Introduce un **componente nuevo** o un **contrato con el exterior**.
   2. Hay **terceros** o un **modelo de acceso** que hoy no existe.
   3. Trae **vocabulario que el repositorio no tiene**, que habría que inventar o desambiguar.
   4. Se divide en **más de cuatro o cinco** *features* de una sesión.
   5. Tiene **decisiones difíciles de revertir**: plataforma, formato del contrato, almacenamiento.

Si no llega al umbral, la tarea entra como *features* añadidas al `feature_list.json` que ya existe y se especifica con `$feature-spec`, que es literalmente lo que hace el ejercicio del módulo 4. **OT-867 cumple los cinco**, y por eso el módulo 1 no era opcional.

**Qué pasa en una segunda ejecución.** Es la pregunta que decide si el umbral es practicable, y lo primero despeja el miedo: **ninguna *skill* borra un documento**. El único verbo sobre ficheros es *«create or update»* (`build-brief/SKILL.md:17`), `harness-starter` lo prohíbe expresamente —*«read it first and update conservatively. Do not overwrite useful human-authored content»* (`:23`)— y la limpieza de `build-brief` (`:179`) elimina texto redundante **dentro** de un documento, nunca un documento. Tres de los cuatro obligatorios se amplían sin conflicto: `CONTEXT.md` acumula términos, `docs/domain-model.md` acumula entidades y ciclos, y `docs/risks-and-open-questions.md` ya está diseñado para que se le pase por encima otra vez.

**El cuarto es el problema: `docs/build-brief.md` no se puede actualizar *in situ*.** Sus secciones son **singulares** —un `## Problem`, una `## MVP Slice`, un `## Validation Plan`— y el problema de una tarea nueva no es el de OT-867. Actualizarlo pierde el informe anterior; añadirle secciones paralelas lo convierte en el documento denso que la regla del *split* existe para evitar. La salida ya está en el curso, aunque no la explique: `harness-starter` declara su segunda entrada como *«`docs/build-brief.md` **or** `docs/product-brief.md`»* (`:30`), y la plantilla de `product-brief.md` **no tiene `MVP Slice` ni `Validation Plan`**: describe el producto, no una entrega. De ahí tres reglas: `build-brief.md` es el informe de la entrega en curso, una a la vez; **antes** de volver a ejecutar la *skill*, el informe saliente se archiva en `docs/briefs/<tarea>-build-brief.md` —antes y no después, porque si se deja en su sitio la inspección de `SKILL.md:16` lo leerá como contexto vigente—; y **las rutas no se mueven**, porque `harness-starter` y `feature-spec` leen los cuatro documentos por ruta fija. Cuando llegue MF11, la parte estable sube a `docs/product-brief.md`, que `harness-starter` ya acepta. **El archivado no está en el curso**, y hay que decirlo: existe porque la alternativa, perder el informe de la tarea anterior, es peor.

**Por qué.** La lectura más fiel —un `build-brief` una sola vez, sobre el producto entero— produce, con unas 328.000 líneas en producción, un glosario y un informe que nadie lee y que envejecen en una semana. No se descarta por preferencia, **se descarta por calendario**, y sigue siendo el objetivo (MF11). Y el umbral conserva lo que el curso protege —que no haya descubrimiento de adorno— con criterios comprobables en lugar del gusto de quien abra la sesión.

**Coste.** Es divergencia frente al **camino demostrado**, no frente al **alcance documentado**, y esa distinción hay que poder sostenerla con las mediciones de arriba delante. El riesgo concreto es **N descubrimientos y N glosarios sin árbitro**, que es lo que MF11 existe para cerrar: mientras MF11 no se haga, cada descubrimiento nuevo **aumenta** esa deuda, y por eso el umbral son cinco criterios y no uno. Si los tutores responden «un solo descubrimiento por producto», esta decisión pasa a *Sustituida* y MF11 sube de *Media* a **Alta inmediata**, porque entonces el `CONTEXT.md` de producto deja de ser mejora y es requisito.

**Pregunta para los tutores**, con la medición incluida para que nadie tenga que adivinar el contexto:

> En el proyecto de referencia, `build-brief` se ejecuta una vez: `CONTEXT.md` tiene un único *commit* y la lista de *features* tiene 19 entradas en `modulo-2` y las mismas 19 en `modulo-6`. Aquí el repositorio es un ERP de unas 328.000 líneas en producción, donde descubrir el producto entero no es viable, y se ha ejecutado `build-brief` sobre **la funcionalidad** —una API de integración nueva— amparándose en que la ficha de la *skill* cubre *«significant features, or product changes»*. ¿Es ésa la lectura correcta, o la intención es un único descubrimiento por producto y el trabajo posterior entra siempre como *features* añadidas? Y una segunda, de mecánica: `docs/build-brief.md` tiene secciones singulares, así que una segunda ejecución o pierde el informe de la entrega anterior o duplica secciones. ¿Es `docs/product-brief.md` —que `harness-starter` acepta y que no lleva `MVP Slice` ni `Validation Plan`— el reparto previsto, o hay otra forma pensada para que un segundo descubrimiento no se coma el primero?

> **Regla reutilizable**: antes de declarar divergencia, **sepárense dos cosas**: lo que el curso **demuestra** y lo que el curso **documenta**. La *skill* es material del curso tanto como el manual, y su ficha a veces cubre casos que el manual nunca ejercita. Y cuando ni una ni otro contestan, la respuesta honesta no es inventar una norma: es **escribir el umbral, marcar la decisión como propuesta y preguntar**.

---

# Módulo 0

## D0.1 · La traza del progreso empieza antes del módulo 2

**Estado**: Acordada

**Contexto.** D2.4 sitúa el registro del avance en `PROGRESS.md`, pero ese fichero no puede nacer hasta el módulo 2, así que el módulo 0 y el módulo 1 quedaban sin registro. Hueco real, y el vídeo narra desde el principio.

**Aquí.** `progreso.md`, fuera del repositorio, desde la primera sesión, con la misma ficha que `PROGRESS.md`. En el módulo 2 su contenido se traslada a `PROGRESS.md` y el fichero se cierra con una línea que dice dónde continúa (MF8).

**Coste.** Durante dos módulos el registro vive fuera del repositorio, donde ningún agente lo lee. Se corrige en el módulo 2 con la sesión de recuperación.

> **Regla reutilizable**: el registro de avance empieza en la primera sesión, no cuando el arnés lo permite. Si el fichero del curso aún no existe, se lleva fuera del repositorio y se traslada en cuanto exista. Una ficha reconstruida de memoria pierde la evidencia ejecutada y los riesgos abiertos, que es lo que da valor a la narración.

---

# Módulo 1

## D1.1 · Los artefactos del arnés van en la raíz de la copia de trabajo, junto a `openspec/`

**Estado**: Aplicada. **Candidata a ADR**, y el ADR está escrito: `docs/adr/0001-artefactos-del-arnes-en-la-raiz.md`

**Contexto.** El proyecto de referencia está bajo Git; IDStone Office está bajo Subversion, con la disposición clásica `branches/ openspec/ trunk/` y el código en `trunk/`. La pregunta —dónde van `AGENTS.md`, `CONTEXT.md`, `docs/`, `.agents/skills/`, `init.sh`, `PROGRESS.md` y `feature_list.json`— parece de fontanería y no lo es: es el primer sitio donde el curso y un repositorio real no coinciden, y la respuesta fija el patrón para los demás repositorios.

**El curso.** Todo en la raíz del repositorio Git. Verificado en el árbol de la etiqueta `modulo-1`, cuya raíz contiene exactamente `.agents`, `.gitignore`, `CONTEXT.md`, `DESIGN.md` y `docs`.

**Aquí.** La **raíz de la copia de trabajo**, el nodo por encima de `trunk/`, al lado del `openspec/` que ya existe.

**Por qué.** Tres razones, en orden de peso.

   1. **Precedente del repositorio.** `openspec/` ya está por encima de `trunk/`, y lo mismo en los demás repositorios de la casa que se comprobaron: es la respuesta que ya se dio a «dónde viven los artefactos de gobierno», antes de que existiera este proyecto. Poner el arnés en otro sitio crearía **dos ubicaciones de gobierno** y la reconciliación con OpenSpec (D2.1) arrancaría partida en dos.
   2. **El único argumento fuerte a favor de `trunk/` no aplica.** En Git los artefactos viven dentro de la unidad ramificable y viajan con la rama de la *feature*; en Subversion esa unidad es `trunk/`. Pero aquí **no se ramifica para trabajar**: `branches/` son diez entradas de archivo histórico, la más reciente de alrededor de 2019, y el historial son confirmaciones directas contra `trunk/`.
   3. **El papel, no la posición.** Git confunde en un solo sitio «el repositorio» y «la línea principal del código»; Subversion los separa. Los artefactos de procedimiento, estado y descubrimiento son del repositorio entero. El código y la salida de compilación, no.

«Misma posición que el curso» y «misma semántica que el curso» apuntan a sitios distintos, y el empate lo rompe **qué es** el artefacto.

**Coste.** `init.sh` queda un nivel por encima de la solución y tiene que nombrar `trunk/IDStone Office.sln`. Es una ruta, y a cambio deja escrito en el propio *script* qué compila la barrera, en lugar de dejarlo implícito en el directorio desde el que se lanza.

> **Regla reutilizable**: ¿este fichero necesitaría alguna vez ser distinto en dos ramas? **No → raíz del repositorio. Sí → dentro de `trunk/`.** En Git la pregunta no se plantea, porque ambas cosas son el mismo sitio. En los repositorios Subversion de la casa —donde además nadie ramifica para trabajar— la respuesta es «no» para todo el arnés.

## D1.2 · El módulo 1 ejecuta `build-brief` sin modificar, en dos pasadas

**Estado**: Aplicada

**Contexto.** El proyecto de referencia es *greenfield*: una tienda construida de cero desde una idea de una frase. Aquí es lo contrario, un ERP de unas 328.000 líneas en producción al que se añade un componente nuevo, y con mucho análisis previo ya escrito —propuesta de arquitectura, borrador del contrato, análisis del canal de captura, notas del cliente—, **todo él fuera del repositorio**.

**El curso.** `$build-brief` entrevista desde una idea difusa, una pregunta cada vez, hasta producir `CONTEXT.md`, `docs/build-brief.md`, `docs/domain-model.md` y `docs/risks-and-open-questions.md`.

**Aquí.** La misma *skill*, sin tocarla, en dos pasadas: primero **inspeccionar y transcribir**, porque el análisis previo es la materia prima; después **entrevistar solo lo que sigue abierto**, una pregunta cada vez.

**Por qué.** La *skill* ya contempla este escenario, y no de refilón: su `description` cubre *«significant features, or product changes»* y *«a replacement for an existing system»*; su regla de `SKILL.md:16` es exactamente el caso —*«If a repository or existing docs exist, inspect them before asking questions that the files can answer»*— y su §9 autoriza la puerta de calidad *«without re-running the interview»*. Lo que cambia no es **si** se ejecuta el módulo 1, sino **de dónde salen las respuestas**: en la tienda, de la entrevista; aquí, en su mayoría, de los ficheros. Y el módulo 1 no se puede saltar aunque la tarea ya apunte a documentos con especificaciones: se escribieron como propuesta interna y **no están en el repositorio**. Ningún agente leerá nunca una ruta de una unidad de red. La salida del módulo 1 es su forma duradera, dentro del repositorio y legible por un agente.

**Resultado medido.** De las ocho decisiones abiertas de la propuesta de arquitectura, **cinco estaban ya respondidas** en los ficheros o en el código —unidades en centímetros, modelo de autenticación, alcance de los tipos de transacción de terceros, modo de imágenes y quién consume la API—, y las tres restantes no eran contestables desde el equipo de desarrollo. La pasada de entrevista se redujo a **una sola pregunta**, el idioma de los encabezados (D1.7), más la confirmación del ADR que la *skill* exige.

**Alcance del descubrimiento.** Cubre **el componente, no el producto**. `CONTEXT.md` es un glosario del dominio de la integración, no del ERP entero, y lo declara en sus dos primeras líneas. No es un atajo: `CONTEXT.md` es *«shared vocabulary for the project»* (`build-brief/references/output-documents.md`), y el *project* aquí es el componente que `build-brief` descubrió. Un glosario del ERP entero no sería un `CONTEXT.md` más grande, sería otro documento de otro proyecto. La deuda que eso deja —dos glosarios sin árbitro cuando una segunda tarea añada su descubrimiento— está recogida en **MF11**.

**¿Y si se hubiera lanzado la *skill* «a pelo»?** En el procedimiento no habría divergido, porque las dos pasadas **no son un añadido**: están escritas dentro de la *skill*, en las citas de arriba. En el resultado sí, y a peor: el análisis previo no está en el repositorio, así que sin esa materia prima las cinco decisiones que los ficheros ya respondían habrían vuelto a la entrevista y se habrían contestado de memoria en lugar de quedar citadas.

**Coste.** Ninguno en el procedimiento. El riesgo es de ejecución: una entrevista en blanco gastaría tiempo preguntando lo que los documentos ya responden. Las dos pasadas existen para evitarlo.

> **Regla reutilizable**: en un repositorio existente, el descubrimiento **no desaparece: cambia de fuente**. Se inspecciona primero, se transcribe lo asentado y se entrevista solo lo abierto. El análisis previo que no esté dentro del repositorio **no cuenta como contexto**, porque ningún agente lo leerá. Y antes de decidir si una *skill* hay que adaptarla, **se lee entera**: casi todas las adaptaciones que uno cree necesarias ya están contempladas dentro. Lo que de verdad hay que preparar no es la *skill*, es **el material que va a inspeccionar**.

## D1.3 · No se crea `DESIGN.md`

**Estado**: Aplicada

**Contexto.** Una Web API no tiene interfaz visual, y el proyecto de referencia sí tiene `DESIGN.md` y una imagen en `docs/design/`.

**El curso.** La *skill* dice qué hacer en ese caso: *«For a non-visual project, explicitly mark visual design as not applicable in the relevant brief and do not create `DESIGN.md`»* (`SKILL.md:163`).

**Aquí.** No se crea, y se marca. La *skill* no se limita a permitir la omisión: **exige la marca**. Está en los *Non-Goals* y en las *Notes* de `docs/build-brief.md`, y en el *Product Surface* de `docs/technical-discovery.md`, donde se explica con qué se sustituye. Omitir el fichero sin la marca habría sido un hueco, no una decisión. **Lo que no desaparece** con `DESIGN.md` es la necesidad de poder *ver* funcionar la API: eso se resuelve en D4.2.

## D1.4 · `docs/user-and-access-model.md` se separa, y lo decide el descubrimiento

**Estado**: Acordada: se crea

**Contexto.** Es uno de los documentos **opcionales** de `build-brief` (`SKILL.md:35-43`), que se crean *«only when they would reduce confusion rather than add ceremony»*. El proyecto de referencia no lo tiene. Que el producto sea acceso de terceros parecía justificarlo, pero eso es una conclusión a la que debe llegar el descubrimiento, no una premisa.

**Aquí.** Se crea, y por un argumento más fuerte que el previo, aparecido al inspeccionar el código. El criterio de la *skill* es *«when permissions are a product risk»*, y aquí el riesgo **no es hipotético: está materializado en el canal que hoy está en producción**. Sus *endpoints* de escritura no comprueban la autenticación en el código; el procesado confía en el usuario que viaja dentro de los datos; y si ese usuario no existe, actúa como administrador. El documento existe para que el componente nuevo no repita ninguna de las tres, y abre declarándolo. El segundo motivo es de densidad, el otro criterio para separar un documento: meter los permisos del ERP, los *scopes* por método, el mínimo privilegio en el NAS, el vencimiento del testigo y el ámbito por almacén dentro del descubrimiento técnico lo habría convertido en el documento denso que la regla existe para evitar.

**Coste.** Un fichero más que mantener, y un artefacto más que el vídeo tiene que saber explicar. A cambio, el modelo de acceso se puede leer sin leer la plataforma, que es lo que necesita quien revise la seguridad.

> **Regla reutilizable**: no se generalice. Este documento se separa porque el producto **es** acceso de terceros con escritura sobre existencias. En una funcionalidad interna, la posición mínima dentro del descubrimiento técnico basta, y crear el fichero sería la ceremonia que la *skill* manda evitar.

## D1.5 · Las *skills* se instalan en `.claude/skills/` desde el módulo 1

**Estado**: Aplicada. El mecanismo del enlace se resolvió en **D1.8**

**Contexto.** El proyecto de referencia guarda las *skills* en `.agents/skills/`, la convención portable, y añade `.claude/skills` como enlace a `../.agents/skills`.

**El curso.** El enlace aparece **en la etiqueta del módulo 6**. Verificado: `git diff --stat modulo-5 modulo-6` lo muestra como fichero nuevo de una línea, y `git ls-tree HEAD .claude/skills` da modo `120000` apuntando a `../.agents/skills`.

**Aquí.** Se instalan **desde el módulo 1**.

**Por qué.** El momento en que el enlace aparece en el repositorio de referencia es **un accidente del cliente que usaba el curso**, no una decisión de método: aquel cliente lee `.agents/skills/` de forma nativa y por eso no lo necesitó hasta el módulo 6. El cliente usado aquí carga *skills* de `.claude/skills/` (proyecto) y `~/.claude/skills/` (usuario), y **no** de `.agents/skills/`. Y el argumento de fondo: el curso explica las *skills* en el módulo 2 y el arnés empieza en el módulo 2. **No hay arnés sin *skills***. Tratar el enlace como «cosa del módulo 6» sería fidelidad a una confirmación, no al método.

**Qué se instaló.** **Seis de las siete *skills***: `build-brief`, `feature-flow`, `feature-implementer`, `feature-spec`, `feature-validator` y `harness-starter`. **`github-flow` no se instala**, por dos motivos que apuntan igual: es la única que no existe en la primera etiqueta del proyecto de referencia —aparece en la cuarta— y, por D4.1, su contenido queda fuera del alcance entregado sobre un repositorio Subversion. Instalarla dejaría una capacidad que nadie puede ejercer. Comprobado: `git ls-tree -d --name-only modulo-1 .agents/skills/` devuelve exactamente esas seis.

**Consecuencia práctica.** Una sesión solo resuelve `/build-brief` o `/harness-starter` si su **carpeta de trabajo es la raíz de la copia de trabajo**, donde vive `.claude/skills`. Una sesión abierta sobre la carpeta de la tarea ve los dos entregables pero no las *skills*, y la invocación no resuelve. La configuración correcta es: carpeta de trabajo la raíz del repositorio, y la carpeta de la tarea **añadida** como secundaria, para poder escribir los dos entregables en paralelo (DM.2).

> **Regla reutilizable**: las *skills* van en `.agents/skills/` como fuente única, y además en la ubicación que exija **el cliente que se vaya a usar**, desde el primer módulo. El sitio donde el curso lo hizo depende de su cliente, no del método. Y la sesión se abre donde está instalado el arnés: si la documentación de la tarea vive fuera del repositorio, se añade como carpeta secundaria, no se convierte en la principal.

## D1.6 · Idioma: español en todo, incluido el arnés

**Estado**: Acordada

**Contexto.** `build-brief` obliga a preguntar el idioma de los documentos y prohíbe deducirlo del idioma de la conversación (`SKILL.md:19`).

**Aquí.** **Español en todos los ficheros del proyecto**: los entregables, los documentos del descubrimiento y también el arnés (`AGENTS.md`, `PROGRESS.md`, `docs/specs/*.md`, `docs/adr/*.md`). Las excepciones no son de idioma sino de sintaxis: identificadores, nombres de fichero, claves de JSON y valores de estado (`not_started`, `passing`, `accepted`, `revise`, `block`) se quedan como están.

**Por qué.** Para alinearse con la preferencia que el repositorio ya tiene escrita: `openspec/config.yaml` exige «Idioma: español para *proposal*, *design* y *tasks*». Un arnés en inglés junto a un OpenSpec en español serían dos convenciones en el mismo repositorio. Se valoró el inglés por ahorro de contexto —el español consume más *tokens* y los ficheros del arnés se leen al arrancar cada sesión—, pero el ahorro medido es moderado, unos 300 *tokens* por arranque, y la coherencia con el repositorio pesa más; además los términos del dominio —tabla, acabado, proceso, transacción— son españoles, y un arnés en inglés los mezclaría en cada frase.

**Coste.** Más *tokens* por arranque de sesión. Se compensa con la disciplina de tamaño que el curso ya exige para `AGENTS.md`: 30-50 líneas al empezar, techo de unas 150, límite duro de 32 KiB con truncado silencioso.

> **Regla reutilizable**: el idioma del arnés es el del repositorio, no el del agente. Si el repositorio ya tiene una convención escrita, se respeta. Y si el arnés crece hasta notarse en el contexto, lo que hay que recortar es el contenido, no el idioma.

## D1.7 · Encabezados de sección en inglés, contenido en español

**Estado**: Acordada. Precisada por **D2.7**

**Contexto.** Las plantillas de `build-brief` traen **encabezados de sección fijos en inglés** —`## Problem`, `## MVP Slice`, `## Core Concepts`, `## Revocation / Expiry`—. Traducirlos o no es una decisión, porque afecta a los seis documentos y no es reversible sin reescribirlos.

**El curso.** El proyecto de referencia ya resuelve este caso, **y a favor del inglés**: su `CONTEXT.md` y sus cuatro documentos de descubrimiento llevan el contenido en español bajo los encabezados en inglés de la plantilla. Comprobado en `git show modulo-1:CONTEXT.md` y `git show modulo-1:docs/build-brief.md`.

**Aquí.** Lo mismo: **estructura en inglés, contenido en español**, en los seis documentos del módulo 1 y en el ADR.

**Por qué.** Tres razones que apuntan al mismo sitio. **Es lo que ya hace el repositorio**: `openspec/config.yaml` dice literalmente «Las specs usan el vocabulario RFC 2119 en inglés (SHALL / NOT SHALL) dentro de frases en español», así que la casa ya decidió que el vocabulario estructural va en inglés dentro de prosa española, y D1.7 no es una excepción a D1.6 sino la misma regla aplicada desde antes. **D1.2 exige ejecutar la *skill* sin modificarla**, y los encabezados son parte de la plantilla, que es parte de la *skill*: traducirlos sería editarla por la puerta de atrás. Y **comparabilidad**, que es parte del entregable: el vídeo muestra estos documentos junto a los del proyecto de referencia, y con los mismos encabezados la comparación es de contenido, mientras que con encabezados traducidos la primera pregunta de quien mire las dos pantallas es por qué no coinciden.

**Coste.** Ninguno respecto al curso: esto **es** lo que hace el curso. El coste es frente a una lectura literal de D1.6, y es de aspecto: documentos bilingües en la primera línea de cada sección.

> **Regla reutilizable**: el idioma del **contenido** es el del repositorio (D1.6); el de la **estructura** es el de la plantilla que la define. Encabezados, identificadores, nombres de fichero, claves de JSON, valores de estado y vocabulario normativo se quedan como están. Si hay que traducir un encabezado para entenderlo, el problema es el contenido de la sección, no su título.

## D1.8 · `.claude/skills` es un enlace simbólico creado con `mklink /D`

**Estado**: Acordada. Resuelve el coste que D1.5 dejaba anotado

**Contexto.** D1.5 instala las *skills* en `.claude/skills/` y deja un coste sin resolver: un enlace simbólico requiere privilegios o modo de desarrollador, y Subversion no versiona enlaces como Git.

**El curso.** Un enlace simbólico `.claude/skills` → `../.agents/skills`, de una línea, modo `120000` en Git.

**Aquí.** Un **enlace simbólico de directorio**, igual que el proyecto de referencia, creado desde `cmd` y sin elevar:

```
cd /d "C:\svn\computel\IDStone Office\.claude"
mklink /D skills ..\.agents\skills
```

**Nunca** con `New-Item -ItemType SymbolicLink`: en Windows PowerShell 5.1 esa orden exige elevación aunque el modo desarrollador esté activado, porque no pasa la bandera `SYMLINK_FLAG_ALLOW_UNPRIVILEGED_CREATE`. En una máquina **sin** modo desarrollador, donde `mklink /D` falla, la alternativa es una **unión de directorios**, que no pide privilegio alguno y exige destino absoluto: `mklink /J skills "C:\svn\computel\IDStone Office\.agents\skills"`.

**Por qué.** Se probaron las cuatro opciones y solo dos sirven:

| Opción | Resultado medido |
|---|---|
| `New-Item -ItemType SymbolicLink` | **Falla**: «Administrator privilege required for this operation» |
| `mklink /D` | **Funciona sin elevar** donde el modo desarrollador está activado |
| `mklink /J` (unión de directorios) | **Funciona sin elevar y sin modo desarrollador** |
| Copiar el directorio | Funciona, pero deja **dos copias que se desincronizan en silencio** |

Los dos que funcionan dan lo mismo —una sola fuente de verdad— y ninguno pide elevación. Se elige el enlace simbólico porque **se ve**: lleva la flecha de acceso directo en el icono y `dir /AL` lo marca como `<SYMLINKD>` con el destino al lado. Una unión no se anuncia —el Explorador la muestra como una carpeta corriente—, de modo que quien borre algo dentro vería desaparecer el original sin entender por qué. Entre dos mecanismos equivalentes, se elige el que se ve.

**Ningún enlace viaja por Subversion en Windows.** Comprobado sobre un repositorio desechable creado al efecto (`svnadmin create`, cliente 1.14.2), no sobre el de la empresa:

| Prueba | Resultado |
|---|---|
| `svn add` de la unión y del enlace simbólico | Ambos se añaden, y Subversion les pone `svn:special` por su cuenta |
| `svn commit` de los dos, y del enlace solo | **Falla**: `E145001: Node ... has unexpectedly changed kind` |
| Enlace subido por un cliente Unix y descargado en Windows | Llega como **fichero de texto de 11 bytes** con el contenido `link target`. No es un enlace |

La razón: Subversion modela un enlace simbólico como **un nodo de tipo fichero** cuyo contenido es `link <destino>`. Un enlace de directorio de Windows no es eso, y el cliente de Windows no materializa enlaces al descargar; Git, en cambio, versiona el enlace de verdad y `git clone` lo recrea. **La conclusión importa para el reparto**: no es la regla `svn:ignore` quien deja el enlace fuera del control de versiones, es Subversion sobre Windows; la propiedad solo evita el ruido en `svn status`. Y esa propiedad ya estaba: el `svn:ignore` de la raíz **contenía `.claude` antes de que este trabajo empezara**, puesto en la confirmación que montó OpenSpec, cuyo mensaje lo dice con todas las letras. Así que el reparto sale solo: **`.agents/skills/` se versiona** como fuente única y viaja a cualquier copia de trabajo; **`.claude/skills` no se versiona** y es local de cada máquina, porque depende del cliente de cada desarrollador y no del repositorio.

**Coste.** Dos. El enlace **hay que crearlo en cada copia de trabajo**: es una línea, pertenece al arranque del entorno y el módulo 2 la recoge en `AGENTS.md`; mientras no esté escrita, quien actualice el repositorio no verá cargarse sus *skills* sin saber por qué. Y **el enlace no protege el destino**: no es una copia ni una vista de solo lectura, así que borrar o editar algo dentro de `.claude\skills` borra o edita el fichero real y versionado de `.agents\skills`. Se asume porque una copia de trabajo recién actualizada **no contiene `.claude` en absoluto** —está ignorado—, así que el enlace solo existe donde alguien lo crea a propósito; porque el daño es **visible y reversible**, ya que un borrado o una edición aparecen como `D` o `M` y `svn revert` los deshace, mientras que copiar el directorio falla en silencio; y porque es **el comportamiento que el curso quiere**, una sola fuente de verdad. La mitigación es que la línea de `AGENTS.md` dice también **que se edita en `.agents/skills/`, nunca en `.claude/skills`**.

> **Regla reutilizable**: en Windows, para apuntar la ubicación que exige el cliente a la fuente única de las *skills*, **enlace simbólico con `mklink /D` desde `cmd`**, nunca `New-Item -ItemType SymbolicLink` en PowerShell 5.1: lo que exige elevación es esa orden, no Windows. Sin modo desarrollador, **unión de directorios** (`mklink /J`). Se versiona la fuente y se ignora el enlace, porque el enlace depende del cliente de cada máquina. Ningún enlace viaja por Subversion en Windows, así que se crea en cada copia de trabajo y la orden vive en `AGENTS.md`. Y antes de dar por hecho que el control de versiones estorba, **se lee su `svn:ignore`**: puede estar resuelto ya.

---

## D1.9 · Cada documento de descubrimiento declara su ámbito, y `AGENTS.md` lo hace cumplir

**Estado**: Aplicada el 19/11/2026. Precisa D1.2, no la sustituye

**Contexto.** D1.2 fija que el descubrimiento cubre **el componente, no el producto**, y lo argumenta. Pero esa frase vive en este documento, que **ningún agente lee**: está fuera del repositorio. Dentro, cuatro de los seis documentos lo declaraban en su cabecera —`CONTEXT.md`, el *brief*, el modelo de dominio y el descubrimiento técnico— y dos no: `docs/risks-and-open-questions.md` no decía nada y `docs/user-and-access-model.md` lo insinuaba. El riesgo no es de lectura humana. Es que la segunda tarea abra el fichero de riesgos, vea un documento de riesgos del repositorio y **añada los suyos**, porque nada se lo impide; el resultado es un documento mezclado sin árbitro, que es la forma exacta del estropicio que MF10 documenta para `openspec/` y que MF11 existe para evitar en el glosario.

**El curso.** **No plantea la pregunta.** Su proyecto de referencia tiene un producto y un descubrimiento, así que el ámbito de un documento es el del repositorio y no hay nada que declarar. La plantilla (`build-brief/references/output-documents.md`) define los `##` de cada fichero y no contempla una línea de ámbito, ni la necesita.

**Aquí.** Dos cosas, y la segunda es la que importa:

   1. Los dos documentos que faltaban **declaran su ámbito en la primera línea**, antes del primer `##`, con la misma forma que ya tenían los otros cuatro.
   2. **`AGENTS.md` lleva la regla**: los documentos de descubrimiento acotan el componente y cada uno lo declara en su primera línea; al actualizarlos se conserva esa línea y no se mezcla en ellos material de otro componente; `docs/adr/` es la excepción, porque su ámbito es el repositorio entero.

La *skill* **no se toca**.

**Por qué.** Tres razones, en orden de peso.

   1. **Quien va a reescribir estos documentos no es `build-brief`**, que se ejecutó una vez: es `feature-implementer` en su paso de documentación durable, con `feature-validator` detrás comprobándolo. Los dos arrancan leyendo `AGENTS.md`. Una línea dentro del fichero, sola, es frágil —se borra por parecer preámbulo—; una línea **más** una regla en el fichero que todo agente lee, no.
   2. **Tocar la plantilla de la *skill* sería la divergencia que D1.2 existe para evitar**, y además rompería la comparación fichero a fichero con el proyecto de referencia, que es la mitad del valor del entregable. `AGENTS.md`, en cambio, es el mecanismo que el propio curso da para las reglas de la casa, y es nuestro.
   3. **La línea es descriptiva, no normativa**: dice qué cubre el documento, no dónde escribe la tarea siguiente. Eso último es MF11 y DM.4, y no se decide en un pie de página.

**Coste.** Dos líneas de prosa que no están en la plantilla, y que alguien que compare fichero a fichero con el proyecto de referencia verá de más. Es visible y barato. La alternativa —un documento cuyo ámbito solo existe por convención compartida— se paga una sola vez y **en silencio**.

> **Regla reutilizable**: cuando un repositorio alberga más de un componente, **el ámbito de un documento es parte del documento** y se escribe en él, no solo en la decisión que lo fijó. Y la regla que obliga a conservarlo va en el fichero de instrucciones del repositorio, porque quien la va a incumplir es un agente que **no leerá el registro de decisiones**. Un ámbito que solo vive en una convención se rompe con el primero que no la conozca, y se rompe sin ruido.

---

# Módulo 2

## D2.1 · OpenSpec y `docs/specs/` conviven, con la frontera escrita

**Estado**: Acordada

**Contexto.** El proyecto de referencia **no usa ningún *framework* SDD de terceros**: su mecanismo es propio, `docs/specs/<feature-id>.md`, escrito por `$feature-spec`. Este repositorio dirige todo desarrollo con **OpenSpec**, y lo demuestra con cuatro *specs* y diez cambios. Las tres opciones eran escribir las *specs* del arnés dentro de `openspec/changes/`, hacerlas convivir, o apartar OpenSpec para este trabajo.

**Aquí.** **Conviven**, y no es un empate: cada uno responde a una pregunta distinta.

| | `docs/specs/<id>.md` | `openspec/` (el de la raíz) |
|---|---|---|
| Unidad | Una *feature* de una sesión | Una capacidad del sistema |
| Pregunta | ¿Qué construye exactamente el agente siguiente? | ¿Qué garantiza IDStone? |
| Vida | Muere cuando la *feature* se acepta | Sobrevive a todas las *features* |
| Quién lo escribe | `$feature-spec` | Quien propone un cambio, con el proceso de la casa |
| Quién lo lee | `$feature-implementer` y `$feature-validator` | Cualquiera que vaya a tocar esa capacidad |

La regla, en una dirección y sin excepciones: una *feature* que **añade o cambia una capacidad de IDStone** abre su cambio en el árbol de OpenSpec de la **raíz**, y su `docs/specs/<id>.md` lo nombra por ruta en *Durable Documentation Impact*; una *feature* que solo construye el componente escribe **únicamente** `docs/specs/<id>.md`. Nunca se escribe en el árbol de OpenSpec duplicado que hay bajo `trunk/` (MF10). Aplicada al alcance entregado: F1 y F2 no cambian ninguna capacidad, así que llevan `docs/specs/` y nada más; las dos primeras *features* que abrirán cambio de OpenSpec están ya identificadas en `feature_list.json` —`validacion-previa-coste`, que debe respetar la *spec* `costes-produccion-pda`, e `idempotencia-clave-y-restriccion-unica`, el único cambio de esquema que el componente necesita—.

**Por qué no las otras dos.**

   1. **Escribir las *specs* del arnés dentro de OpenSpec obligaría a editar las *skills*, que es lo que D1.2 prohíbe.** Las cuatro *skills* del ciclo traen la ruta escrita dentro: `feature-spec/SKILL.md:16`, `feature-implementer/SKILL.md:28`, `feature-validator/SKILL.md:28` y `feature-flow/SKILL.md:61`. Y además metería un plan de implementación desechable dentro del almacén de especificaciones durables, que es lo contrario de lo que `openspec/specs/` significa.
   2. **Apartar OpenSpec rompería el proceso de la casa justo donde más caro sale.** La *spec* `costes-produccion-pda` fija la prioridad de búsqueda de tarifa, el filtro por máquina y la independencia por línea, y es **la lógica que la validación previa de coste de la API tiene que respetar**. Apartarla sería garantizar que alguien la reimplemente sin haberla visto.
   3. **Hay precedente propio de que el solapamiento no existe.** El `openspec/config.yaml` de la raíz declara el contexto del producto entero —familia, migración, instalador, subsistema fiscal—: ni una línea de eso cabe en un `docs/specs/<id>.md`, y ningún plan de ficheros a tocar cabe en una *spec* de OpenSpec.

**Coste.** Se escribe dos veces cuando una *feature* toca una capacidad, y dos documentos que describen lo mismo divergen si nadie lo impide. Lo que lo impide aquí es que **no describen lo mismo**: uno dice qué garantiza el sistema y el otro qué hace este agente esta sesión. El coste es real, y lo que lo eliminaría está anotado como **MF12**. Segundo coste, de orientación: quien llegue nuevo ve dos carpetas de especificación y no sabe cuál leer, y por eso `AGENTS.md` nombra las dos y dice cuál es la viva.

> **Regla reutilizable**: cuando un repositorio ya tiene su propio mecanismo de especificación, **no se elige entre él y el del arnés: se separan por unidad y por vida**. La especificación de la casa describe lo que el sistema garantiza y sobrevive; la del arnés describe lo que construye un agente en una sesión y muere al aceptarse. La referencia de uno al otro se escribe **en una sola dirección** —de la *feature* hacia la capacidad, nunca al revés— y se decide contra el árbol vivo, aunque haya más de uno. Y antes de proponer mover las *specs* del curso a otro sitio: **leer si la ruta está escrita dentro de las *skills***. Casi siempre lo está.

## D2.2 · El alcance entregado: módulos 1 a 4, con el 5 y el 6 especificados y diferidos

**Estado**: Acordada

**Contexto.** El entregable del curso no es código: es **un vídeo** que explique qué se hizo y por qué. No se puede mostrar código fuente —IDStone es un producto comercial de la empresa—, pero sí los artefactos del arnés y las herramientas funcionando. La pregunta que decide el alcance no es «¿responde algo en pantalla?», sino **qué módulos puede reclamar el vídeo con honestidad**.

**El curso.** Medido sobre las etiquetas del proyecto de referencia:

| Etiqueta | *Specs* | *Features* `accepted` | Ficheros en `src` | Sobre qué se demuestra el módulo |
|---|---|---|---|---|
| `modulo-1` | 0 | 0 | 0 | Solo descubrimiento: todavía no existe ninguna *feature* |
| `modulo-2` | 1 | 0 | 0 | El arnés, más la **lista completa de 19 *features*** escrita de una vez |
| `modulo-3` | 1 | **1** | 3 | Implementador y validador, sobre esa única *feature* |
| `modulo-4` | 7 | 7 | 28 | El flujo encadenado, sobre **seis *features* nuevas** |
| `modulo-5` | 11 | 11 | 49 | Cuatro *features* de IA |
| `modulo-6` | 19 | 19 | 100 | El *host*, sobre un lote de ocho |

Tres hechos de esa tabla cambian el plan: `feature_list.json` **se escribe una sola vez, completo, en el módulo 2** —las 19 entradas están ya ahí como `not_started`, y el fichero crece en detalle pero nunca gana una *feature*—; una sola *feature*, `bootstrap-stack`, **cubre los módulos 2 y 3 y ninguno más**; y **el módulo 4 nunca se demuestra sobre ella**, porque el flujo necesita otra *feature* sobre la que correr, ya que la primera se condujo a mano para enseñar los papeles.

**Aquí.** Cuatro *features* del alcance entregado, cada una cubriendo exactamente un módulo:

| # | *Feature* | Módulo que cubre | ¿Necesita base de datos? | Alcance |
|---|---|---|---|---|
| **F1** | `api-bootstrap`: compila desde la barrera, arranca, `GET /health`, documento OpenAPI y su interfaz de exploración | Módulos 2 y 3, y el §10 del 4 | **No** | **Dentro** |
| **F2** | Códigos de error públicos y deterministas: un conjunto cerrado más un respaldo `desconocido` | **El flujo encadenado del módulo 4**, por ser la segunda *feature* sobre la que corre sin conducción manual | **No** | **Dentro** |
| **F3** | El mismo contrato resuelto con un modelo: salida estructurada sobre ese conjunto cerrado, con el respaldo como guarda | Módulo 5 | **No** | **Ambicioso** |
| **F4** | *Host* mínimo: tabla de flujo, tabla de reglas, instantánea antes y después de cada papel, y el *host* escribiendo `accepted` | Módulo 6 | No | **Fuera, especificado** |

**El mínimo exigible queda fijado en el contenido del módulo 3**, porque el módulo 5 trata de herramientas que pueden necesitarse o no y el módulo 6 es un extra. Así que F1 y F2 son el entregable, y **F3 deja de ser un objetivo al que sacrificar calidad**: si no entra, no es una carencia del proyecto.

**Matiz que no conviene perder.** Con F1 aceptada, **la maquinaria del flujo encadenado ya está entera**: la *skill* `feature-flow`, la barrera, los tres papeles y `feature_list.json` con F2 en `not_started` y su `depends_on` satisfecho. No falta ninguna pieza; falta una *feature* sobre la que correr. Así que el vídeo puede afirmar que el arnés **ya permite** el flujo, mostrando la *skill* instalada, sus puertas de salida y la siguiente *feature* desbloqueada, pero tiene que enunciarlo en su forma más débil: **instalado y verificable, no ejercitado**.

**Por qué.** F2 y F3 comparten contrato a propósito: mismo punto de entrada, mismo conjunto cerrado, dos motores, y el determinista sirve de oráculo contra el que se comprueba el otro —la forma más limpia de mostrar qué añade un modelo y por qué el respaldo no es opcional—. Además mantiene el módulo 5 **fuera de la base de datos**, cosa que ninguna otra *feature* candidata consigue, y la base de datos de desarrollo es precisamente la pregunta sin responder. F1 tampoco necesita base de datos, ni carga de módulos de DevExpress, ni seguridad de XAF: todo eso pertenece a la *feature* siguiente, la prueba de concepto, y parte el riesgo donde lo parte el curso. Y F4 es el módulo 6 honesto: el *host* del curso es un *script* de 542 líneas, pero el mecanismo que enseña es una sola regla —**lo que ha cambiado es lo que se ha tocado, diga lo que diga el papel**—, y eso es una instantánea antes y después de cada papel, una tabla de flujo, y el *host* escribiendo `accepted` para que ningún papel pueda concedérselo a sí mismo.

**Coste.** **El vídeo reclama cuatro módulos, no seis.** Es el coste real y no se disimula: se declara en el propio vídeo y en la lista de trabajo. Lo que lo hace defendible es que la diferencia entre **diferido** y **omitido** queda escrita: el módulo 5 está especificado como F3 y desarrollado en MF3; la mitad remota del módulo 4 está en MF1; el módulo 6 está especificado como F4.

> **Regla reutilizable**: la primera *feature* de un repositorio antiguo es **la que no necesita base de datos**: que el proyecto exista, compile desde la barrera, arranque y responda algo. Todo lo demás —esquema, seguridad, carga de módulos— es la segunda. Y antes de fijar el alcance, **se cuenta sobre el proyecto de referencia cuántas *features* consume cada módulo**: un módulo que se demostró sobre seis no se demuestra sobre una. Una *feature* que está en la lista con su *spec* y su motivo de aplazamiento demuestra que se entendió el módulo; una que no aparece, no.

## D2.3 · Qué es una *feature* cuando se añade funcionalidad a un producto que ya existe

**Estado**: Acordada. No es una divergencia sino una adaptación, y se registra porque la pregunta se repetirá en cada repositorio de la casa

**Contexto.** El proyecto de formación es un producto entero construido de cero: sus 19 *features* **son la tienda completa**. Aquí es una funcionalidad nueva dentro de un ERP que lleva décadas funcionando. De ahí la pregunta: ¿`feature_list.json` tiene **una** entrada, la tarea, o **tantas como partes** admita?

**El curso.** Primero, dónde nace el fichero: **no en el módulo 1**. `$harness-starter` genera los cuatro ficheros del arnés en el **módulo 2**, y `build-brief` prohíbe crearlos antes (`build-brief/SKILL.md:13`). Comprobado:

```
git ls-tree --name-only modulo-1   ->  .agents  .gitignore  CONTEXT.md  DESIGN.md  docs
git ls-tree --name-only modulo-2   ->  + AGENTS.md  PROGRESS.md  feature_list.json  init.sh
```

Después, la granularidad, que la puerta de salida del módulo 2 fija por escrito: «Dependencias y granularidad: sin ciclos ni *features* fantasma; **cortes de una sesión, verificables**», y el material lo completa —una *feature* es «un resultado comprobable, con límites claros y una comprobación que **otra persona pueda repetir**»—. La prueba de cuán fino es el corte está en su propia lista: **`catalog-list`, `catalog-filter` y `catalog-sort` son tres entradas distintas**, no una *feature* «catálogo».

**Aquí.** **Tantas entradas como *features* de una sesión verificables admita la tarea. No una.** OT-867 no es una *feature*: es la lista de trabajo, y las *features* son sus partes. Una entrada única llamada «Web API IDStone» fallaría las dos mitades de la regla —nadie la termina en una sesión, y su lista de `verification` no se puede escribir en cuatro líneas que otra persona repita—: sería el *epic* sin trocear que la puerta de salida rechaza.

**Advertencia: en D2.2 el mapa *feature*↔módulo está invertido a propósito.** En el curso **las *features* no se corresponden con los módulos**: el módulo 3 consume una, el 4 seis, el 5 cuatro y el 6 ocho. El tamaño de una *feature* lo decide el dominio y las dependencias, nunca el plan de estudios. La tabla de D2.2 —cuatro *features*, un módulo cada una— es **una inversión impuesta por el vídeo**, legítima como estrategia de demostración y que hay que decir en voz alta, porque **en cualquier otro repositorio la lista no se trocea así**.

**Coste.** Quedan dos unidades de medida en paralelo: la **tarea** sigue siendo la unidad de gestión en el gestor de incidencias, y la ***feature*** es la unidad de trabajo en `feature_list.json`. Se concilian anotando el `id` de la *feature* en el mensaje de confirmación.

> **Regla reutilizable**: una entrada de `feature_list.json` es **trabajo de una sesión que otra persona pueda verificar**, no una funcionalidad del producto ni una tarea del gestor de incidencias. Si no se puede escribir su lista de `verification` en cuatro o cinco comprobaciones repetibles, está sin trocear. Y al revés: si una entrada no deja nada comprobable al terminar, no es una *feature*, es un paso dentro de otra.

## D2.4 · El reparto entre los tres documentos: avance, decisiones y trabajo futuro

**Estado**: Acordada. La **forma** de `PROGRESS.md` la fija D2.9, que sustituye a esta ficha en ese punto

**Contexto.** Hay que poder explicar, al terminar cada módulo, qué se ha conseguido, porque es el material del vídeo. Los dos entregables recogen *decisiones* y *trabajo futuro*; faltaba decir dónde se registra el **avance**. No hace falta un documento nuevo: es un artefacto del curso que ya estaba previsto.

**El curso.** `PROGRESS.md` es «qué pasó y por dónde seguir» (`AIExpert.md:2111`), uno de los cuatro ficheros del arnés que nacen en el módulo 2, y el único puramente narrativo: en el proyecto de referencia crece de 23 a 518 líneas a lo largo de los módulos. No existe nada parecido a estos dos entregables, porque el curso no tiene de qué apartarse.

**Aquí.** El reparto es **por pregunta**: `PROGRESS.md` registra el **avance** —¿qué pasó y por dónde sigo?—; `decisiones-divergencias-arnes.md`, las **decisiones** que se apartan del curso o lo adaptan —¿por qué no se hizo como el curso?—; y `mejoras-trabajo-futuro.md`, lo que **queda fuera** y por qué merece hacerse —¿qué falta y qué valdría?—. Eso es lo que significa «en paralelo al avance de cada módulo»: los dos entregables se escriben **a la vez que** se avanza, no que contengan el avance.

La traza por módulos —qué módulo cubre cada parte del trabajo, qué puerta de salida obligó a qué— vive en estos dos entregables y en el guion del vídeo, nunca en `PROGRESS.md`: el porqué está en D2.9.

**Coste.** La disciplina de cerrar cada módulo escribiendo las tres fichas, en vez de dejarlo para el final.

> **Regla reutilizable**: el avance va en el registro del repositorio y **tiene un solo sitio**; lo que se escribe aparte es el *porqué* de apartarse de la guía y el trabajo que queda fuera. Los tres se escriben al cerrar, no después.

## D2.5 · Puntos de restauración: una confirmación por módulo, con marca en el mensaje

**Estado**: Acordada, pendiente de la primera confirmación

**Contexto.** El arnés entra en un repositorio de producción compartido, y lo hace por motivos del curso: el entregable es el arnés, no IDStone Office. De ahí la necesidad de poder **volver al estado en que cada módulo dejó el repositorio** sin arrastrar el trabajo de los demás, y de poder retirarlo entero.

**El curso.** El proyecto de referencia es Git y lo resuelve con **etiquetas**, `modulo-1` … `modulo-6`, una por módulo. Todas las mediciones de la sesión de preparación se hicieron contra ellas.

**Aquí.** No hay traducción directa, y la razón se da con la medición delante: **el proyecto tiene `trunk/` y `branches/`; lo que no tiene es `tags/`**, y tampoco lo tienen los demás proyectos del repositorio. **No se etiqueta en esta casa.** Crear `tags/` sería barato y estaría en su sitio —hermana de `trunk/` y `branches/`, dentro del propio proyecto, sin tocar nada de nadie—, pero es **estrenar una convención en un repositorio compartido**, y eso lo decide quien manda en el repositorio, no el arnés. Así que el punto de restauración es **la revisión**, el identificador natural de un estado del árbol en Subversion. Tres reglas:

   1. **Una confirmación por módulo**, al cerrarlo, y **solo con las rutas del arnés**. Nunca mezclada con código de producto. Si un módulo necesita dos confirmaciones, la última es la del punto de restauración y así se anota. **Precisada por D3.1** desde `api-bootstrap`: cuando la unidad de trabajo es una *feature*, ésta confirma su propio código de producto junto a su arnés en una sola revisión, y la lista de ficheros la escribe su *spec*.
   2. **Mensaje con marca fija**, para que el registro sea buscable: `[OT-867][arnes][modulo-N] <qué deja comprobable>`. Sin tildes en la marca, para que `svn log --search` no dependa de la codificación del terminal. `AGENTS.md` enuncia la forma **general** —`[<tarea>][arnes] ...`, que es la que sirve a cualquier agente— y no menciona `[modulo-N]`: ese segmento solo tiene sentido mientras se despliega el arnés, y es el que hace buscable el punto de restauración de cada módulo (D2.9).
   3. **La revisión se anota** en `PROGRESS.md`: en la línea «Punto de restauración» del estado verificado actual, y en la entrada de sesión que se cierra con ella. Ese número **es** el punto de restauración.

Con eso, las tres operaciones que pueden hacer falta: **ver qué cambió un módulo** con `svn diff -c <rev>`; **mirarlo sin tocar la copia de trabajo** con `svn export -r <rev>`; y **volver a él** con `svn merge -r HEAD:<rev> .` limitado a las rutas del arnés, que es una deshecha hacia delante —deja el árbol como estaba y **no borra historia**, que es lo que hay que hacer en un repositorio compartido—. `svn update -r <rev>` sirve para *mirar*, no para volver: deja la copia de trabajo clavada en una revisión antigua.

**«Una confirmación por módulo» es literal**, y conviene dejarlo medido, porque si confirmar veinte ficheros produjera veinte revisiones no habría punto de restauración que anotar. **En Subversion la confirmación es atómica**: una llamada a `svn commit` crea **una** revisión con todo lo que lleve dentro. Medido sobre un repositorio desechable, con tres ficheros y una carpeta en una sola confirmación, la salida da un único `Committed revision 1.` y los cuatro elementos devuelven `Last Changed Rev: 1`. Es la diferencia de fondo con CVS, y es lo que hace que la regla sea ejecutable y no una aspiración.

**Coste.** Frente al curso se pierden dos cosas. **El nombre**: `modulo-1` se lee de un vistazo y un número de revisión no; se compensa con la marca en el mensaje y con la anotación en `PROGRESS.md`. Y la **inmutabilidad**: nada impide que alguien confirme encima, y por eso la marca y la anotación son obligatorias, no decorativas: son lo que convierte un número cualquiera en un punto de restauración. **Alternativa aplazada, no descartada**: si hiciera falta el nombre, se pide una carpeta `tags/` hermana de `trunk/` y se etiqueta con `svn copy` **desde cada revisión anotada**. No cuesta más hacerlo después que ahora.

> **Regla reutilizable**: en Subversion sin `tags/`, el punto de restauración **no es una etiqueta: es una revisión anotada**. Lo que la convierte en punto de restauración no es la confirmación, sino que su número esté escrito en el documento que se lee y que el mensaje lleve una marca buscable. Y se vuelve con `svn merge -r HEAD:<rev>`, nunca con `svn update -r`.

## D2.6 · `feature_list.json` lleva la lista de trabajo entera, no solo el alcance entregado

**Estado**: Acordada

**Contexto.** Es la primera vez que una **puerta de salida del curso** y una **decisión propia** tiran en direcciones distintas, y por eso merece ficha: el caso se repetirá en cada repositorio de la casa, porque todos desplegarán el arnés sobre una tarea concreta y no sobre un producto entero.

**El curso.** La puerta de salida del módulo 2 lo dice tres veces: *«If a non-trivial MVP produces fewer than 10 features, treat that as a smell»* (`harness-starter/SKILL.md:67`) y *«expect roughly 12-30 session-sized features, not 5-8 broad milestones»* (`:68`), repetido como comprobación de cierre en `:94`. D2.2 fija **cuatro** *features*: cuatro suspende esa puerta, y este componente es exactamente el MVP que describe esa línea —autenticación, papeles, datos, flujos de trabajo e integraciones—. El proyecto de referencia escribe **19 *features*** en el módulo 2, todas `not_started`, con el *bootstrap* primero y sin dependencias.

**Aquí.** **La lista de trabajo entera: 20 *features***, todas `not_started` salvo una `blocked`, troceadas por dominio y por `depends_on`. F1 a F4 van **dentro** de ella, marcadas en `notes` como lo que son —F1 a F4 del alcance entregado, según la Lista de trabajo de `docs/build-brief.md`— y, las que quedan fuera, con su motivo de aplazamiento. **Qué módulo del curso cubre cada una no se escribe ahí**: se queda en D2.2, fuera del repositorio, porque el agente que lea `feature_list.json` no sabe que existe un curso (D2.9). Las dieciséis restantes son el resto de la tarea, que el descubrimiento ya nombraba: la prueba de concepto, el acceso, las lecturas de catálogo, el registro de imágenes, la operación de acabado con sus dos validaciones previas, la idempotencia, la consulta de resultado, la observabilidad y el endurecimiento. La única `blocked` es `host-carga-modulo-erp`, por la base de datos de desarrollo; las que dependen de ella **heredan el bloqueo por `depends_on`** y no se marcan una a una, porque el estado se deduce del grafo: repetirlo inventaría mantenimiento y, en cuanto la base de datos se resolviera, quedaría mintiendo en quince sitios a la vez.

**Por qué.** **Porque los dos documentos no estaban en conflicto: medían cosas distintas.** La puerta de salida habla de **la lista**; D2.2 habla de **el alcance entregado**. Una lista de cuatro entradas sería una lista de hitos —precisamente lo que la *skill* rechaza por su nombre— y además diría una falsedad: que la tarea son cuatro cosas. Escribirla completa hace **legible el aplazamiento**, que es el argumento entero de D2.2: quien mire el repositorio ve las veinte *features* y ve cuáles se entregan. Con cuatro entradas el recorte no se ve, se intuye.

**Cómo se trocearon, y la trampa que hay que evitar.** Por **dominio y `depends_on`**, nunca por módulo del curso, que es la advertencia explícita de D2.3. Dos *features* merecen explicación porque podrían parecer la misma: `validacion-nombre-fichero` se separa de `registro-imagen-con-validacion` porque la primera es comprobable **sin NAS y sin base de datos** y es la regla de seguridad del componente —hoy el canal en producción concatena a la ruta base el nombre que envía el cliente—, así que juntarlas la habría dejado bloqueada por una dependencia de infraestructura que no necesita; y `salud-del-canal` se separa del `GET /health` de `api-bootstrap` porque no es un duplicado: el de F1 demuestra que el proceso está vivo, el otro tiene tres sondas con dependencias reales. Se dice en `notes` de las dos, para que nadie lo lea como una *feature* fantasma.

**Coste.** **Veinte entradas que esta entrega no va a tocar**, y una lista larga que nadie actualiza envejece. Se asume por tres razones: el estado vive en `depends_on` y en una única `blocked`, no en veinte campos a mano; `evidence` se queda vacío hasta que algo se ejecute de verdad; y la alternativa —escribir la lista cuando toque— pierde justamente lo que la hace útil, que es poder mirar el repositorio y ver el trabajo entero.

> **Regla reutilizable**: `feature_list.json` es **la lista de trabajo del repositorio para esa tarea**, no el alcance de la entrega. El alcance se expresa en **qué entradas llegan a `accepted`**, no en qué entradas existen. Una lista recortada al alcance entregado convierte un aplazamiento razonado en un hueco invisible. Y cuando una puerta de salida del curso choque con una decisión propia, **comprobar primero que miden lo mismo**: casi nunca lo hacen.

## D2.7 · Idioma de los encabezados en los artefactos del arnés: se sigue al proyecto de referencia fichero a fichero

**Estado**: Acordada. Precisa D1.7, no la sustituye

**Contexto.** D1.7 fija «estructura en inglés, contenido en español», y su regla dice que el idioma de la estructura es el de la plantilla que la define. Al escribir los cuatro ficheros del módulo 2 esa regla da un resultado y el proyecto de referencia da el contrario, así que hay que decidir cuál manda.

**El curso.** **Las dos cosas, y traza una línea perfectamente clara.** Medido:

| Fichero del proyecto de referencia | Encabezados |
|---|---|
| `CONTEXT.md` y los documentos de `docs/` | **Inglés** (`## Glossary`, `## Problem`, `## Non-Goals`), contenido en español |
| `docs/specs/bootstrap-stack.md` | **Inglés** (`## Acceptance Scenarios`, `## Verification Plan`) |
| `AGENTS.md` | **Español** (`## Leer primero`, `## Flujo de arranque`, `## Fin de sesión`) |
| `PROGRESS.md` | **Español** (`# Registro de progreso`, `## Estado verificado actual`, `### Sesión 001`) |
| `feature_list.json` | **Inglés siempre**: claves (`user_visible_behavior`, `depends_on`) y valores de estado |

Sus plantillas de `harness-starter` traen los encabezados en inglés en los cuatro casos. Al escribir de verdad, el curso tradujo dos y no tradujo los otros dos.

**Aquí.** **Lo mismo, fichero a fichero.** `AGENTS.md` y `PROGRESS.md` con encabezados en español; `feature_list.json` con claves y valores de estado en inglés, intactos; los documentos del descubrimiento, el ADR y las futuras *specs* con encabezados en inglés.

**Por qué.** Porque la línea que trazó el curso **no es arbitraria, y se puede enunciar**: coincide exactamente con **quién lee el encabezado**. `feature_list.json` lo **parsea** una *skill*, así que traducir `depends_on` o `not_started` rompe las cuatro *skills* del ciclo: no es un encabezado, es un contrato. Los documentos del descubrimiento los lee un agente que viene con la plantilla en inglés en su propia *skill*, y además son los que el vídeo muestra junto a los del proyecto de referencia, donde la comparación tiene que ser de contenido. Y `AGENTS.md` y `PROGRESS.md` los lee **una persona**: son los dos ficheros narrativos del arnés, el mapa de entrada y el guion, y ahí el español no cuesta nada y D1.6 manda.

**Coste.** Que la regla es «fichero a fichero» y no «un idioma», así que hay que consultarla. Es barato, porque solo hay dos categorías y el criterio cabe en una frase. El riesgo real sería el contrario: un arnés íntegramente en inglés que nadie de la casa lee con gusto, o uno íntegramente en español con un `feature_list.json` que ninguna *skill* entiende.

> **Regla reutilizable**: **lo que parsea una herramienta se queda en el idioma de la plantilla; lo que lee una persona va en el idioma del repositorio.** Claves de JSON, valores de estado, nombres de fichero y vocabulario normativo no se traducen nunca; los encabezados de un documento narrativo, sí. Si hay duda, **mirar qué hizo el proyecto de referencia con ese mismo fichero**: cuando la plantilla y el ejemplo discrepan, el ejemplo es el curso aplicándose a sí mismo, y gana.

## D2.8 · La barrera de comprobaciones en Windows, y qué puede comprobar honestamente

**Estado**: Acordada en cuanto a forma y al contenido del módulo 2; el contenido del módulo 3 queda fijado y **pendiente de medir**, porque todavía no hay nada que compilar

**Contexto.** El curso usa `init.sh` en bash, con instalación, *lint*, tipos, *tests* y compilación. Aquí hay dos preguntas: la **forma** —Git Bash existe, pero PowerShell es la consola de la casa— y el **contenido**, porque **el componente no tiene pruebas propias**.

**Forma: `init.sh`, en bash.** `init.ps1` queda en MF7, para el módulo 3. Tres motivos, los tres medidos:

   1. **El intérprete no aporta nada funcional, ni ahora ni en el módulo 3.** Hoy el *script* solo hace `echo`; en el módulo 3 ejecutará `dotnet restore` y `dotnet build`, que **se escriben igual en bash y en PowerShell**.
   2. **`harness-starter` prohíbe el quinto fichero, y literalmente**: «No extra files were created» (`harness-starter/SKILL.md:97`, regla en `:20`). El módulo 2 entrega cuatro.
   3. **La política de ejecución de PowerShell bloquea los `.ps1`, y bash no tiene esa puerta.** Medido en la máquina de trabajo: `LocalMachine` queda `Undefined` —en Windows cliente el valor por omisión es `Restricted`— y `CurrentUser` está en `RemoteSigned`, que es lo que permite ejecutar y vive en el perfil del usuario. Quien actualice la copia de trabajo en una máquina donde nadie haya tocado `CurrentUser` **no puede lanzar `.\init.ps1`**: Windows lo bloquea con «running scripts is disabled on this system». El *script* «nativo de Windows» es el que necesita que alguien cambie una política de seguridad antes de funcionar.

Los dos primeros motivos **caducan en el módulo 3**; el tercero no, y es el que explica que `init.sh` siga existiendo cuando `init.ps1` exista. **Cómo queda entonces**: `init.ps1` contiene la barrera e `init.sh` se reduce a ejecutarla.

```bash
#!/usr/bin/env bash
exec powershell.exe -NoProfile -ExecutionPolicy Bypass -File "$(dirname "$0")/init.ps1" "$@"
```

Dos caminos a la misma barrera: `.\init.ps1` directo, que no necesita Git Bash, y `./init.sh`, cuyo `-ExecutionPolicy Bypass` evita el bloqueo del tercer motivo. Y **ninguna de las 24 menciones de `init.sh` repartidas por las seis *skills*** hay que tocarla. Eso no es comodidad: si una se quedara sin cambiar, un agente lanzaría `./init.sh`, no existiría, y la barrera fallaría **en silencio**. El permiso de ejecución viaja por Subversion como `svn:executable`.

**Contenido: lo que haya, y en cada fase se dice lo que no se puede comprobar.**

| Momento | Lo que la barrera hace | Lo que **no** puede hacer, y por qué |
|---|---|---|
| **Módulo 2** | Variante *pre-bootstrap*: confirma el directorio, declara que el componente no existe, enumera los comandos futuros y sale con **cero a propósito** | Nada más: no hay proyecto que compilar. Es el caso que el §4 de `harness-starter/SKILL.md` contempla literalmente |
| **Módulo 3**, con F1 | `dotnet restore` y `dotnet build` del proyecto nuevo para `net8.0-windows`, más una compilación de la solución restringida a `net472` para probar que el patrón de exclusión funciona | **Sigue sin ejecutar *tests***: el componente no tiene pruebas propias, y el único proyecto de pruebas de la solución es del módulo del ERP. Y **nada que toque base de datos**: la de desarrollo existe y responde, pero con qué cuenta la usa esta API está sin decidir, y esta máquina solo tiene LocalDB, sin el esquema de IDStone |

**La ruta se nombra, no se deduce.** Por D1.1 la barrera vive un nivel por encima de la solución, así que nombra `trunk/IDStone Office.sln` explícitamente, y lo que compila queda **escrito en el *script*** en lugar de depender del directorio desde el que se lanza. **Y lo que no puede comprobar está dentro del propio `init.sh`**, no en una nota aparte: las últimas líneas de su salida dicen por qué no se lanzan pruebas y que no hay base de datos, y remiten a `docs/technical-discovery.md`.

**Verificación ejecutada.** `./init.sh` desde Git Bash: salida completa, acentos correctos en consola y **código de salida 0**. `svn proplist -v init.sh` devuelve `svn:executable`.

**Corrección del 19/11/2026.** Esta ficha se escribió diciendo que **no había ningún proyecto de pruebas en la solución**. Dejó de ser cierto tres días antes de redactarse esta corrección: **r31949**, de jonathan, el 16/11/2026, añadió `IDStone Office.Module.Tests` para OT-890 mientras el arnés ya estaba escrito, y la copia de trabajo no se actualizó hasta que el módulo 3 tuvo que bloquear un fichero. **La conclusión de la decisión no cambia; cambia su motivo.** La barrera de F1 sigue sin ejecutar *tests*, pero ya no porque no existan: porque los que existen prueban el módulo del ERP, lo referencian entero y arrastran su restauración por el *feed* privado de la organización, que desde un terminal exige `GITHUB_ACTOR` y `GITHUB_TOKEN`. Un motivo medido vale más que el anterior, que era una ausencia. **La lección no es sobre pruebas**, y está en D3.2.

**Coste.** Frente al curso se pierde lo que de verdad da autonomía: *lint*, tipos y *tests*. Queda una barrera que **solo compila**, y un validador independiente tiene poco que reejecutar. No se disimula: se escribe el hueco y se le pone dueño. **MF4 —proyecto de pruebas del componente, no del ERP— es la mejora de prioridad alta de todo este trabajo**, y es la que convierte la barrera en una de verdad. Frente a la casa, mientras `init.ps1` no exista, quien no tenga Git Bash no puede lanzarla: es MF7, y su forma ya está decidida arriba.

> **Regla reutilizable**: la barrera comprueba **lo que hay**, lo dice en su propia salida y **enumera lo que no puede comprobar y por qué**. Una barrera que solo compila es honesta; una que aparenta validar pierde la garantía que el método entero sostiene. En un repositorio sin pruebas, lo primero no es escribir *tests* del producto entero: es declarar el hueco con dueño y prioridad, y poner las pruebas **del componente nuevo**, que son las únicas que se pueden escribir sin base de datos. Y el nombre del *script* no se cambia por gusto de consola: está escrito dentro de las plantillas del arnés y en la puerta de salida.

## D2.9 · `PROGRESS.md` se escribe para el agente siguiente, no para el vídeo

**Estado**: Acordada. Fija la forma de `PROGRESS.md`, y sustituye a D2.4 en ese punto

**Contexto.** `PROGRESS.md` es un fichero del arnés que vive **dentro** del repositorio y que irá actualizando cada agente que aborde una tarea nueva. Ese agente no sabe que existe un curso. Una entrada titulada «Módulo 2 — arnés mínimo», una línea `Módulo:` y referencias como `D2.5`, `MF7` o `Q8` le piden un contexto que no tiene y que no puede resolver: los documentos que definen esas etiquetas están fuera del repositorio y no llegan en una copia de trabajo.

**El curso.** La plantilla fija dos secciones y ocho campos por entrada —Fecha · Objetivo · Completado · Verificación ejecutada · Evidencia capturada · Archivos o artefactos actualizados · Riesgo o cuestión no resuelta · Siguiente mejor paso— (`harness-starter/references/artifact-templates.md:112-140`). El proyecto de referencia titula sus sesiones **por *feature*** (`### Sesión 002 — bootstrap-stack`), nunca por módulo, y su `PROGRESS.md` no contiene **ni una** referencia al curso: ni a módulos, ni a puertas de salida, ni a su material. Medido además: su fichero en la etiqueta `modulo-2` tiene **una sola entrada**, la de ese módulo, y el descubrimiento del módulo 1 no aparece. Para el curso ese fichero solo sirve para seguir trabajando.

**Aquí.** La plantilla tal cual, **sin línea `Módulo:` y sin ninguna etiqueta que no se resuelva dentro del repositorio**. Una sesión es una sesión de trabajo: la 001 es el descubrimiento y la 002 el arnés —eso es lo que pasó de verdad aquí, y la 001 se recupera porque su trabajo está en el repositorio—, y de la 003 en adelante se titulan por la *feature*, como la referencia. Tampoco se citan recuentos de líneas de otros ficheros: envejecen en cuanto alguien los edita.

La traza por módulos —qué módulo cubre cada parte del trabajo, qué puerta de salida obligó a qué— vive en **este** documento y en el guion del vídeo, que es donde el lector sí sabe qué es un módulo.

**Por qué.** **Dos audiencias no caben en un fichero.** El agente siguiente y el espectador del vídeo no necesitan lo mismo, y este fichero vive en el repositorio: sirve al primero. Tratarlo además como guion de la narración le mete un vocabulario —módulos, puertas de salida, etiquetas de decisión— que solo se entiende con documentos que no están ahí, y lo que gana el espectador lo paga quien lo va a leer de verdad. El reparto por preguntas de D2.4 no cambia: lo que cambia es que el avance se escribe en el idioma del repositorio.

**Coste.** La traza por módulos hay que escribirla al cerrar cada uno en este documento, porque ya no se puede leer de `PROGRESS.md`. Y el vídeo pierde un guion literal: hay que narrar desde los dos entregables.

> **Regla reutilizable**: un artefacto que vive dentro del repositorio se escribe **solo** para quien lo va a leer dentro del repositorio. Si una sección, una etiqueta o una cifra necesita un documento externo para entenderse, no va ahí. El material de narración se escribe aparte y se alimenta del artefacto, nunca al revés.

---

# Módulo 3

## D3.1 · Una *feature* se confirma entera: su código y su arnés, en una sola revisión

**Estado**: Acordada. **Precisa D2.5 en su regla 1** y reescribe la viñeta de confirmación de `AGENTS.md`

**Contexto.** D2.5 fijó que el punto de restauración es una revisión anotada, y `AGENTS.md` lo enunció con una lista de siete rutas —`.agents`, `AGENTS.md`, `CONTEXT.md`, `docs`, `feature_list.json`, `init.sh`, `PROGRESS.md`— y la condición de no mezclar nunca código de producto. Las dos cosas se escribieron cuando el arnés solo producía documentos: los módulos 1 y 2 no tocaron un solo fichero bajo `trunk/`, así que la regla nunca se puso a prueba. La *spec* de `api-bootstrap` es la primera que sí, y la rompe por dos sitios a la vez. Sus *Expected File Changes* son **doce ficheros en dos árboles**: siete bajo `trunk/` —seis del proyecto nuevo `IDStone Office.WebApi` y la solución `IDStone Office.sln`, que hay que modificar— y cinco en la raíz —`init.sh`, `PROGRESS.md`, `feature_list.json`, más `ARCHITECTURE.md` y `CONSTRAINTS.md`, que se crean—. Los dos últimos **no estaban en la lista de siete**: tal como estaba escrita la regla, no se podían confirmar en ningún sitio.

**El curso.** No distingue los dos árboles, y no por descuido: **confirma la *feature* entera en una sola confirmación**. Medido en el proyecto de referencia, `git show --stat a29a2df` («feat: complete cart-add») devuelve un único *commit* con `ARCHITECTURE.md`, `CONSTRAINTS.md`, `PROGRESS.md`, `docs/specs/cart-add.md`, `docs/technical-discovery.md`, `docs/risks-and-open-questions.md` y `feature_list.json` **junto a once ficheros de `src/`**. Y aparecen ahí los mismos dos ficheros que a nosotros nos desbordan la lista, por el mismo motivo: la primera *feature* que establece una superficie nueva los crea.

**Aquí.** Lo mismo, con una sola precisión que el curso no necesita porque su repositorio es solo del producto: **lo que define la confirmación es la unidad de trabajo, no el árbol donde caen los ficheros.** La viñeta de `AGENTS.md` queda así: la confirmación lleva **exactamente los ficheros de esa unidad y ninguno más** —los que su *spec* declara en *Expected File Changes*, o los que nombre la entrada del registro cuando no hay *spec*—; una *feature* confirma su propio código de producto junto a los ficheros del arnés que actualiza, para que la unidad sea **una sola revisión**; y lo ajeno a la unidad **se mira cada vez**, porque `svn status` devuelve artefactos de compilación versionados bajo `trunk/` que son de otros. Si aparece algo que no está en la lista de la unidad, no se confirma y se dice.

**La regla 1 de D2.5 queda precisada así**: «solo con las rutas del arnés, nunca mezclada con código de producto» valía mientras la unidad de trabajo era un módulo que solo escribía documentos. Desde `api-bootstrap` la unidad es **una *feature* aceptada**, y una *feature* incluye su código. Lo que sobrevive íntegro de D2.5 es lo importante: el punto de restauración sigue siendo **una revisión anotada**, y por eso mismo la unidad no puede partirse en dos.

**Por qué.** La lista de siete rutas tenía un propósito legítimo y comprobable: mantener fuera el trabajo ajeno. Hay artefactos de compilación **versionados** bajo `trunk/`, como `trunk\IDStone Office.Web\obj\Debug\DesignTimeResolveAssemblyReferencesInput.cache`, que aparecen modificados en `svn status` según quién haya compilado —el 19/11/2026 lo estaba, y tras actualizar a r32034 ya no—, y la regla existe para que nunca entren. Eso se conserva entero, y mejor que antes: una lista cerrada de rutas no habría impedido que entrara un fichero de `docs/` que no fuera de la *feature*, y la nueva redacción sí. Lo que sobraba era confundir «trabajo ajeno» con «código de producto»: el código de la *feature* no es ajeno a la *feature*.

**Coste.** Una confirmación del arnés deja de ser inspeccionable de un vistazo por su ruta: ahora hay que compararla con la lista de la *spec*. A cambio se gana que **una *feature* sea una revisión**, que es la única forma de que el número anotado en `PROGRESS.md` restaure algo coherente. Con dos revisiones por *feature*, deshacer la del arnés dejaría el proyecto nuevo dentro de `trunk/` con `feature_list.json` diciendo `not_started`, y deshacer la del producto dejaría `feature_list.json` diciendo `accepted` y `init.sh` compilando un proyecto que ya no existe. Ninguno de los dos estados es un punto de restauración. **Y el prefijo del mensaje se queda en `[OT-867][arnes]`** aunque la confirmación lleve código de producto: el ámbito que marca es de dónde viene el trabajo, no qué árbol toca.

> **Regla reutilizable**: una confirmación se define por **la unidad de trabajo que cierra**, y su lista de ficheros la escribe la especificación de esa unidad, no una lista de rutas en el fichero de instrucciones. Una lista de rutas envejece a la primera unidad que crea un fichero nuevo. Y si el repositorio mezcla gobierno y producto, la regla que hay que escribir no es «no mezclar árboles» sino «nada que no sea de esta unidad» —que es más estricta y, además, no caduca.

## D3.2 · Un hecho medido lleva su revisión, y se recomprueba al abrir el módulo

**Estado**: Acordada

**Contexto.** Entre el 13/11 y el 19/11/2026 la copia de trabajo pasó de **r31850** a **r32034**: ciento ochenta y cuatro revisiones de los compañeros, en un repositorio que no es nuestro en exclusiva. Una de ellas, **r31949**, añadió un proyecto de pruebas a la solución. El arnés y los dos entregables afirmaban en **veintitrés sitios** que no existía ninguno. Nadie se enteró: la copia de trabajo no se actualizó hasta que el módulo 3 tuvo que bloquear un fichero, y el descubrimiento fue un efecto colateral de ese bloqueo. No había ningún mecanismo que lo detectara, y sin ese tropiezo la afirmación falsa habría llegado al vídeo.

**El curso.** No se le plantea el problema, y no es un descuido suyo. Su proyecto es un repositorio de una sola persona creado de cero: nadie modifica el producto por otro lado mientras se monta el arnés, así que un hecho medido en el módulo 1 sigue siendo cierto en el 6. Es la primera consecuencia de montar esto sobre un **repositorio compartido y en producción** que el material no puede anticipar, y por eso vale para las demás soluciones de la casa, que están todas en la misma situación.

**Aquí.** Dos reglas, y ninguna cuesta nada:

   1. **Todo hecho medido se escribe con la revisión a la que se midió.** `PROGRESS.md` ya lo hacía sin darle nombre —su primera línea declara la revisión de la copia de trabajo—, y `docs/technical-discovery.md` también. Ahora es obligatorio y explícito: una tabla de entorno sin revisión no está terminada.
   2. **La primera acción de cada sesión es comprobar si esa revisión sigue siendo la de la copia de trabajo.** Va en el flujo de arranque de `AGENTS.md`, justo después de confirmar el directorio. Si no coincide, lo primero no es trabajar: es **volver a medir** los hechos del *Estado verificado actual* y corregir lo que haya caducado.

**Por qué.** Porque la diferencia de fondo entre este despliegue y el del curso no es Subversion, ni el tamaño del producto: es que **aquí hay otros escribiendo**. Un arnés que registra hechos y no registra cuándo dejaron de ser ciertos acumula mentiras a la velocidad a la que trabaja el resto del equipo. Y el daño no es el fichero desactualizado —ese se arregla en una tarde— sino que **un agente decide sobre él**: la *spec* de `api-bootstrap` razona sobre la ausencia de pruebas, y lo que de verdad hubo que mirar es si esa ausencia seguía siendo cierta.

**Coste.** Un comando al abrir cada sesión, y la disciplina de escribir un número junto a cada tabla de entorno. A cambio, el arnés deja de afirmar cosas que ya no puede sostener. **Lo que esto no arregla** es el trabajo de volver a medir cuando la revisión ha cambiado: eso sigue siendo manual, y con ciento ochenta y cuatro revisiones de diferencia no es una comprobación de un minuto. La automatización —un `init.sh` que compare y avise— está anotada aparte.

> **Regla reutilizable**: en un repositorio compartido, **un hecho sin revisión no es un hecho: es un recuerdo**. Todo lo que un arnés mide sobre el entorno se fecha con la revisión en que se midió, y la primera acción de cada sesión es comprobar si esa revisión sigue vigente. Si el arnés solo se entera de que el mundo cambió cuando algo se rompe, lo que tiene no es contexto: es contexto caducado con aspecto de vigente.

---

# Módulo 4

## D4.1 · Sin *pull requests* ni CI remota

**Estado**: Diferida, y fuera del alcance entregado

**Contexto.** El módulo 4 se apoya en `gh issue`, `gh pr` y GitHub Actions, que no existen sobre Subversion.

**Aquí.** Para el proyecto entregado **se asume que no habrá peticiones de integración ni CI remota**, y el asunto pasa a `mejoras-trabajo-futuro.md` (MF1). **Lo que sí se conserva** del módulo 4 es el mecanismo que de verdad importa en el módulo 6: la **instantánea antes y después de cada papel**, para comprobar qué ha tocado cada uno. Eso se traduce a Subversion con `svn status` y `svn diff` sin perder nada, porque no necesita ramas.

> **Regla reutilizable**: de un módulo que depende de una plataforma ausente no se descarta el módulo, se descarta la plataforma. Lo que hay que identificar es **qué mecanismo enseña** y si ese mecanismo sobrevive sin ella.

## D4.2 · Cómo se ejercita la API sin interfaz: MCP de terceros, configurado, no construido

**Estado**: Propuesta

**Contexto.** D1.3 deja la API sin `DESIGN.md`, pero sigue haciendo falta **poder demostrar que funciona**, y el §10 del módulo 4 introduce MCP justamente para que el validador tenga con qué probar lo que construyó el implementador.

**El curso.** Conecta **Chrome DevTools MCP**, un servidor MCP **de terceros que solo se configura**, y le añade una regla al arnés. No construye ningún servidor MCP.

**Aquí.** Lo mismo, con la pieza equivalente para una API: un **puente OpenAPI → MCP genérico, de terceros, configurado apuntándolo al documento OpenAPI** que el componente ya emite. Cero proyectos nuevos, cero código.

**Por qué.** Porque es lo que hace el curso; porque la alternativa que se valoró antes —escribir un proyecto aparte con el SDK oficial de C#— **es un proyecto en sí mismo** y no cabe en el alcance; y porque el documento OpenAPI **sale gratis**, ya previsto en la propuesta de arquitectura, así que el puente se alimenta de un artefacto que iba a existir de todos modos.

**La capa visual, además.** El generador de OpenAPI sirve también su **interfaz de exploración**: una página con todos los *endpoints*, su contrato y un botón que lanza la petición real y muestra la respuesta. Para demostrar la API —y para grabarla— es una interfaz de verdad, estándar en la industria, y no cuesta nada. Con eso la demostración tiene las dos mitades que se necesitan mutuamente: **la API detrás** y **algo delante que la llame**, sin construir lo segundo.

**Coste.** El puente genérico expone *todos* los *endpoints* del documento como herramientas, sin el criterio que tendría un servidor escrito a mano. Para probar y demostrar sobra; para uso real por terceros, no se propone.

> **Regla reutilizable**: para ejercitar una API, **la interfaz ya existe**: el documento OpenAPI más su interfaz de exploración para las personas, y un puente OpenAPI → MCP genérico para los agentes. Escribir un cliente propio es trabajo que el contrato ya hace.
