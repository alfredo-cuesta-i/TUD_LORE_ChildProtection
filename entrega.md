# Demo: oportunidad de contacto y disclosure

Es un **trazo sintético y determinista**, no una predicción sobre niños reales. El escenario fija los perfiles, pero no determina todas las acciones; por eso marco cuáles añado solo para poder ejecutar esta demostración.

### Configuración trazable

- Niño:
  - `ChildAgent / Demographics / Age / 14`
  - `ChildAgent / Online Behaviour / Stranger Interaction Frequency / occasional interactions with unknown users`
  - `ChildAgent / Behavioural Responses / Likelihood to Seek Help / seeks help after escalation`
- Agente amenazante:
  - `ThreatActorAgent / Threat Category / Primary Threat Type / grooming`
  - `ThreatActorAgent / Operational Style / Approach Strategy / gradual trust building`
  - `ThreatActorAgent / Threat Progression / Personal Information Requests / requests after rapport`
- Plataforma:
  - `PlatformAgent / Platform Type / Service Category / messaging application`
  - `PlatformAgent / Account Controls / Messaging Restrictions / unrestricted contact`
- El escenario también especifica conocimiento limitado de las actividades del niño por parte de ParentUnit y una relación regular entre niño y docente. No les atribuyo observaciones que no ocurren en esta traza.

Fuente: `grooming_opportunity.md`. Los valores se corresponden con `ChildAgent.md`, `ThreatActorAgent.md` y `PlatformAgent.md`.

### Dos ejecuciones controladas

Comparten el escenario, los agentes, la semilla `0` y los mismos eventos del niño. La diferencia es la política de la plataforma:

- **A — Base:** no añade intervención.
- **B — Privacy reminder:** regla de demostración: ante `Personal information requested`, la plataforma aplica `Privacy reminder`. Es una intervención disponible en la ontología; el escenario no la configura de antemano.

Para completar el recorrido, fijo explícitamente dos acciones no especificadas por el escenario: el niño acepta la solicitud y, más adelante, comparte su nombre. Son entradas controladas de esta demo, no conductas inferidas de su edad o perfil.

| Tiempo | Evento y efecto en la situación |
|---|---|
| T1 | **E-001** ThreatActor-001 → Child-001: `Friend request sent`, `Direct Message`. |
| T2 | **E-002** Child-001 → ThreatActor-001: `Friend request accepted`. **SS-001:** `No relationship + Friend request accepted → New online friendship`. |
| T3 | **E-003** ThreatActor-001 → Child-001: `New conversation started`. |
| T4–T5 | **E-004**, **E-005**: `Conversation continued`. La segunda conversación satisface la condición explícita de conversaciones repetidas. **SS-002:** `New online friendship + Conversation continued + repeated conversations → Established online friendship`. SS-001 queda inactiva. |
| T6 | **E-006** ThreatActor-001: `Trust-building conversation`. **SS-003:** `Established online friendship + Trust-building conversation → Trust building`. |
| T7 | **E-007** ThreatActor-001 → Child-001: `Personal information requested`, después del rapport. No hay observación formal: la ontología de observaciones no define un tipo para solicitudes de información. |
| T7, solo B | **I-001:** `Privacy reminder`, Platform-001 → Child-001. **E-008:** `Privacy reminder shown`, `Platform Notification`. |
| T8 | **E-008 en A / E-009 en B** Child-001: `Personal information shared`, contexto `information_type=name`. **SS-004:** `Trust building + Personal information shared → Dependency formation`. SS-003 queda inactiva. |
| T8 | **O-001 en ambas ejecuciones:** Platform-001 observa `Observes disclosure of personal information`, originada por el evento de disclosure. La conversación es visible para la plataforma; no se propaga automáticamente al padre o al docente. |

Las transiciones siguen `StateTransitionOntology.md`; los eventos y observaciones, `EventOntology.md` y `ObservationGenerationRules.md`. No activo `No relevant signals`: el escenario no lo declara como situación inicial.

**Punto de parada:** registro un checkpoint después del primer disclosure, antes del horizonte de 50 turnos del escenario. Es una condición de parada de esta demo, declarada de antemano, no un estado terminal.

### Outcomes registrados

| Outcome | A — Base | B — Privacy reminder |
|---|---|---|
| Interacción | `Contact established`; `Contact maintained` | Igual |
| Información | `Limited personal information disclosed` | Igual |
| Apoyo | `No adult involved` | Igual |
| Protección | `No intervention` | `Educational intervention` |
| Estado de interacción | `Trust building reached`; `Dependency formation reached` | Igual |
| Sistema | `Single actor observed signals` | Igual |

Los nombres están tomados de `OutcomeOntology.md`. La notificación de privacidad no cambia los eventos posteriores en esta comparación porque fijé la misma acción de disclosure en ambas ejecuciones. **Eso no demuestra que la intervención sea ineficaz**: muestra que hace falta especificar cómo responde el agente niño a un aviso para evaluar ese efecto.

## ¿Para qué serviría?

Esta demo ilustra cómo usar el entorno para:

- **Comparar políticas con las mismas condiciones iniciales:** aquí se ve exactamente qué evento y outcome añade la política de privacidad.
- **Encontrar huecos en la configuración:** por ejemplo, la respuesta del niño al aviso no está determinada por este escenario.
- **Auditar la circulación de información:** la plataforma observa el disclosure; padre y docente no reciben automáticamente el contenido.
- **Probar reglas y límites del sistema:** validar transiciones permitidas, intervenciones disponibles y paradas declaradas.

El resultado permite comparar **trazas sintéticas** y decisiones de política; no permite afirmar tasas reales de prevención ni efectos sobre el bienestar de niños.