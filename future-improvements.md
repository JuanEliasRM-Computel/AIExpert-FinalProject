# Mejoras y trabajo futuro

**Proyecto**: despliegue del arnés del curso AI Expert (DevExpert Academy) sobre IDStone Office. **Tarea de referencia**: OT-867 «Web API IDStone (integración escáner tablas)». **Documento hermano**: `decisiones-divergencias-arnes.md`, que recoge las divergencias con el curso.

## 0. Para qué sirve este documento

Para dejar por escrito **lo que se deja fuera a propósito**, de modo que un alcance recortado se lea como una decisión y no como un olvido. Tiene los mismos dos lectores que el documento de decisiones: la evaluación del curso y los demás repositorios de la casa.

Regla de entrada: aquí no se apunta lo que *sería bonito*, sino lo que **se ha identificado como necesario o valioso y se ha dejado fuera del alcance entregado**, con lo que costaría traerlo.

## 1. Cómo se lee

   * **Nomenclatura**: `MF-n` = **Mejora Futura** número *n*. Numeración continua, sin renumerar. En `decisiones-divergencias-arnes.md`, `D<módulo>.<ordinal>` = **Decisión**, y `DM.n` las de método. El prefijo `MF` lleva las dos letras porque una sola colisionaba con *Módulo*: al leer «M3» era razonable entender «módulo 3».
   * **Ficha fija**: Origen · Prioridad · Qué es · Por qué queda fuera · Qué haría falta · Valor.
   * **Prioridad**: *Alta* si hay un riesgo real en no hacerlo, *Media* si es una mejora clara, *Baja* si es una conveniencia.
   * Cuando una mejora se implementa, se marca **Hecha en**, con el módulo que la hizo.

### Índice

| | Mejora | Prioridad |
|---|---|---|
| **MF1** | *Pull requests* y CI remota | Media |
| **MF2** | Un servidor MCP propio para la API | Baja |
| **MF3** | Consumir un modelo desde dentro del producto | Media |
| **MF4** | Proyecto de pruebas del componente | **Alta** |
| **MF5** | Plataforma: DevExpress y .NET | **Alta**, y ajena al arnés |
| **MF6** | Endurecer el canal actual, al margen de la API | **Alta** |
| **MF7** | `init.ps1` como barrera, con `init.sh` reducido a ejecutarla | Media |
| **MF8** | Retirar los relevos externos en favor de `PROGRESS.md` | **Hecha en el módulo 2** |
| **MF9** | El *host* de orquestación | Media |
| **MF10** | Consolidar los dos árboles de OpenSpec | Media |
| **MF11** | Un `CONTEXT.md` de producto por encima del glosario del componente | Media, Alta con la segunda tarea |
| **MF12** | Automatizar la referencia entre `docs/specs/` y OpenSpec | Baja, Media en cuanto una *feature* toque una capacidad |

---

# MF1 · *Pull requests* y CI remota

**Origen**: D4.1 · **Prioridad**: Media

**Qué es.** El módulo 4 del curso termina en una *pull request* por *feature*, con la evidencia en la descripción, y repite la barrera de comprobaciones en remoto. La revisión humana es la *pull request*, y nadie integra sin que la barrera esté en verde.

**Por qué queda fuera.** El repositorio es Subversion: `gh issue`, `gh pr` y las acciones remotas no existen ahí, y el equipo no ramifica para trabajar.

**Qué haría falta.** Tres caminos, de menor a mayor compromiso: una **revisión sin *pull request***, registrada como artefacto en el repositorio igual que hace el curso, más la confirmación en Subversion, que es lo que se entrega; **`git svn`**, ya instalado, que daría ramas y copias de trabajo paralelas sobre el mismo repositorio con sincronización al final, y permitiría el paralelismo del módulo 4 sin cambiar el servidor; o un **espejo en una plataforma con integración continua** solo para el flujo de revisión, que da el módulo 4 completo y es el que más decisiones de organización implica.

**Valor.** La barrera remota es lo único que comprueba que **el conjunto** sigue funcionando tras integrar varios cambios; en local cada rama se comprueba sola. El curso lo ilustra con el caso de dos peticiones en verde que chocan al integrarse.

---

