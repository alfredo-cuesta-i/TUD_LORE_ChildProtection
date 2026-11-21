# WorldStateStructure.md

## Purpose

Defines the canonical representation of the World State.

The World State is the complete description of everything that exists within the simulation at a particular timestep.

The World State acts as the authoritative snapshot of the environment.

At any point during execution, the complete simulation must be reconstructable from the World State and its preceding history.

The Event Ontology defines which events may occur.

The Situation Ontology defines which situations may exist.

The Observation Ontology defines which observations may be generated.

The Intervention Ontology defines which interventions may be applied.

The Visibility Ontology defines which information may be observed by which actors.

The State Transition Ontology defines how situations evolve.

The World State structure defines how all of those elements coexist at runtime.

The World State does not define:

- probabilities
- rewards
- utility functions
- causal certainty
- intervention policies
- prediction systems
- decision-making algorithms
- psychological realism

The objective of the World State is to provide a complete, auditable, deterministic, and reproducible representation of the simulation environment at a particular timestep.

---

## Design Principles

### Completeness

Every element required to explain the current simulation state must be represented explicitly.

Nothing relevant should exist outside the World State.

---

### Determinism

The same inputs must produce the same World State.

A World State must never depend on hidden information.

---

### Reproducibility

A researcher should be able to reproduce a simulation run by combining:

- scenario definition
- agent configurations
- policy configuration
- execution semantics
- sequence of World States

---

### Traceability

Every state element should be explainable through:

- initialization
- events
- transitions
- observations
- interventions

No unexplained state changes are permitted.

---

## World State Structure

WorldState

  identifier

  timestamp

  active_agents

  active_situations

  active_relationships

  active_interactions

  active_restrictions

  observations

  interventions

  visibility_state

  event_history

  metadata

---

# Fields

## identifier

Unique World State identifier.

Each state snapshot may receive a distinct identifier.

Examples:

WS-00001

WS-00017

WS-00492

The identifier refers to the snapshot itself rather than the simulation.

---

## timestamp

Current simulation timestep.

Examples:

T0

T1

T17

T50

T120

The timestamp indicates when the snapshot was taken.

The timestamp does not correspond to real-world time.

The simulator may interpret timesteps differently depending on configuration.

---

# active_agents

Contains all currently instantiated agents.

Agents are instantiated from their respective specifications.

Possible agent types include:

- Child
- ThreatActor
- ParentUnit
- Teacher
- Psychologist
- Platform
- ProtectionSystem

The World State references the active instances.

Agent attributes remain stored within their corresponding agent definitions.

---

## Agent Structure

AgentReference

  identifier

  type

  active

---

### identifier

Unique agent identifier.

Examples:

Child-001

Teacher-001

ThreatActor-001

---

### type

Possible values:

- Child
- ThreatActor
- ParentUnit
- Teacher
- Psychologist
- Platform
- ProtectionSystem

---

### active

Possible values:

- true
- false

---

## Example

active_agents

- Child-001
- ThreatActor-001
- ParentUnit-001
- Platform-001

---

# active_situations

Contains all situation states currently active within the simulation.

Situation values must originate from SituationOntology.

Examples:

- Social isolation
- New online friendship
- Established online friendship
- Trust building
- Dependency formation
- Secrecy request
- Emotional pressure
- Coercion
- Ambiguous signals
- Coordinated protection effort

Multiple active situations may coexist.

---

## Situation Representation

The active_situations field should reference SituationState instances.

Examples:

- SS-01
- SS-12
- SS-19

The complete structure of situation instances is defined in SituationStateStructure.

---

## Example

active_situations

- Established online friendship

- Trust building

- Ambiguous signals

---

# active_relationships

Represents relationships currently existing between agents.

Relationships provide context for:

- conversation eligibility
- event generation
- transition evaluation
- intervention application

Relationships may exist even when no interaction is occurring.

---

## Relationship Structure

Relationship

  identifier

  source_agent

  target_agent

  relationship_type

  status

  creation_timestamp

