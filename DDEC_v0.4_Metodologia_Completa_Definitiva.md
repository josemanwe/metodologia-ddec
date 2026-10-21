# DDEC — Desarrollo Dirigido por Especificación Conversacional
## Metodología operativa, versión 0.4

**Autor:** Jose Tomás Caballero García  
**Fecha:** 20 de octubre de 2026  
**Estado:** propuesta metodológica operativa, pendiente de validación externa  
**Lema:** *Primero el plano, después la obra.*

> **Nota de alcance.** DDEC es una propuesta nacida de la práctica de su autor. La versión 0.4 formaliza sus procedimientos, pero no afirma todavía superioridad empírica frente a otras metodologías. Se prevé publicar la metodología tras documentar tres casos prácticos de distinta complejidad. Las denominaciones y comparaciones con proyectos externos son orientativas y deben revisarse antes de la publicación definitiva.

---

## 1. Propósito, alcance y público

DDEC transforma una idea o necesidad en software construido con asistencia sustancial de agentes de IA mediante una secuencia explícita de **entrevista, especificación, aprobación, implementación por fases, verificación independiente y aceptación humana**. El centro del trabajo de dirección no es redactar cada línea de código, sino definir y mantener un acuerdo de requisitos comprobables.

DDEC sirve tanto para personas sin formación técnica como para desarrolladores y equipos profesionales. **Accesible no significa autónomamente seguro:** cuando el riesgo o la complejidad excedan las competencias del director, este debe incorporar apoyo experto (§3). La IA no sustituye responsabilidades legales, técnicas ni contractuales.

Cubre el ciclo de vida completo: viabilidad, diseño, construcción, pruebas, entrega, operación, mantenimiento, cambios y retirada. Se aplica tanto a proyectos nuevos como a la evolución de productos existentes (§5.2.1), desde un script hasta un sistema de mayor criticidad, ajustando la documentación y los controles al nivel (§4).

**No promete:** ausencia de defectos, cumplimiento legal automático, costes siempre inferiores, verificación exhaustiva ni resultados mejores sin evidencia. Tampoco exige un proveedor, modelo, lenguaje o IDE concretos.

### 1.1. Qué es obligatorio y qué es orientativo

**Lo obligatorio está definido de forma exhaustiva en los criterios de conformidad (§17).** Las reglas marcadas en el texto como **OBLIGATORIO** o **CONDICIONAL** desarrollan alguno de esos criterios e indican a cuál corresponden. Todo lo demás es recomendado.

- **OBLIGATORIO:** exigido en el nivel o niveles indicados.
- **CONDICIONAL:** obligatorio cuando se cumple la condición indicada.
- **EJEMPLO:** configuración ilustrativa, no prescripción universal.

**Terminología.** *Etapa* es una parte del ciclo de vida (§5). *Fase* es una unidad de construcción con objetivo y criterios de aceptación propios. No se usan otros términos como sinónimos normativos. Los niveles de aplicación no eliminan los principios, sino que adaptan sus artefactos.

## 2. Los siete principios

1. **La especificación aprobada es la referencia acordada.** El SPEC vigente describe el comportamiento acordado. Si difiere del producto, se abre una incidencia o solicitud de cambio; ninguna de las partes lo modifica silenciosamente. El SPEC no sustituye al contrato con un cliente; si existe contrato, puede remitir a una versión aprobada del SPEC.
2. **El humano conserva la autoridad sobre las decisiones.** La IA propone y ejecuta dentro de límites autorizados. Alcance, prioridades, presupuesto y riesgos aceptados requieren la autoridad humana correspondiente.
3. **Se especifica lo necesario antes de construir.** No se inicia una fase con decisiones bloqueantes sin resolver para esa fase. El descubrimiento de nuevos requisitos durante el desarrollo es normal y se gestiona formalmente según su impacto (§7).
4. **La entrevista facilita decisiones informadas.** Se priorizan opciones concretas, recomendación razonada y alternativa abierta; las preguntas abiertas se usan cuando las opciones predefinidas distorsionan el problema.
5. **La construcción avanza en fases verificables.** Cada fase tiene objetivo, entregables, criterios observables y pruebas acordes al nivel; no se confunde avance de código con aceptación.
6. **Nadie da por bueno su propio trabajo.** El constructor puede autocomprobar y corregir, pero no certifica su resultado; la verificación se realiza en una sesión separada (§3) y la aceptación corresponde al humano. El mismo criterio se aplica a la revisión del SPEC (§5.3).
7. **La supervisión y la seguridad son proporcionales al riesgo.** Los controles relevantes se aplican desde el inicio y durante todas las fases. No se entrega a cliente ni se despliega en producción sin autorización humana.

## 3. Roles y autoridad

| Rol | Responsable habitual | Puede | No puede |
| --- | --- | --- | --- |
| **Director** | Humano: promotor, profesional o representante autorizado. Incorpora apoyo experto (técnico, de seguridad o jurídico) cuando el nivel o sus competencias lo exijan | Aprobar SPEC, nivel, prioridades, cambios, aceptación y despliegues | Delegar tácitamente responsabilidades que requieren juicio humano o profesional |
| **Analista** | IA conversacional con dirección humana | Entrevistar, proponer opciones, detectar huecos, redactar especificaciones | Inventar decisiones, dar por aprobados requisitos o revisar su propio borrador en la misma sesión |
| **Constructor** | Agente de código | Implementar la fase aprobada, probar localmente, corregir defectos, proponer cambios | Alterar alcance o aceptar su propia entrega |
| **Verificador** | Agente en sesión separada; otro modelo o herramienta cuando convenga | Derivar y ejecutar pruebas, inspeccionar código, aportar evidencias y dictamen | Corregir código durante la verificación o sustituir la aceptación humana |

