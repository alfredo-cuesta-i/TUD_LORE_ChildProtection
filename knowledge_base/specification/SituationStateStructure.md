# SituationStateStructure.md

## Purpose

Defines the canonical representation of situation instances.

The Situation Ontology defines which situations may exist within the simulation environment.

The Interaction Ontology defines how situations may evolve through events and transitions.

This specification defines how active situations are represented during execution.

The objective is to provide a deterministic and reproducible representation of situation state.

This specification does not define:

- probabilities
- risk scores
- causal certainty
- rewards
- utility functions
- intervention policies

The specification only defines how an instantiated situation is represented inside the simulation state.

A Situation State represents the existence of a particular situation at a particular point in simulation time.

A Situation State is not the ontology itself.

A Situation State is an instance of a situation defined by the ontology.

---

## Relationship With Other Specifications

SituationOntology defines:

- what situations may exist

InteractionOntology defines:

- how situations may be activated
- how situations may change

ExecutionSemantics defines:

- when transition evaluation occurs

WorldStateStructure includes:

- the currently active situation states

SituationStateStructure defines:

- how each situation instance is represented

---

## Situation State Structure

SituationState

  identifier

  type

  activation_time

  originating_event

  active

---

## Fields

### identifier

Unique situation-state identifier.

The identifier refers to the specific state instance rather than to the ontology concept itself.

Examples:

SS-001

SS-014

SS-102

Different activations of the same situation may have different identifiers.

---

### type

Situation type represented by the state.

The value must be selected from SituationOntology.

No other values are permitted.

---

#### Relationship Situations

Possible values:

- New online friendship
- Established online friendship
- Dependency formation
- Social isolation

---

#### Manipulation Situations

Possible values:

- Trust building
- Emotional pressure
- Secrecy request
- Coercion

---

#### Protection Situations

Possible values:

- No relevant signals
- Ambiguous signals
- Conflicting signals
- Coordinated protection effort

---

### Consistency Requirement

Every Situation State must reference a valid SituationOntology value.

Invalid situation types are not permitted.

---

### Example

SituationState

  identifier: SS-04

  type:
    Trust building

---

### activation_time

Simulation timestep at which the situation became active.

Examples:

T0

T3

T17

T42

Activation time records when the state first appeared in the simulation.

Activation time does not record when the situation was observed.

Activation time records when the situation became part of the world state.

---

### Example

SituationState

  identifier: SS-06

  type:
    Established online friendship

  activation_time:
    T9

---

### originating_event

Event responsible for activating the situation.

The originating event must be compatible with the transition definitions specified by the Interaction Ontology.

Examples:

- Friend request accepted
- Repeated conversations
- Personal information shared
- Secrecy requested
- Observation reported
- Corroborating observation

---

### Purpose

The originating event provides traceability.

Researchers must be able to determine:

- why the situation exists
- when it appeared
- which event activated it

---

### Example

SituationState

  identifier: SS-11

  type:
    Secrecy request

  activation_time:
    T22

  originating_event:
    Secrecy requested

---

### active

Indicates whether the situation is currently active.

Possible values:

- true
- false

---

### Meaning

true

The situation currently exists within the World State.

false

The situation previously existed but is no longer active.

---

### Example

SituationState

  identifier: SS-09

  type:
    New online friendship

  activation_time:
    T5

  originating_event:
    Friend request accepted

  active:
    false

---

## Situation Lifecycle

### Creation

A Situation State is created when a valid transition activates a situation.

Example:

No relationship

+

Friend request accepted

=

New online friendship

The simulator creates a Situation State representing:

New online friendship

---

### Persistence

A Situation State may remain active for multiple timesteps.

The state remains part of the World State until:

- replaced
- terminated
- superseded
- explicitly deactivated

according to transition rules.

---

### Deactivation

A situation may become inactive.

Examples:

New online friendship

may later be replaced by:

Established online friendship

In such a case:

New online friendship

active = false

Established online friendship

active = true

---

### Historical Preservation

Deactivated situation states must not be deleted.

Historical states provide:

- traceability
- reproducibility
- auditability

Situation history is part of the simulation trace.

---

## Situation-State Categories

Although represented identically, different categories serve different purposes.

---

### Relationship Situation States

Represent relationship development.

Examples:

- New online friendship
- Established online friendship
- Dependency formation

These states describe relationships between actors.

---

### Manipulation Situation States

Represent manipulation-related developments.

Examples:

- Trust building
- Secrecy request
- Emotional pressure
- Coercion

These states describe harmful interaction progression.

---

### Protection Situation States

Represent protection-system evolution.

Examples:

- No relevant signals
- Ambiguous signals
- Conflicting signals
- Coordinated protection effort

These states describe the state of protective awareness and coordination.

---

## Simultaneous Situations

Multiple situation states may be active simultaneously.

The simulator does not require a single active situation.

---

### Example

Active Situation States

- Established online friendship
- Trust building
- Ambiguous signals

All three may coexist within the same World State.

---

## Situation Transition Traceability

Every active situation should be explainable through:

- previous situation state
- triggering event
- transition rule

---

### Example

SituationState

  identifier: SS-18

  type:
    Dependency formation

  activation_time:
    T27

  originating_event:
    Personal information shared

The simulator can trace:

Trust building

+

Personal information shared

=

Dependency formation

---

## Initial Situation States

Scenarios may create Situation States during initialization.

These states do not require a previous transition.

Their originating event may be:

INITIALIZATION

---

### Example

SituationState

  identifier: SS-01

  type:
    Social isolation

  activation_time:
    T0

  originating_event:
    INITIALIZATION

  active:
    true

---

## Terminal Situation States

Some situations may correspond to terminal conditions.

Examples:

- Coercion
- Coordinated protection effort

depending on simulation configuration.

Activation of a terminal situation does not automatically terminate execution.

Termination remains governed by Execution Semantics.

---

## Consistency Requirements

### Ontology Consistency

Every type value must be defined by SituationOntology.

No undefined situations may exist.

---

### Temporal Consistency

Activation time must be equal to or later than simulation initialization.

Negative timesteps are not permitted.

---

### Event Consistency

The originating event must exist in the event history.

Exception:

INITIALIZATION

used for scenario-created states.

---

### State Uniqueness

Every Situation State must possess a unique identifier.

Duplicate identifiers are not permitted.

---

### Trace Consistency

Every active situation must be derivable from:

- scenario initialization

or

- a valid situation transition

The existence of a situation must always be explainable.

---

## Example

SituationState

  identifier: SS-027

  type:
    Ambiguous signals

  activation_time:
    T18

  originating_event:
    Observation reported

  active:
    true

SituationState

  identifier: SS-028

  type:
    Trust building

  activation_time:
    T21

  originating_event:
    Repeated personal disclosure

  active:
    true