# MF2 · Un servidor MCP propio para la API

**Origen**: D4.2 · **Prioridad**: Baja

**Qué es.** Un servidor MCP escrito a mano que exponga solo las operaciones que interesan, con nombres, descripciones y validaciones pensadas para que un agente las use bien. El SDK oficial de C# existe para eso.

**Por qué queda fuera.** Es un proyecto en sí mismo. Para probar y demostrar basta el puente OpenAPI → MCP genérico de D4.2, que solo se configura.

**Qué haría falta.** Un proyecto aparte, en `net8.0` **liso** —sin DevExpress ni XAF, para que no arrastre las restricciones de plataforma del ERP—, que hable HTTP con la Web API. Se puede construir contra el contrato antes de que la API exista.

**Valor.** Un puente genérico expone *todos* los *endpoints* sin criterio; uno propio expone las operaciones de negocio con el vocabulario del dominio. Interesa si algún día un agente va a operar contra la API de forma habitual.

---

# MF3 · Consumir un modelo desde dentro del producto

**Origen**: D2.2, D4.2 y el módulo 5 del curso · **Prioridad**: Media

> **Esta mejora ha pasado a la lista de trabajo**, partida en dos *features* que comparten contrato: **F2**, la normalización determinista a un conjunto cerrado de códigos, y **F3**, el mismo contrato resuelto con un modelo. F2 es realista; F3 es ambicioso. Lo que sigue describe la versión con modelo, que es la que cubre el módulo 5.

**Qué es.** El módulo 5 trata de **llamar** a un modelo desde la aplicación: salida estructurada, *function calling*, RAG. MCP es la dirección contraria —exponer la aplicación a un modelo—, así que no lo cubre.

**La candidata más pequeña y honesta ya es un requisito del proyecto.** La propuesta de arquitectura pide que los mensajes internos de error se **normalicen a códigos públicos**, sin textos ni rutas internas. Hoy ese detalle vive solo como texto libre dentro de cada línea de transacción, escrito por el ERP. Clasificar ese texto en un conjunto cerrado de códigos es exactamente una tarea de clasificación.

**Por qué puede quedar fuera.** Porque es alcance por encima de la tarea y afecta al contrato que ya se ha enviado al cliente: necesita un acuerdo que no es solo técnico. Y porque antes hay que entregar F1 y F2. Si F3 no entra, el módulo 5 queda **especificado y aplazado**, no omitido, que es la distinción que sostiene D2.2.

**Qué haría falta.** El conjunto cerrado de códigos públicos, un muestreo real de los mensajes internos para evaluar la clasificación, y la decisión de si la llamada al modelo se hace en línea o en diferido. Más una salvaguarda: un código `desconocido` al que caer, porque un clasificador no debe inventar.

**Valor.** Es el único punto del proyecto donde la IA entra en el producto y no en el proceso de desarrollo. Y resuelve un requisito que ya está escrito y que hoy no tiene solución.

---

# MF4 · Proyecto de pruebas del componente

**Origen**: D2.8 · **Prioridad**: **Alta**

**Qué es.** El componente no tiene pruebas propias. Desde **r31949** (16/11/2026, OT-890) la solución sí tiene `IDStone Office.Module.Tests` —xunit 2.9.3, `net8.0-windows;net472`—, pero prueba el **módulo del ERP**: lo referencia entero, arrastra su restauración por el *feed* privado y sus pruebas contra SQL Server se saltan solas donde no hay LocalDB —en esta máquina lo hay, así que se ejecutarían—. No cubre nada de la API.

> **Corregido el 19/11/2026.** Esta mejora decía «no existe ningún proyecto de pruebas en la solución». Dejó de ser cierto el 16/11, mientras el arnés ya estaba escrito. **La recomendación no cambia**, porque desde el principio decía «del componente nuevo, no del ERP entero»: lo que cambia es la premisa, y lo que aparece es un **precedente de forma** —xunit, los dos marcos, el atributo que salta sin LocalDB— que ahora conviene copiar en lugar de inventar.

**Por qué queda fuera.** Crear una red de pruebas para un ERP de unas 328.000 líneas no es una tarea de este proyecto.