**Sesión separada (OBLIGATORIO, §17.5).** Se considera sesión separada un contexto de trabajo independiente del historial conversacional y del razonamiento de la sesión cuyo resultado revisa. Un mensaje nuevo dentro de la misma conversación no es una sesión separada. Las entradas y el acceso del verificador se definen en §9.1.

**Grados de independencia de la verificación:**

| Nivel | Exigencia |
| --- | --- |
| Rápido | Sesión separada |
| Estándar | Sesión separada; se recomienda otro modelo o herramienta cuando sea viable |
| Completo (OBLIGATORIO, §17.12) | Sesión separada con otro modelo o herramienta, más revisión de apoyo experto |

Cambiar de modelo reduce potencialmente errores correlacionados, pero no garantiza independencia absoluta.

**Director no técnico:** puede dirigir alcance y valor de negocio. En nivel completo, el apoyo experto es obligatorio (§17.12); en los demás niveles se recomienda siempre que el director no pueda valorar por sí mismo un riesgo. El director puede programar; DDEC no lo prohíbe.

### 3.1. Matriz de decisiones

| Decisión | Propone | Autoriza |
| --- | --- | --- |
| Nivel DDEC | Analista | Director |
| Aprobación de una versión del SPEC (incluido el plan de fases) | Analista | Director |
| Ajuste técnico menor (definición en §7.1) | Constructor | Constructor, con registro |
| Corrección que restaura comportamiento ya especificado | Constructor | Constructor implementa; verificador comprueba; director acepta la fase |
| Nuevo requisito, cambio de alcance o aceptación de riesgo | Cualquier rol | Director |
| Aceptar o diferir hallazgos medios o bajos que no incumplen criterios de aceptación | Verificador informa | Director |
| Excepción de seguridad, pagos o privacidad | Analista o constructor | Director, con apoyo experto en nivel completo (§17.12) y, en los demás, cuando no pueda valorar el riesgo |
| Cierre de fase | Verificador informa | Director |
| Entrega a cliente o despliegue en producción | Constructor o director | Director |

## 4. Niveles y clasificación del riesgo

El analista propone el nivel en la etapa de viabilidad y el director lo decide y lo justifica en `VIABILIDAD.md` o, en nivel rápido, en una nota breve que después se incorpora al SPEC. **El tamaño no equivale al riesgo:** un script corto que procesa pagos no es de nivel rápido.

| Nivel | Uso típico | Especificación | Trazabilidad | Verificación |
| --- | --- | --- | --- | --- |
| **Rápido** | Prototipo, landing o automatización de bajo riesgo | SPEC breve, entrevista reducida | Lista numerada de criterios y comprobaciones | Sesión separada y aceptación humana |
| **Estándar** | Web o aplicación de negocio convencional | SPEC, instrucciones de agentes y decisiones | IDs de requisitos, criterios y pruebas | Por fase, con evidencias y regresión; otro modelo recomendado |
| **Completo** | Sistemas críticos, datos especialmente protegidos o impacto elevado | Kit ampliado, análisis de amenazas y registros | Matriz de trazabilidad y evidencias auditables | Otro modelo o herramienta, revisión de apoyo experto y aprobación reforzada |

**Factores de clasificación:** sensibilidad de datos, efectos de un fallo, exposición pública, acceso a infraestructura, volumen de usuarios, dependencia de terceros, reversibilidad, exigencias regulatorias y capacidad del equipo para supervisar.

**Umbrales mínimos (OBLIGATORIO, §17.1).** Los factores orientan la decisión, pero estos supuestos fijan un nivel mínimo:

| Si el sistema… | Nivel mínimo |
| --- | --- |
| Trata datos personales (salvo la excepción de datos de contacto básicos), procesa pagos, accede a producción o a infraestructura de terceros | Estándar |
| Trata categorías especiales de datos personales (por ejemplo, datos de salud), trata datos de menores, puede causar daño físico o económico grave, o está sujeto a regulación sectorial específica | Completo |

**Excepción de datos de contacto básicos.** Un sistema puede mantenerse en nivel rápido si se limita a recoger datos de contacto ordinarios (por ejemplo, nombre, correo electrónico, teléfono y un mensaje de contacto), facilitados voluntariamente por el usuario, sin solicitar información sensible ni realizar tratamientos adicionales distintos de su transmisión al destinatario. No debe almacenar esos datos en una base de datos propia. El reenvío, por ejemplo mediante correo electrónico, puede implicar su conservación en buzones o registros técnicos y no elimina las obligaciones legales aplicables, como informar al usuario o disponer de base legal. La excepción no se aplica si concurre cualquier supuesto de nivel completo.

El director puede elevar el nivel, nunca rebajarlo por debajo del umbral.

**Regla de escalado (OBLIGATORIO, §17.1):** si aparece un riesgo que supera el nivel elegido, se pausa la actividad afectada y se reclasifica antes de continuar.

Los números de rondas o fases que aparecen en este documento son ejemplos, nunca límites universales.

## 5. Ciclo de vida DDEC

```text
Idea / necesidad (o producto existente)
      ↓
0. Viabilidad y clasificación de riesgo
      ↓
1. Entrevista y descubrimiento de requisitos
      ↓
2. SPEC con plan de fases + revisión en sesión separada + aprobación humana
      ↓
3. Preparación del entorno → puerta de entrada a construcción
      ↓
4. Construcción de una fase + autocomprobación
      ↓
5. Verificación en sesión separada → dictamen
      ├─ NO APTO: defecto de implementación → volver a 4
      │           defecto de especificación o cambio de alcance → aprobación del cambio (§7) → volver a 4
      ├─ BLOQUEADO: el director resuelve el bloqueo → volver a 4 o 5
      └─ APTO: revisión del director
              ├─ Rechaza: defecto de implementación → volver a 4
              │           defecto de especificación → aprobación del cambio (§7) → volver a 4
              └─ Acepta: registro y cierre de fase → ¿quedan fases? sí → volver a 4
      ↓ (todas las fases cerradas)
6. Entrega y autorización de despliegue
      ↓
7. Operación, mantenimiento, cambios y retirada
```

