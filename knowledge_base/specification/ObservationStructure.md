# ObservationStructure.md

## Purpose

Defines the canonical representation of observations.

The Event Ontology defines which events may occur.

The Visibility Ontology defines which actors may observe which information.

The Observation Ontology defines the types of observations that may exist.

This specification defines how observations are represented within the simulation.

An observation represents information that has become available to a particular observer.

Observations are not events.

Events occur in the world.

Observations represent an actor becoming aware of information about the world.

Different actors may observe different information even when exposed to the same environment.

This specification does not define:

- probabilities
- reasoning processes
- intervention policies
- risk scores
- psychological interpretations
- causal inference

The purpose of the Observation Structure is to provide a deterministic and reproducible representation of information acquisition.

---

## Relationship With Other Specifications

EventOntology defines:

- which events may occur

VisibilityOntology defines:

- which actors may observe which information

ObservationOntology defines:

- valid observation categories

VisibilityResolutionRules defines:

- when observations are generated

WorldStateStructure stores:

- active observations

This specification defines:

- the representation of observation instances

---

## Observation Structure

Observation

  identifier

  observer

  observation_type

  source_event

  timestamp

  visibility_basis

---

# Fields

## identifier

Unique observation identifier.

Every observation instance must have a unique identifier.

Examples:

O-001

O-015

O-208

The identifier refers to the observation instance itself.

It does not refer to the event being observed.

---

## observer

Actor that possesses the observation.

The observer is the entity that became aware of information.

Possible values:

- Child
- ThreatActor
- ParentUnit
- Teacher
- Psychologist
- Platform
- ProtectionSystem

The observer must correspond to a valid simulation actor.

---

### Example

Observation

  identifier: O-12

  observer:
    Teacher

---

## observation_type

Observation category.

The value must be selected from ObservationOntology.

Only valid ontology values are permitted.

---

### Possible Values

- Observes behavioural change
- Observes increased online activity
- Observes disclosure of personal information
- Observes help-seeking behaviour
- No relevant observation

---

### Consistency Requirement

Observation types outside the Observation Ontology are not permitted.

---

### Example

Observation

  observation_type:
    Observes behavioural change

---

## source_event

Event that caused the observation.

Observations must be traceable to observable events.

The source event must originate from EventOntology.

Examples:

- Behavioural change observed
- Personal disclosure observed
- Help-seeking behaviour observed
- Child report submitted
- Parent notified

The source event explains why the observation exists.

---

### Purpose

The source event provides:

- traceability
- explainability
- reproducibility

Researchers should always be able to identify which event generated an observation.

---

### Example

Observation

  source_event:
    Personal disclosure observed

---

## timestamp

Simulation timestep at which the observation was generated.

Examples:

T0

T8

T21

T49

The timestamp records when the observer became aware of the information.

The timestamp is not necessarily identical to the event timestamp.

An observation may occur after the underlying event.

---

### Example

Observation

  timestamp:
    T13

---

## visibility_basis

Records why the observation was permitted.

Observations should always be explainable through visibility rules.

The visibility basis identifies the rule, condition, or mechanism that enabled observation generation.

---

### Possible Sources

Examples include:

- direct visibility
- local interaction participation
- parent notification
- teacher informed
- psychologist informed
- platform moderation access
- active monitoring
- reporting event
- visibility escalation
- scenario-enabled visibility

---

### Purpose

Visibility basis improves:

- auditability
- explainability
- reproducibility

Researchers can determine:

- why an observation exists
- how it became visible
- whether visibility policies affected the outcome

---

### Example

Observation

  visibility_basis:
    teacher informed

---

# Observation Lifecycle

## Observation Creation

Observations are generated when:

- a visible artefact exists
- visibility conditions are satisfied
- observation generation is permitted

Observation generation follows the Visibility Ontology and Visibility Resolution Rules.

---

## Observation Persistence

Once generated, observations become part of simulation history.

Observations should not disappear from historical records.