**Qué haría falta.** Empezar por donde la barrera de comprobaciones lo note: un proyecto de pruebas **del componente nuevo**, no del ERP entero. Validaciones de contrato, idempotencia y las reglas que la API añade y que hoy no existen. Son además las únicas pruebas que se pueden escribir sin base de datos. **Y ya no hay que decidir la forma**: se copia la de `IDStone Office.Module.Tests` —xunit, `Microsoft.NET.Test.Sdk`, `IsTestProject`, y el patrón `FactConLocalDbAttribute` para que lo que necesite base de datos se salte solo en lugar de fallar—, que es además la que la casa ya usa en `IDS.Module.Tests`.

**Valor.** Es la carencia que más limita todo lo demás. Mientras la barrera solo compile, el validador no tiene casi nada que reejecutar, y el curso es tajante: **sin validación no hay autonomía, y sin autonomía el paralelismo solo multiplica el ruido**. Todo el valor del ciclo del módulo 4 depende de esto.

---

# MF5 · Plataforma: DevExpress y .NET

**Origen**: propuesta de arquitectura · **Prioridad**: **Alta**, y ajena al arnés

**Qué es.** El repositorio está en DevExpress 23.2.5, una rama que ya no recibe parches de seguridad, sobre .NET 8, cuyo soporte ha terminado.

**Por qué queda fuera.** Es una decisión de producto para toda la familia, no de esta tarea.

**Qué haría falta.** La tarea de plataforma que la propuesta ya recomienda abrir, con las tres opciones valoradas allí: quedarse en la versión actual como piloto interno, subir un escalón, o subir al último con .NET 10.

**Valor.** Condiciona si la API puede abrirse a terceros fuera de la red interna. Mientras no se resuelva, la propuesta exige controles compensatorios: proxy inverso, aislamiento de red y lista de direcciones permitidas.

---

# MF6 · Endurecer el canal actual, al margen de la API

**Origen**: propuesta de arquitectura · **Prioridad**: **Alta**

**Qué es.** En el servicio del canal de captura, los *endpoints* de escritura no tienen la comprobación de autenticación activa en el código, y el nombre de fichero que envía el cliente se concatena a la ruta antes de escribir. Además, los terceros leen las rutas base de las imágenes mediante una vista SQL con `GRANT SELECT`.

**Por qué queda fuera.** No es la API nueva: es el servicio que ya está en producción.

**Qué haría falta.** Reactivar la autenticación, sanear el nombre de fichero, restringir el acceso por red y, cuando el tercero migre a la API, retirar el permiso de la vista.

**Valor.** Son correcciones de severidad alta e **independientes** de este proyecto. Si el servicio es alcanzable desde fuera de la red interna, son urgentes y no deberían esperar a la API.

---

# MF7 · `init.ps1` como barrera, con `init.sh` reducido a ejecutarla

**Origen**: D2.8 · **Prioridad**: Media · **Cuándo**: módulo 3, con `api-bootstrap`

**Qué es.** El curso usa `init.sh` en bash; aquí la consola de la casa es PowerShell y el resto de los *scripts* del repositorio son `.ps1` o `.bat`. La mejora **no es sustituir** `init.sh`: es invertir los dos ficheros. `init.ps1` contiene la barrera —`dotnet restore`, `dotnet build`— e `init.sh` se reduce a ejecutarla:

```bash
#!/usr/bin/env bash
exec powershell.exe -NoProfile -ExecutionPolicy Bypass -File "$(dirname "$0")/init.ps1" "$@"
```

Dos caminos a la misma barrera: `.\init.ps1` directo, que no necesita Git Bash, y `./init.sh`, cuyo `-ExecutionPolicy Bypass` evita que Windows bloquee el `.ps1`.

**Por qué queda fuera.** Por los tres motivos de D2.8, y los dos primeros caducan en el módulo 3: hoy el *script* solo hace `echo`, así que el intérprete no aporta nada; `dotnet restore` y `dotnet build` se escriben igual en los dos; y `harness-starter` prohíbe crear un quinto fichero. El tercero —la política de ejecución de PowerShell, `Restricted` por omisión en Windows cliente— no caduca, y es la razón de que `init.sh` siga existiendo después.