El circuito 4–5 se repite por fase. Una modificación posterior **no obliga** a repetir toda la viabilidad: se reevalúan únicamente alcance, coste y riesgos afectados. Los cambios de alcance pueden requerir volver a la entrevista.

### 5.1. Etapa 0: viabilidad

Antes de una entrevista extensa se documentan, en `VIABILIDAD.md` o, en nivel rápido, en una nota breve que después se incorpora como sección del SPEC:

- Problema, destinatarios, valor esperado y alternativa de no construir.
- Producto mínimo útil y exclusiones.
- Nivel DDEC y su justificación conforme a los umbrales de §4.
- Hipótesis, dependencias y riesgos técnicos, legales y comerciales.
- Estimación **en intervalos**, con supuestos: dirección humana, implementación, verificación, correcciones, herramientas, uso de modelos, infraestructura, operación y mantenimiento.
- Decisión del director: continuar, reducir alcance, investigar o descartar.

No se estima por líneas de código. La estimación por fases es una herramienta, no una fórmula garantizada.

**Relación con la propuesta comercial.** Cuando hay un cliente, `VIABILIDAD.md` puede servir de base para el presupuesto o la propuesta: alcance mínimo, exclusiones, nivel, intervalos de coste y riesgos ya están documentados. La propuesta aceptada no sustituye a la aprobación del SPEC, y las diferencias entre ambas se resuelven antes de construir.

### 5.2. Etapa 1: entrevista conversacional

El analista realiza rondas breves, agrupadas por problema, usuarios, procesos, datos, integraciones, restricciones, seguridad, experiencia y operación. Se recomiendan entre tres y cuatro preguntas por ronda, con opciones, consecuencias y recomendación justificada.

Cada respuesta se registra como decisión resuelta o como cuestión pendiente. Se admiten preguntas abiertas para descubrir necesidades no previstas. El analista debe cuestionar premisas inseguras, detectar contradicciones y distinguir hechos confirmados de sugerencias.

**Estados de una cuestión:**

| Estado | Significado | Efecto |
| --- | --- | --- |
| Resuelta | Decisión aprobada por el director | Puede implementarse |
| Pendiente no bloqueante | Puede posponerse sin afectar a la fase en curso | Se registra responsable y fecha o condición de revisión |
| Pendiente bloqueante | Impide definir o probar una fase | No se inicia esa fase |

**Supuestos.** Un supuesto es una cuestión pendiente con su condición de validación (quién lo comprueba, cómo y antes de qué fase). Se clasifica como bloqueante o no bloqueante igual que cualquier otra cuestión; ninguna fase se construye sobre un supuesto bloqueante sin validar.

**Condición de salida:** información suficiente para redactar el SPEC con su plan de fases; objetivos, límites, usuarios, requisitos prioritarios y riesgos claros; sin cuestiones bloqueantes para la primera fase.

#### 5.2.1. Productos existentes

Cuando el sistema ya existe sin SPEC, la etapa 1 parte del producto: el analista documenta su comportamiento actual (a partir del código, la documentación disponible y el uso real) y redacta un **SPEC de línea base**, que el director aprueba como descripción del comportamiento conocido y documentado del estado actual, no como garantía de que se haya identificado todo su funcionamiento ni como diseño deseado. A partir de ahí, toda modificación se tramita como solicitud de cambio (§7) y se verifica con regresión sobre el comportamiento documentado.

### 5.3. Etapa 2: SPEC, revisión y aprobación

El analista produce un borrador del SPEC, **incluido el plan de fases** (§6.1). El borrador se revisa en **una sesión separada de la que lo redactó** (principio 6), buscando:

- Requisitos ambiguos, contradictorios o duplicados.
- Flujos principales y alternativos omitidos; errores y condiciones límite.
- Requisitos no funcionales sin métrica.
- Dependencias, supuestos y cuestiones bloqueantes.
- Privacidad, seguridad, accesibilidad y obligaciones aplicables.
- Criterios de aceptación no verificables o sin requisito asociado.
- Fases mal delimitadas o incompatibles con presupuesto y alcance.

La revisión genera hallazgos; **no certifica que el SPEC sea completo**. El director decide las cuestiones abiertas, valida el alcance y aprueba una versión identificada del documento. En nivel completo, la revisión del SPEC se realiza además con otro modelo o herramienta y con apoyo experto técnico (§17.12); cuando existan obligaciones legales relevantes, se incorpora también revisión jurídica.

Al estar el plan de fases dentro del SPEC, añadir, eliminar o redefinir una fase es un cambio de SPEC (§7).

### 5.4. Etapa 3: preparación del entorno

Se preparan repositorio, entorno de desarrollo y de pruebas, permisos de los agentes, secretos fuera del código, comandos de ejecución y las reglas de `AGENTS.md` o, en nivel rápido, su sección del SPEC (incluido el límite de reintentos, §5.6).

**Puerta de entrada a construcción (OBLIGATORIO, §17.3 y §17.4):** versión del SPEC aprobada, fase delimitada con criterios comprobables, cuestiones bloqueantes de esa fase resueltas y entorno preparado.

### 5.5. Etapa 4: construcción

El constructor recibe **una fase incluida en el SPEC aprobado**, el SPEC vigente y las reglas del repositorio. Puede tomar ajustes técnicos menores (§7.1). Si descubre una contradicción, un requisito nuevo o una decisión que no sea un ajuste menor, detiene la parte afectada y abre una solicitud de cambio o consulta dirigida al director.

Se permiten commits de trabajo intermedios; el cierre de fase exige un estado versionado identificable y aceptado.