Persistent observation history supports:

- auditing
- intervention analysis
- trace reconstruction

---

## Observation Consumption

Observations may later be used by:

- ParentUnit
- Teacher
- Psychologist
- Platform
- ProtectionSystem

to support intervention decisions.

Observation existence does not require intervention.

An observation may simply remain recorded.

---

# Observer Categories

Different observers have access to different information.

---

## Child Observations

Examples:

- warnings received
- conversations
- secrecy requests
- educational content

The Child cannot directly observe internal protection-system reasoning.

---

## ThreatActor Observations

Examples:

- child responses
- child disclosures
- child blocking actions

The ThreatActor cannot directly observe protection decisions.

---

## ParentUnit Observations

Examples:

- parent notifications
- child disclosures
- behavioural changes

Some observations require enabling conditions such as monitoring.

---

## Teacher Observations

Examples:

- behavioural changes
- help-seeking behaviour
- school-related disclosures

Teachers do not directly observe private conversations.

---

## Psychologist Observations

Examples:

- case reports
- parent reports
- teacher reports
- intervention history

Psychologists generally observe indirectly through information sharing.

---

## Platform Observations

Examples:

- conversations
- uploaded content
- reports
- disclosure activity

Platform observations depend on platform capabilities.

---

## ProtectionSystem Observations

Examples:

- parent reports
- teacher reports
- platform signals
- child reports

The Protection System relies on configured information channels.

---

# Observation Sources

An observation may originate from several types of artefacts.

---

## Event-Derived Observations

Generated from events.

Examples:

- Child report submitted
- Behavioural change observed
- Parent notified

---

## Situation-Derived Observations

Generated from active situations.

Examples:

- Trust building
- Ambiguous signals
- Emotional pressure

An actor may observe evidence indicating a situation exists.

---

## Intervention-Derived Observations

Generated from interventions.

Examples:

- Educational content delivered
- Parent notification
- Teacher support

---

## Observation-Derived Observations

A previously generated observation may be communicated to another actor.

Examples:

Teacher observation

→ Parent communication

→ Parent observation

The new observation remains separately represented.

---

# Visibility Dependencies

Every observation must satisfy visibility constraints.

---

## Direct Visibility

Observation generated because the observer directly witnessed the event.

Example:

Child sees a warning.

---

## Conditional Visibility

Observation generated because enabling conditions exist.

Example:

Parent observes online activity because monitoring is enabled.

---

## Escalated Visibility

Observation generated because an escalation event occurred.

Examples:

- Parent notified
- Teacher informed
- Psychologist informed

---

## Restricted Visibility

Observation generated only after authorized information sharing.

Examples:

- case reports
- professional referrals
- protection-system notifications

---

# Consistency Requirements

## Observer Consistency

The observer must correspond to a valid simulation actor.

---

## Observation Type Consistency

Every observation type must be defined by ObservationOntology.

Invalid observation types are not permitted.

---

## Event Consistency

The source event must exist within simulation history.

---

## Visibility Consistency

The observation must be permitted by the Visibility Ontology.

Observations violating visibility rules are invalid.

---

## Temporal Consistency

Observation timestamps cannot occur before simulation initialization.

Observation timestamps cannot occur before the source event.

---

## Trace Consistency

Every observation must be explainable through:

- a source event

and

- a valid visibility basis

Observations must never appear without explanation.

---

## Reproducibility Consistency

Given:

- identical world state
- identical visibility rules
- identical events

the same observations must be generated.

---

# Example

Observation

  identifier: O-19

  observer:
    Teacher

  observation_type:
    Observes behavioural change

  source_event:
    Behavioural change observed

  timestamp:
    T17

  visibility_basis:
    direct visibility

Observation

  identifier: O-20

  observer:
    ParentUnit

  observation_type:
    Observes increased online activity

  source_event:
    Increased online activity observed

  timestamp:
    T18

  visibility_basis:
    active monitoring