**Qué haría falta.** Escribir `init.ps1` con la barrera real, reducir `init.sh` al envoltorio de arriba, y **no tocar ninguna de las 24 menciones de `init.sh` que hay en las seis *skills***, repartidas en nueve ficheros. Eso último es la razón de hacerlo así y no renombrando: si una mención se quedara sin cambiar, un agente lanzaría `./init.sh`, no existiría, y la barrera fallaría **en silencio**.

**Valor.** Dos cosas, y la segunda es la que subió la prioridad de *Baja* a *Media*. La primera es de **adopción**: el arnés tiene que poder usarlo quien no haya hecho el curso, desde la consola de la casa y sin instalar nada. La segunda es que **`init.ps1` es el sitio natural de las órdenes `mklink` de D1.8**: hoy viven en `AGENTS.md` como instrucciones para una persona, y son el motivo de que ese fichero salga con 101 líneas en lugar de las 30-50 que el curso recomienda al arrancar. Un `init.ps1` que cree el enlace si falta, además de comprobar la barrera, descarga ese bloque y resuelve el arranque de una copia de trabajo nueva **sin que nadie lea nada**.

---

# MF8 · Retirar los relevos externos en favor de `PROGRESS.md`

**Origen**: DM.1 · **Prioridad**: Media, con fecha · **Hecha en: módulo 2**

**Qué es.** Los ficheros de relevo de la carpeta de la tarea son andamio: existen porque el módulo 1 no tiene permiso para crear `PROGRESS.md`.

**Por qué quedaba fuera.** Hacía falta un relevo entre la sesión de preparación y la del módulo 1, y `PROGRESS.md` todavía no podía existir.

**Qué hacía falta.** En el módulo 2, al generar `PROGRESS.md`, trasladar el estado y **dejar de escribir relevos externos**, con una nota de una línea que diga que la serie está cerrada y dónde continúa.

**Valor.** Evita dos fuentes de verdad sobre el estado del proyecto. Es el error que este documento existe para no cometer.

**Hecha.** `PROGRESS.md` existe en el repositorio con la sesión 001 recuperada del módulo 1 y la sesión 002 de este módulo; `progreso.md` queda cerrado con una línea que dice dónde continúa; y el relevo del módulo 2 es **el último** de la serie. A partir de aquí, quien quiera saber el estado abre el repositorio.

---

# MF9 · El *host* de orquestación

**Origen**: D2.2 (*feature* F4) y el módulo 6 del curso · **Prioridad**: Media

**Qué es.** El módulo 6 separa tres capas: el **arnés**, que no cambia; el ***host***, que contiene la tabla de flujo, la tabla de reglas y el bucle, y es determinista; y el **motor**, que es intercambiable. El *host* comprueba las reglas con **instantáneas del repositorio antes y después de cada papel** —lo que ha cambiado es lo que se ha tocado, diga lo que diga el papel— y es el *host*, nunca un papel, quien escribe `accepted`.

**Por qué queda fuera.** Por plazo, y solo por plazo. El *script* de verificación del proyecto de referencia tiene 542 líneas y aparece en la última etiqueta, cuando las once *features* anteriores ya estaban aceptadas. Montarlo sin haber conducido antes el flujo a mano sería construir el automatismo antes de saber qué automatiza.

**Qué haría falta.** Una versión mínima y honesta, que no imita las 542 líneas sino la regla: una tabla de flujo —*spec* → implementar → validar—, una tabla de reglas que diga qué ficheros puede tocar cada papel, `svn status` y `svn diff` antes y después de cada uno para comprobarlo, y el *host* como único autor de `accepted`. En Windows, con PowerShell (véase MF7).

**Requisito previo.** Que el flujo encadenado del módulo 4 haya corrido al menos una vez a mano, con F2. Sin eso no hay nada que orquestar.

**Valor.** Es el escalón que convierte el arnés en algo que corre solo, y el único punto donde `accepted` deja de depender de la disciplina de quien ejecuta. Es también el orden que el curso insiste en respetar: **validación → autonomía → paralelismo**.

---

# MF10 · Consolidar los dos árboles de OpenSpec

**Origen**: descubrimiento del módulo 1 y D1.1 · **Prioridad**: Media