Debe ejecutar autocomprobaciones y entregar **al director** la referencia del código y un resumen de modificaciones, ajustes técnicos menores, pruebas realizadas y limitaciones. El resumen se conserva en el registro de la fase, pero no forma parte de las entradas del verificador (§9.1). No se autoriza a modificar el SPEC aprobado por iniciativa propia.

### 5.6. Etapa 5: verificación y aceptación

El verificador, en sesión separada, trabaja con las entradas y el acceso definidos en §9.1. Deriva sus pruebas de los requisitos y criterios, no de explicaciones del constructor.

**Salida mínima:** pruebas ejecutadas, resultado, evidencia, entorno, versión, hallazgos clasificados por severidad (§9.3), requisitos sin cubrir y dictamen de la fase:

- `APTO`: se cumplen todos los criterios de aceptación exigidos y no hay hallazgos críticos ni altos abiertos. Pueden quedar hallazgos medios o bajos que no incumplan dichos criterios; el director decide si los acepta o difiere. No equivale a garantía de ausencia de defectos.
- `NO APTO`: existe algún hallazgo crítico o alto, o un incumplimiento demostrable de un criterio de aceptación exigido, con independencia de la severidad asignada.
- `BLOQUEADO`: faltan datos, acceso, entorno o decisiones para comprobar algún criterio. Lo resuelve el director; un bloqueo no se trata como defecto de código sin evidencia.

**Precedencia:** si en una misma fase concurren resultados distintos, el dictamen es `NO APTO` cuando exista algún incumplimiento; en su defecto, `BLOQUEADO` cuando algún criterio no haya podido comprobarse; solo en ausencia de ambos, `APTO`.

**Criterios incumplidos.** Un criterio de aceptación incumplido no puede aceptarse como hallazgo medio o bajo. Para darlo por bueno hay que modificar el SPEC mediante el protocolo de cambio (§7).

Tras `APTO`, el director revisa el informe y realiza la validación funcional proporcional al nivel. Puede **aceptar, rechazar o solicitar aclaraciones**. Si rechaza, clasifica el motivo según §7.1: un defecto de implementación vuelve al constructor y exige nueva verificación; un defecto de especificación sigue el protocolo de cambio. El siguiente informe de verificación incorpora pruebas que cubran el defecto detectado. Una fase solo se cierra tras aceptación humana.

**Reintentos:** el valor recomendado es un máximo de **tres ciclos de corrección y verificación por hallazgo** antes de escalar al director, configurable en `AGENTS.md` (o, en nivel rápido, en el SPEC). Se escala antes ante hallazgos críticos, duda de especificación, repetición del mismo fallo o coste desproporcionado.

### 5.7. Etapa 6: entrega y despliegue

Antes de entregar se comprueba: objetivos medibles (§6.1, punto 2) y requisitos no funcionales, pruebas de regresión, documentación mínima, seguridad y privacidad aplicables, migraciones y copias de seguridad cuando haya datos persistentes, plan de reversión, monitorización y responsables operativos (en `OPERACION.md` cuando sea exigible, §6).

**Ningún agente despliega en producción sin autorización expresa del director** (§17.10), que cuenta con el apoyo experto que exija el nivel. Se conserva referencia a la versión del SPEC, del código y de los resultados de pruebas.

### 5.8. Etapa 7: operación, evolución y retirada

Las incidencias de producción se clasifican por impacto y urgencia. Una corrección se vincula al comportamiento especificado; si el requisito era erróneo, se tramita un cambio. Se incluyen regresión, seguimiento posterior, actualización de dependencias, revisión de accesos, copias de seguridad y respuesta ante incidentes según el nivel.

La retirada de un sistema exige evaluar exportación o eliminación de datos, obligaciones de conservación, revocación de accesos, cierre de servicios y comunicación a afectados cuando proceda.

## 6. Contrato documental y artefactos

Los nombres son convenciones portables; los adaptadores específicos de herramientas no forman parte del núcleo.

| Artefacto | Función | Nivel |
| --- | --- | --- |
| `VIABILIDAD.md` | Justificación, nivel, riesgo y estimación | Estándar y completo; en rápido, sección del SPEC |
| `SPEC.md` | Requisitos, criterios, plan de fases, alcance y versión aprobada | Todos, con distinta extensión |
| `AGENTS.md` | Límites, comandos, reglas de agentes, reintentos y escalado | Estándar y completo; en rápido, sección del SPEC |
| `CLAUDE.md` | Adaptador de Claude Code que remite a archivos canónicos | Opcional |
| `DECISIONES.md` | Decisiones, alternativas, autor, fecha y motivo | Estándar y completo; en rápido, sección 10 del SPEC |
| `CAMBIOS.md` | Solicitudes de cambio y su resolución | Estándar y completo; en rápido, sección 11 del SPEC |
| `INFORME_VERIFICACION.md` | Pruebas, evidencias y dictamen por fase | Todos, abreviado en rápido |
| `TRAZABILIDAD.md` | Mapa de requisitos, criterios, pruebas y versiones | Completo; tabla integrada en el SPEC en estándar |
| `CHANGELOG.md` | Cambios entregados por versión | Recomendado |
| `OPERACION.md` | Despliegue, recuperación, monitorización y retirada | CONDICIONAL (§17.13): obligatorio si el sistema se despliega en un entorno accesible por terceros o conserva datos persistentes; en otro caso, sección del SPEC |

### 6.1. Estructura mínima del SPEC