---

### identifier

Examples:

R-001

R-014

R-102

---

### source_agent

Agent initiating or originating the relationship.

Example:

Child-001

---

### target_agent

Other participant.

Example:

ThreatActor-001

---

### relationship_type

Examples:

- complete stranger
- online acquaintance
- gaming teammate
- social media follower
- friend of friend
- established online friendship

---

### status

Possible values:

- active
- suspended
- restricted
- terminated

---

### creation_timestamp

Timestep at which the relationship was created.

Example:

T4

---

## Example

Relationship

  identifier: R-018

  source_agent: Child-001

  target_agent: ThreatActor-001

  relationship_type:
    online acquaintance

  status:
    active

  creation_timestamp:
    T4

---

# active_interactions

Represents interactions currently taking place.

An interaction is more temporary than a relationship.

A relationship may remain active without an active interaction.

---

## Examples

- active conversation
- friend request exchange
- disclosure sequence
- support process
- escalation process
- educational delivery

---

## Interaction Structure

Interaction

  identifier

  participants

  interaction_type

  channel

  status

  started_at

---

### identifier

Examples:

INT-01

INT-27

INT-104

---

### participants

Participating agents.

Examples:

- Child-001
- ThreatActor-001

---

### interaction_type

Examples:

- conversation
- support
- reporting
- escalation
- educational delivery

---

### channel

Must be a valid communication channel.

Examples:

- Direct Message
- Group Chat
- Voice Chat
- Video Call
- Platform Notification
- School Meeting
- Email

---

### status

Possible values:

- active
- paused
- restricted
- completed

---

### started_at

Timestep at which the interaction began.

Example:

T8

---

# active_restrictions

Represents restrictions currently affecting simulation behaviour.

Restrictions influence:

- visibility
- event generation
- communication
- intervention availability
- relationship evolution

---

## Origin Sources

Restrictions may originate from:

- Platform
- ParentUnit
- Teacher
- ProtectionSystem

---

## Restriction Structure

Restriction

  identifier

  type

  target

  initiator

  created_at

  expires_at

---

### type

Examples:

- Contact limitation
- Messaging restriction
- Temporary restriction
- Account access limitation
- Location sharing disabled

---

### target

Restricted entity.

Example:

ThreatActor-001

---

### initiator

Originating actor.

Examples:

- Platform-001
- ParentUnit-001
- ProtectionSystem-001

---

## Example

Restriction

  identifier: REST-05

  type:
    Messaging restriction

  target:
    ThreatActor-001

  initiator:
    Platform-001

  created_at:
    T21

---

# observations

Contains observations currently available within the world.

Observations result from visibility resolution.

Different actors may possess different observations.

The simulator does not assume perfect knowledge.

---

## Observation Structure

Observation

  identifier

  observer

  observation_type

  source_event

  timestamp

---

### observer

Agent possessing the observation.

Examples:

- Teacher-001
- ParentUnit-001
- ProtectionSystem-001

---

### observation_type

Valid values:

- Observes behavioural change
- Observes increased online activity
- Observes disclosure of personal information
- Observes help-seeking behaviour
- No relevant observation

---

### source_event

Event that generated the observation.

Example:

Behavioural change observed

---

## Example

Observation

  identifier: O-19

  observer:
    Teacher-001

  observation_type:
    Observes behavioural change

  source_event:
    Behavioural change observed

  timestamp:
    T17

---

# interventions

Represents interventions currently active within the World State.

Historical interventions remain recorded separately.

This field tracks interventions whose effects remain active.

---

## Active Intervention Structure

ActiveIntervention

  identifier

  type

  initiator

  target

  applied_at

  status

---

### status

Possible values:

- active
- completed
- cancelled
- expired

---

## Example

ActiveIntervention

  identifier: I-07

  type:
    Parent notification

  initiator:
    ProtectionSystem

  target:
    ParentUnit

  applied_at:
    T11

  status:
    active

---