**Qué es.** El repositorio tiene **dos** directorios `openspec/`, no uno:

| Ubicación | Contenido |
|---|---|
| `openspec/`, en la raíz de la copia de trabajo | `config.yaml`, tres cambios activos, cuatro *specs* y su archivo. Es más reciente |
| `trunk/openspec/` | Sin `config.yaml`. Una sola *spec*, `costes-produccion-pda`, y `changes/` vacío |

El de la raíz es claramente el vivo: tiene la configuración, es más reciente y concentra el trabajo. El de `trunk/` parece un resto de cuando se decidió la ubicación.

**Por qué queda fuera.** No bloquea nada del módulo 1 ni de la primera *feature*, y tocar la estructura de gobierno de un repositorio ajeno a esta tarea no es decisión del agente. Queda anotada como cuestión abierta, con dueño, en `docs/risks-and-open-questions.md`.

**Qué haría falta.** Decidir el destino de `costes-produccion-pda`, moverla a `openspec/specs/` con `svn move` para no perder el historial, y retirar `trunk/openspec/`. Media hora, más el acuerdo.

**Valor.** Tres cosas, y la tercera es la que importa para los dos lectores del §0.

   1. Elimina la duda de dónde se escribe una *spec* nueva, que es justo lo que el módulo 2 tiene que decidir al reconciliar OpenSpec con el mecanismo del curso (D2.1).
   2. `costes-produccion-pda` **no es una *spec* cualquiera para este trabajo**: fija las reglas de coste —prioridad de búsqueda de tarifa, filtro por máquina, independencia entre filas— que la validación previa de coste de la API tiene que respetar. Que esté en el árbol menos visible es un riesgo de que alguien la reimplemente sin verla.
   3. **Es el contraejemplo que valida D1.1.** La duplicidad es solo de este repositorio: los demás tienen un único `openspec/`, en la raíz. El precedente de la casa es unánime *entre* repositorios y está roto *dentro* de uno, y el estropicio es exactamente el que D1.1 existe para no volver a crear con el arnés. La lección transferible es que antes de colocar el arnés **se comprueba si el repositorio ya tiene gobierno duplicado**, porque heredarlo sin verlo multiplica el problema por dos.

---

# MF11 · Un `CONTEXT.md` de producto por encima del glosario del componente

**Origen**: DM.3 y D1.2 · **Prioridad**: *Media*, **Alta en cuanto una segunda tarea añada su propio descubrimiento al arnés que ya existe**

**Qué es.** Un `CONTEXT.md` en la raíz que fije el vocabulario **estable de IDStone Office** —las veinte o treinta palabras que no cambian: almacén, stock, bloque, material, formato, operación, tarifa, dispositivo, transacción— y que delegue en los glosarios de componente el vocabulario específico de cada integración.

**Por qué queda fuera.** El `CONTEXT.md` que existe lo escribió `build-brief` en el módulo 1, y su alcance es el que la *skill* prescribe —*«shared vocabulary for the project»*—, donde el *project* es el componente de integración. Ampliarlo a todo el ERP en el módulo 1 habría sido modificar el resultado de la *skill* por la puerta de atrás, justo en el módulo cuya decisión (D1.2) es ejecutarla sin tocarla. Y un glosario de unas 328.000 líneas de producto escrito de una sentada no lo lee nadie y envejece en una semana.

**Qué haría falta.**

   1. Decidir la **forma**: un `CONTEXT.md` de producto en la raíz y los de componente bajo `docs/<componente>/CONTEXT.md`, o un único fichero con una sección por componente. La primera escala mejor.
   2. **No escribirlo de golpe.** Se arranca con lo que ya está medido —los términos que el descubrimiento tuvo que aclarar y que **no** son de la integración: stock, almacén, formato, material, tarifa, máquina, operación— y crece cuando una tarea nueva tropiece con una palabra ambigua.
   3. Una **regla de entrada** escrita: un término sube al glosario de producto cuando **lo usan dos componentes con el mismo significado**. Hasta entonces se queda abajo. Sin esa regla, el fichero vuelve a ser el documento colosal que esta mejora existe para no escribir.
   4. Un **dueño**. Sin dueño nadie lo poda, y un glosario sin podar miente.