1. Identificación, estado, versión, aprobador y fecha.
2. Problema, objetivos medibles y alcance.
3. Usuarios, permisos y casos de uso.
4. Requisitos funcionales identificables y priorizados; en niveles estándar y completo, con identificador único.
5. Requisitos no funcionales medibles: seguridad, privacidad, rendimiento, accesibilidad, fiabilidad y mantenibilidad, según aplique.
6. Datos, integraciones, límites y dependencias.
7. Arquitectura o stack propuesto y razones, cuando proceda.
8. Riesgos, obligaciones legales identificadas y supuestos por validar (el *qué hay que cumplir y por qué*; su traducción en requisitos comprobables va en el punto 5).
9. Plan de fases: para cada fase, identificador, objetivo, requisitos cubiertos, dependencias, entregables, áreas de código autorizadas, criterios de aceptación, pruebas previstas, riesgos y controles pertinentes.
10. Exclusiones y cuestiones abiertas clasificadas.
11. Historial de cambios y referencias a evidencias.

Las fases deben ser pequeñas y coherentes: lo bastante acotadas para que un fallo pueda aislarse y lo bastante completas para aportar un resultado comprobable.

**Ejemplo de trazabilidad (estándar):**

| Requisito | Criterio | Prueba | Estado |
| --- | --- | --- | --- |
| `REQ-014` Evitar reservas duplicadas | `AC-014-01` Dos peticiones simultáneas no confirman el mismo hueco | `TEST-014-01` Prueba de concurrencia | Pendiente |

**Identificadores (OBLIGATORIO en estándar y completo, §17.11):** requisitos, criterios y pruebas llevan identificador; su formato es un EJEMPLO. En nivel rápido basta un listado numerado que relacione criterio y comprobación.

### 6.2. Control de versiones del SPEC

El documento identifica versión, estado (`borrador`, `en revisión`, `aprobado`, `sustituido`) y responsable de aprobación. La implementación se vincula a una versión concreta.

| Tipo (§7.1) | Efecto en la versión |
| --- | --- |
| Cambio de alcance | Sube la versión mayor (v1.x → v2.0) |
| Corrección de un defecto de especificación | Sube la versión menor (v1.2 → v1.3) |
| Ajuste técnico menor | No modifica el SPEC ni su versión |

La actualización no reescribe silenciosamente el acuerdo anterior: registra qué cambió, por qué y desde cuándo se aplica.

## 7. Gestión de cambios y defectos

**Principio:** descubrir un requisito nuevo no es un fallo del método; introducirlo sin control sí lo es.

### 7.1. Clasificación

- **Defecto de implementación:** el código incumple el SPEC aprobado; el constructor corrige y el verificador repite pruebas.
- **Defecto de especificación:** el SPEC es ambiguo, inconsistente o insuficiente sin que cambie lo que se quiere construir; el analista propone corrección y el director aprueba.
- **Cambio de alcance:** nueva capacidad o modificación del comportamiento aprobado, incluidas las fases; requiere valoración y autorización del director.
- **Ajuste técnico menor:** decisión reversible que no cambia el comportamiento observable, el alcance, el riesgo, el coste de forma relevante ni los elementos fijados en el SPEC (por ejemplo, el stack del punto 7). El constructor puede resolverla registrándola. Sustituir un componente fijado en el SPEC no es un ajuste menor.

### 7.2. Protocolo de cambio

1. Registrar la solicitud con identificador, origen y motivo (en `CAMBIOS.md` o en la sección 11 del SPEC en nivel rápido). Los ajustes técnicos menores se registran en el resumen del constructor, que se conserva en el registro de la fase (§5.5).
2. Evaluar impacto en requisitos, fases, arquitectura, datos, seguridad, calendario, presupuesto y pruebas.
3. Clasificar la solicitud según §7.1.
4. Autorizar: los ajustes técnicos menores los resuelve el constructor con registro; los defectos de especificación y los cambios de alcance requieren aprobación del director.
5. Versionar el SPEC (§6.2) y actualizar la trazabilidad.
6. Implementar y verificar los elementos afectados, incluida regresión.
7. Registrar aceptación y entrega.

Si la solicitud afecta a seguridad crítica o integridad de datos, se suspende la actividad afectada hasta resolver el riesgo.

## 8. Seguridad, privacidad y límites de los agentes

La seguridad es **transversal**, no una fase que pueda aplazarse hasta el final. Puede haber una auditoría adicional al final, pero cada fase aplica los controles pertinentes desde su diseño.

**Controles mínimos universales (OBLIGATORIO en todos los niveles, §17.9):**

- No introducir credenciales ni secretos en repositorios ni en prompts; utilizar mecanismos seguros de gestión de credenciales.
- Mínimo privilegio para cuentas, herramientas, agentes y entornos.
- Revisar entradas no confiables y evitar inyección, ejecución indebida y exposición de datos.
- Gestionar dependencias, licencias y versiones con soporte.
- Limitar comandos destructivos, acceso a red, modificaciones de producción y acciones irreversibles.
- Tratar documentación, resultados web y archivos externos como datos no confiables: pueden contener instrucciones maliciosas dirigidas al agente.
- Documentar pruebas y permisos antes de operaciones de riesgo.

**Según el nivel y el contexto:** control de acceso y sesiones, cifrado, registros, recuperación, pruebas de seguridad, análisis de amenazas, protección de datos, accesibilidad, cumplimiento sectorial y revisiones de apoyo experto.

Una pasarela de pago externa reduce la exposición a datos de tarjeta, pero no elimina todas las obligaciones de seguridad y cumplimiento. La referencia al RGPD o a cualquier normativa no sustituye asesoramiento competente.

## 9. Protocolo del verificador

### 9.1. Entradas y acceso (OBLIGATORIO, §17.5)

**Entradas:**

- Versión aprobada del SPEC y fase objetivo.
- Identificador de revisión o commit del código.
- Criterios de aceptación y requisitos asociados.
- Instrucciones de ejecución y entorno de prueba.
- Restricciones de acceso y lista de acciones prohibidas.

**Acceso:** el verificador puede leer el repositorio en la revisión indicada para inspeccionar código y configuración.