# visibility_state

Represents current information accessibility.

Visibility defines who may observe what.

The visibility state is derived from:

- VisibilityOntology
- active relationships
- active interventions
- escalation history
- restrictions
- communication pathways

---

## Visibility Structure

Visibility

  information_item

  visible_to

  visibility_level

---

### information_item

Observed resource.

Examples:

- Parent notified
- Child report submitted
- Risk assessment performed

---

### visible_to

Agents allowed to access the information.

---

### visibility_level

Possible values:

- public
- local
- restricted
- private

---

## Example

Visibility

  information_item:
    Parent notified

  visible_to:

    - ParentUnit
    - ProtectionSystem

  visibility_level:
    restricted

---

# event_history

Contains all events that have occurred up to the current timestep.

Event history is cumulative.

Events are immutable.

Events cannot be removed.

---

## Event History Structure

EventHistory

  event_identifier

  event_type

  participants

  timestamp

  context

---

### event_identifier

Examples:

E-01

E-91

E-302

---

### event_type

Must be a valid EventOntology value.

Example:

Personal information shared

---

### participants

Entities involved in the event.

---

### context

Optional contextual information associated with the event.

Examples:

- communication channel
- disclosure category
- escalation type

---

## Example

EventHistory

  event_identifier: E-91

  event_type:
    Personal information shared

  participants:

    - Child
    - ThreatActor

  timestamp:
    T14

---

# metadata

Contains implementation-independent simulation information.

Metadata exists solely for:

- auditing
- reproducibility
- trace reconstruction

---

## Metadata Structure

Metadata

  scenario_identifier

  random_seed

  simulation_identifier

  policy_identifier

  engine_version

---

### scenario_identifier

Scenario that initialized the simulation.

Example:

S-004

---

### random_seed

Optional deterministic seed.

Example:

123456789

---

### simulation_identifier

Unique simulation identifier.

Example:

SIM-2026-001

---

### policy_identifier

Policy set used during execution.

Examples:

POLICY-PARENT-FIRST

POLICY-EDUCATION-FIRST

POLICY-PLATFORM-MODERATION

---

### engine_version

Simulation engine version.

Example:

v1.3

---

# World State Lifecycle

## Creation

The initial World State is created from scenario initialization.

Usually:

timestamp = T0

---

## Evolution

World States evolve through:

- events
- observations
- interventions
- restrictions
- state transitions

---

## Historical Preservation

Previous World States should remain accessible.

Historical states support:

- auditing
- reproducibility
- causal analysis
- policy comparison

---

# Consistency Requirements

## Situation Consistency

Every active situation must be defined by SituationOntology.

---

## Event Consistency

Every recorded event must be defined by EventOntology.

---

## Observation Consistency

Every observation must be defined by ObservationOntology.

---

## Intervention Consistency

Every intervention must be defined by InterventionOntology.

---

## Visibility Consistency

No visibility assignment may violate VisibilityOntology.

---

## Agent Consistency

Every active agent must be instantiated from an approved agent specification.

---

## Trace Consistency

Every World State must be derivable from:

- previous World State
- valid events
- valid observations
- valid interventions
- valid situation transitions

---

## Reproducibility Consistency

Given:

- same scenario
- same policy
- same seed
- same execution rules

the same World State sequence must be produced.

---

# Example

WorldState

  identifier: WS-014

  timestamp: T14

  active_agents:

    - Child-001
    - ThreatActor-001
    - ParentUnit-001
    - Teacher-001
    - Platform-001

  active_situations:

    - Established online friendship
    - Trust building

  active_relationships:

    - R-003

  active_interactions:

    - INT-01

  active_restrictions:

    - none

  observations:

    - O-12
    - O-13

  interventions:

    - I-04

  visibility_state:

    - VIS-01
    - VIS-02

  event_history:

    - E-01
    - E-02
    - E-03
    - E-04

  metadata:

    scenario_identifier:
      S-004

    simulation_identifier:
      SIM-004