**El gemelo que el curso ya trae previsto.** Lo que esta mejora propone para el **vocabulario**, el curso lo tiene contemplado para el **informe**: `harness-starter` declara su segunda entrada obligatoria como *«`docs/build-brief.md` **or** `docs/product-brief.md`»* (`:30`), y la plantilla de `product-brief.md` **no tiene `## MVP Slice` ni `## Validation Plan`**: describe el producto, no una entrega. Así que esta mejora no se hace sola: se crea el `CONTEXT.md` de producto **y** `docs/product-brief.md`, y `docs/build-brief.md` se queda con la entrega en curso. El reparto completo está en **DM.4**.

**Valor.** Evita el escenario que hace inútiles los glosarios: dos documentos que definen «operación» de forma distinta y ningún árbitro. Y completa por arriba el arnés **del repositorio**: sus artefactos ya lo son desde D1.1 —un solo `AGENTS.md`, un solo `init.sh`, un solo `PROGRESS.md`, un solo `feature_list.json`, un solo árbol de *skills*, todos sobre `trunk/`—, y lo único que hoy sigue siendo de una tarea es el **vocabulario**. Con un solo componente descubierto no hay conflicto que arbitrar, y adelantarse sería exactamente la ceremonia que la *skill* manda evitar.

---

# MF12 · Automatizar la referencia entre `docs/specs/` y OpenSpec

**Origen**: D2.1 · **Prioridad**: *Baja* hoy, **Media en cuanto una *feature* toque una capacidad del ERP**, es decir desde `validacion-previa-coste`

**Qué es.** D2.1 decide que los dos mecanismos de especificación conviven: `docs/specs/<id>.md` es el contrato de implementación de **una *feature* de una sesión**, y `openspec/` de la raíz es la verdad **del sistema**. La regla que los relaciona está escrita, pero se aplica **a mano**: cuando una *feature* añade o cambia una capacidad, alguien tiene que abrir el cambio de OpenSpec y nombrarlo desde la *spec* de la *feature*.

**Por qué queda fuera.** Porque en el alcance entregado **no se recorre ni una vez**: F1 y F2 no cambian ninguna capacidad de IDStone, crean un componente nuevo y su normalización interna de errores. Automatizar un camino que todavía no ha tenido un solo caso real sería diseñar sobre una suposición, y el primer caso real es el que enseña qué hay que automatizar.

**Qué haría falta.** Por orden de coste creciente, y la primera ya basta para la mayoría.

   1. **Una sección obligatoria en la plantilla de la *spec*.** `feature-spec` ya genera *Durable Documentation Impact*: que esa sección tenga una línea fija —«cambio de OpenSpec: `openspec/changes/<id>/`, o **ninguno**, y por qué»— y que `feature-validator` la exija para conceder `accepted`. Es la opción barata y la que de verdad cierra el agujero, porque convierte el olvido en un rechazo del validador en lugar de en una divergencia silenciosa.
   2. **Una comprobación en la barrera**: que ninguna *spec* de una *feature* marcada como «toca capacidad» se quede sin su carpeta en `openspec/changes/`.
   3. **Generación en una dirección**, de la *feature* hacia la capacidad: derivar el esqueleto del cambio de OpenSpec desde los *Acceptance Scenarios* de la *spec*. Nunca al revés: la capacidad no se deduce de un plan de implementación.

**Lo que no hay que hacer, y conviene decirlo.** Unificar los dos ficheros. Se intentaría por ahorro y se perdería lo único que hace útil a cada uno: la *spec* de la *feature* **muere** cuando la *feature* se acepta, y la de OpenSpec **sobrevive**. Un documento que es las dos cosas acaba siendo un plan de implementación viejo que nadie se atreve a borrar porque alguien lo cita como contrato.

**Valor.** Es lo que impide que el coste escrito en D2.1 —«se escribe dos veces»— se convierta en el riesgo que ya está materializado en este repositorio: **dos árboles de OpenSpec** (MF10), uno de ellos con la *spec* que la validación previa de coste tiene que respetar y que es la más fácil de no ver. La duplicidad no empieza por mala fe: empieza porque nadie comprueba que el segundo sitio se actualizó.