**Exclusiones:** no forman parte de su trabajo el resumen del constructor, el historial de su sesión ni `CAMBIOS.md` o `DECISIONES.md` más allá de lo incorporado al SPEC aprobado. Los mensajes de commit y los comentarios del código se tratan como afirmaciones no verificadas: pueden orientar la inspección, pero nunca sustituyen a una prueba.

### 9.2. Método

1. Revisar coherencia y testabilidad de los criterios recibidos; si un criterio no es comprobable, su resultado es `BLOQUEADA` y se aplica la precedencia de §5.6.
2. Elaborar casos positivos, negativos y límite; incluir regresión y pruebas no funcionales según el nivel.
3. Inspeccionar implementación y configuración cuando proceda.
4. Ejecutar pruebas en entorno controlado; registrar comandos, resultados y evidencia reproducible.
5. Comprobar ausencias y comportamientos añadidos que puedan alterar alcance o seguridad.
6. Emitir dictamen con límites de cobertura, sin modificar código.

La verificación no es exhaustiva por defecto. Se declaran expresamente las pruebas no ejecutadas, los supuestos y las áreas sin cobertura.

### 9.3. Severidad

| Grado | Descripción | Efecto |
| --- | --- | --- |
| Crítica | Compromiso grave de seguridad, datos o funcionamiento esencial | `NO APTO`; escalado inmediato al director, sin agotar reintentos |
| Alta | Incumplimiento de requisito esencial o regresión relevante | `NO APTO` |
| Media | Defecto significativo no esencial | Compatible con `APTO` solo si no incumple criterios de aceptación exigidos; el director decide corregirlo o aceptarlo con riesgo documentado |
| Baja | Detalle menor | Compatible con `APTO` solo si no incumple criterios de aceptación exigidos; puede diferirse con registro |

No se permite aceptar un riesgo como forma de eludir obligaciones legales o controles imprescindibles.

### 9.4. Plantilla de informe

```md
# Informe de verificación — FASE-XX
SPEC: vX.Y (aprobado) | Código: <commit> | Entorno: <descripción>
Fecha: <fecha> | Verificador: <herramienta/sesión>

## Alcance y cobertura
- Requisitos/criterios revisados:
- Pruebas no ejecutadas y motivo:
- Pruebas añadidas por defectos detectados anteriormente (en verificación o por el director):

## Evidencias
| Prueba | Criterio | Resultado | Evidencia |
| --- | --- | --- | --- |
| TEST-... | AC-... | PASA/FALLA/BLOQUEADA | comando, log o captura |

## Hallazgos
| ID | Severidad (§9.3) | Hecho observable | Reproducción | Tipo (§7.1) |
| --- | --- | --- | --- | --- |

## Dictamen (precedencia §5.6)
APTO / NO APTO / BLOQUEADO
Hallazgos medios/bajos pendientes de decisión del director:
Limitaciones:
Cuestiones pendientes:
```

## 10. Entrevista: protocolo y prompt de inicio

**Formato preferido:** rondas cortas con alternativas `A/B/C/Otra`, recomendación y consecuencia principal de cada opción. No se fuerzan opciones cerradas cuando la pregunta requiere descubrimiento abierto.

**Prompt de analista:**

```text
Actúa como ANALISTA DDEC. Idea: [descripción]. Usuarios: [quiénes].
Nivel inicial: [rápido/estándar/completo o por determinar].
[Si existe producto: describe primero su comportamiento actual.]

Entrevístame por rondas de 3-4 preguntas relacionadas.
Ofrece opciones concretas, una recomendación justificada y la opción
«Otra». Identifica riesgos, contradicciones, supuestos y necesidades
que no haya mencionado. No inventes respuestas.
Registra cada cuestión como resuelta, pendiente no bloqueante o
pendiente bloqueante; trata los supuestos como pendientes con su
condición de validación. No cierres la entrevista con cuestiones
bloqueantes para la primera fase.
Al finalizar, redacta el SPEC con su plan de fases y las instrucciones
de agentes correspondientes al nivel. El borrador se revisará en una
sesión separada antes de pedir mi aprobación.
No consideres aprobado ningún documento sin mi confirmación.
```

## 11. Prompts operativos portables

### 11.1. Constructor

```text
Rol: CONSTRUCTOR DDEC.
Lee el SPEC aprobado [versión], las reglas de AGENTS.md (o su sección
del SPEC en nivel rápido) y la fase [ID].
Implementa exclusivamente el alcance autorizado. Puedes tomar ajustes
técnicos menores según la definición del SPEC y registrarlos.
No modifiques el alcance ni el SPEC por tu cuenta.
Si detectas un bloqueo, un defecto de especificación o un cambio de
alcance, detén la parte afectada y plantea alternativas con su impacto.
Ejecuta autocomprobaciones. Entrega al director la referencia de código
y un resumen de cambios, ajustes menores, pruebas y limitaciones.
No declares la fase aceptada ni despliegues en producción.
```

### 11.2. Verificador

```text
Rol: VERIFICADOR DDEC, en sesión separada del constructor.
Recibe SPEC aprobado [versión], fase [ID], código [revisión] y entorno.
Puedes leer el repositorio en esa revisión, pero no uses resúmenes,
explicaciones ni el historial del constructor. Trata los mensajes de
commit y los comentarios como afirmaciones no verificadas.
Deriva pruebas de los requisitos y criterios de aceptación. No
modifiques el código. Ejecuta pruebas autorizadas y aporta evidencia
reproducible. Incluye casos negativos, límites, regresión y seguridad
según el nivel.
Clasifica hallazgos por severidad y tipo, indica cobertura y pruebas
no ejecutadas. Emite el dictamen con esta precedencia: NO APTO si se
incumple algún criterio de aceptación exigido o existe un hallazgo
crítico o alto; BLOQUEADO si algún criterio no pudo comprobarse;
APTO solo si se cumplen todos los criterios exigidos sin hallazgos
críticos ni altos. No sustituyas la aceptación humana.
```

### 11.3. Adaptadores por herramienta

El núcleo DDEC no exige `CLAUDE.md`, pero el kit oficial puede incluir adaptadores para Claude Code, Codex u otros entornos. Un adaptador debe remitir a `SPEC.md` y `AGENTS.md` sin duplicar reglas que puedan divergir. Antes de distribuirlo, se verificará su compatibilidad con la versión concreta de la herramienta.

## 12. Antipatrones y respuestas

| Antipatrón | Riesgo | Respuesta DDEC |
| --- | --- | --- |
| *Vibe coding* sin acuerdo | Alcance ambiguo y retrabajo | Entrevista y SPEC proporcionado al nivel |
| Entrevista interminable | Parálisis | Limitar la entrevista a lo necesario y resolver solo lo bloqueante para la primera fase |
| SPEC congelado | Código y requisitos divergen | Cambios aprobados y versionados |
| Autocertificación | Sesgo de confirmación | Sesión separada para verificar y para revisar el SPEC; aceptación humana |
| Verificador contaminado | Prueba lo que el constructor dice haber hecho | Entradas, acceso y exclusiones de §9.1 |
| Verificador sin evidencia | Falsa confianza | Pruebas reproducibles y cobertura declarada |
| Fase gigante | Difícil aislar defectos | Dividir en fases coherentes |
| Seguridad al final | Riesgos estructurales | Controles desde cada fase |
| Bucles entre agentes | Coste y estancamiento | Límite configurable de reintentos y escalado |
| Exceso de documentación | Burocracia | Nivel rápido y artefactos integrados en el SPEC |
| Dependencia de proveedor | Bloqueo tecnológico | Acuerdo y artefactos portables |

## 13. Estado del arte y posicionamiento

DDEC se sitúa en la familia de prácticas de **desarrollo dirigido por especificaciones (SDD)**, ingeniería de requisitos y desarrollo asistido por agentes. No reivindica haber inventado la especificación previa, las entrevistas, los roles separados ni las pruebas por fases.

**Referencias a contrastar antes de la publicación pública:**

- **GitHub Spec Kit:** especificación, planificación, tareas y ejecución asistida.
- **Kiro:** flujos de requisitos, diseño y tareas con asistencia de IA.
- **BMAD Method:** procesos y agentes especializados por roles.
- **OpenSpec:** gestión de especificaciones y cambios.

**Características distintivas propuestas, no exclusividad demostrada:** entrevista conversacional con opciones razonadas, accesible a directores no técnicos; conexión de viabilidad, alcance y propuesta comercial (§5.1); separación de sesiones para construir, verificar y revisar el SPEC; proporcionalidad por riesgo con umbrales mínimos; especificación como acuerdo portable y verificable; documentación originaria en español.

La diferenciación debe evaluarse frente a versiones concretas de herramientas y flujos, evitando afirmaciones de novedad absoluta.

## 14. Plan de validación previa a publicación

Se adopta una **validación exploratoria con tres casos documentados**:

1. Proyecto pequeño de bajo riesgo.
2. Aplicación estándar con usuarios, datos y permisos.
3. Evolución de un producto existente, partiendo de un SPEC de línea base (§5.2.1), con cambios y regresiones.

Para cada caso se conservarán: problema inicial, decisiones, SPEC aprobado, fases, cambios, pruebas, fallos, costes, tiempo humano, tiempo de agentes, defectos detectados, retrabajo y valoración del resultado.

**Métricas sugeridas:** porcentaje de criterios aceptados, defectos por severidad, tiempo hasta aceptación, número de cambios, coste total, rondas de corrección, defectos detectados por el director tras un `APTO`, incidencias tras la entrega y satisfacción del director o usuario.

Si es viable, comparar con prompts libres y con un flujo SDD existente, manteniendo equivalentes los requisitos y condiciones. Tres casos no prueban superioridad estadística; permiten identificar utilidad, fricciones y límites. Se publican también los resultados negativos.

**Condición de publicación prevista:** casos documentados, plantillas utilizables, revisión de referencias externas y límites explícitos. Hasta entonces, la metodología se etiqueta como versión de trabajo o candidata.

## 15. Kit oficial propuesto

- `VIABILIDAD.md`
- `SPEC.md` (variantes rápida, estándar y completa; la rápida integra viabilidad, reglas de agentes, decisiones y cambios)
- `AGENTS.md`
- `CLAUDE.md` y adaptadores adicionales
- `DECISIONES.md`
- `CAMBIOS.md`
- `TRAZABILIDAD.md`
- `INFORME_VERIFICACION.md`
- `OPERACION.md`
- Prompts de entrevista, construcción y verificación
- Tres casos prácticos documentados

El kit se publicará con ejemplos rellenados, no solo plantillas vacías.

## 16. Publicación, licencia y gobernanza

**Decisión editorial:** metodología abierta con atribución y repositorio público recomendado. La documentación puede distribuirse bajo **CC BY 4.0**; las plantillas que se utilicen como software y el código de ejemplo requieren elegir explícitamente una licencia de software apropiada (por ejemplo, MIT o Apache-2.0). No debe suponerse que una única licencia es la mejor para todos los componentes.

La autoría del texto y del método debe atribuirse correctamente. La publicación de un procedimiento no garantiza exclusividad jurídica sobre sus ideas. Antes del lanzamiento se revisarán el nombre, posibles marcas coincidentes, las licencias de dependencias y la atribución a proyectos de referencia.

**Gobernanza recomendada:** versiones numeradas, registro de cambios, canal de propuestas, revisión de contribuciones y distinción entre texto normativo, recomendaciones y adaptadores de herramientas. No existe una certificación DDEC; una eventual certificación requeriría criterios públicos, auditoría y reglas de uso del nombre.

## 17. Criterios de conformidad DDEC

Esta sección es la **lista exhaustiva de requisitos obligatorios** (§1.1). Un proyecto puede **autodeclararse** «desarrollado siguiendo DDEC v0.4, nivel X» si existe evidencia de:

**En todos los niveles:**

1. Nivel elegido conforme a los umbrales mínimos y la excepción de datos de contacto de §4, riesgos evaluados y reclasificación cuando el riesgo cambió.
2. Requisitos documentados y SPEC aprobado, incluido el plan de fases, tras revisión en sesión separada.
3. Cuestiones bloqueantes resueltas antes de la fase afectada.
4. Fases delimitadas con criterios comprobables y entorno preparado antes de construir.
5. Construcción y verificación en sesiones separadas según la definición de §3, con las entradas, el acceso y las exclusiones de §9.1.
6. Evidencias y dictamen de verificación por fase, conforme a la precedencia de §5.6.
7. Aceptación humana de cada fase.
8. Defectos de especificación y cambios de alcance aprobados y versionados según §6.2.
9. Controles mínimos universales de §8 aplicados en todas las fases.
10. Autorización humana antes de entrega o producción.

**En niveles estándar y completo:**

11. Identificadores de requisitos, criterios y pruebas (§6.1).

**En nivel completo:**

12. Verificación con otro modelo o herramienta y revisión de apoyo experto, tanto de la construcción (§3) como del SPEC (§5.3).

**Condicional:**

13. `OPERACION.md` cuando el sistema se despliega en un entorno accesible por terceros o conserva datos persistentes (§6).

La autodeclaración describe **seguimiento del proceso**; no es una certificación ni garantiza calidad, seguridad o cumplimiento legal del producto.

## 18. Registro de decisiones de diseño

### Decisiones de v0.2

| Nº | Decisión | Resultado |
| --- | --- | --- |
| 1 | Público objetivo | Perfiles técnicos y no técnicos, responsabilidades según riesgo |
| 2 | Autonomía de IA | Autonomía controlada |
| 3 | Verificación | Independencia proporcional al riesgo |
| 4 | Nuevos requisitos | Gestión de cambios según impacto |
| 5 | Aprobación del SPEC | Revisión del SPEC en sesión separada y aprobación humana |
| 6 | Trazabilidad | Adaptativa por nivel |
| 7 | Seguridad | Transversal según riesgo |
| 8 | Fallos repetidos | Reintentos limitados y escalado humano |
| 9 | Herramientas | Núcleo independiente con adaptadores oficiales |
| 10 | Distribución | Abierta con atribución |
| 11 | Validación previa | Tres casos prácticos documentados |
| 12 | Alcance | Ciclo de vida completo |

### Decisiones de v0.3

| Nº | Decisión | Resultado |
| --- | --- | --- |
| 13 | Plan de fases | Forma parte del SPEC aprobado; cambiar fases es cambio de SPEC |
| 14 | Resumen del constructor | Se entrega solo al director; no es entrada del verificador |
| 15 | Carácter normativo | §17 es la lista exhaustiva de lo obligatorio |
| 16 | Productos existentes | SPEC de línea base antes de cualquier cambio |
| 17 | Naturaleza del SPEC | Referencia acordada, no sustituye al contrato |
| 18 | Propuesta comercial | `VIABILIDAD.md` como base del presupuesto |
| 19 | Clasificación de nivel | Umbrales mínimos obligatorios por factor de riesgo |
| 20 | Dictamen `APTO` | Todos los criterios exigidos cumplidos y sin hallazgos críticos ni altos; los medios y bajos que no incumplen criterios los decide el director |

### Decisiones de v0.4

| Nº | Decisión | Resultado |
| --- | --- | --- |
| 21 | Obligaciones fuera de §17 | Incorporadas a §17, estructurado por nivel |
| 22 | Acceso del verificador | Repositorio accesible, con exclusión de las explicaciones del constructor; commits y comentarios como afirmaciones no verificadas |
| 23 | Datos de contacto básicos | Excepción acotada que permite el nivel rápido sin almacenamiento propio |
| 24 | Versiones del SPEC | Cambio de alcance sube la mayor; defecto de especificación, la menor |

### Cambios respecto a v0.3

- §17 reorganizado por niveles e incorporadas las obligaciones que estaban dispersas: identificadores, requisitos del nivel completo, controles mínimos universales y `OPERACION.md`.
- Acceso del verificador definido en §9.1 (entradas, acceso y exclusiones); eliminada la contradicción entre §3 y §5.6.
- Excepción de datos de contacto básicos en los umbrales de §4.
- Taxonomía única de cambios (§7.1) vinculada al versionado (§6.2); eliminados los términos «sustancial» y «significativo».
- Regla de precedencia entre dictámenes y prohibición de aceptar como hallazgo medio un criterio incumplido.
- Resumen del constructor conservado en el registro de la fase, con los ajustes técnicos menores.
- Diagrama del ciclo: los cambios de SPEC pasan por aprobación antes de volver a construcción.
- Matriz de decisiones alineada con los grados de apoyo experto de §3.
- «Criterios globales» sustituidos por objetivos medibles y requisitos no funcionales.
- Principio 6 y antipatrón de entrevista reformulados; tamaño de las fases trasladado a §6.1.
- Ajustes finales: ubicación de la viabilidad en nivel rápido antes de que exista el SPEC, reintentos contados por hallazgo y ejemplo de §4 coherente con la excepción de datos de contacto.

## 19. Próximos pasos

1. Revisar y aprobar el texto normativo de v0.4.
2. Crear el kit real de plantillas y adaptadores.
3. Ejecutar los tres casos y registrar resultados, incluidas limitaciones.
4. Incorporar la retroalimentación de usuarios externos.
5. Verificar estado del arte, licencias y atribuciones.
6. Publicar la primera versión pública con historial y documentación.

---

**DDEC v0.4 — Documento de trabajo.**  
*Primero el plano, después la obra.*
