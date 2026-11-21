# StateTransitionOntology.md

## Purpose

The purpose of this ontology is to define the valid transitions between situation states.

The Situation Ontology defines:

- which situations may exist

The Event Ontology defines:

- which events may occur

The State Transition Ontology defines:

- how situations evolve
- which events may trigger transitions
- which situations may activate other situations
- which situations may terminate
- which situations may coexist

The ontology does not define:

- probabilities
- rewards
- intervention policies
- risk scores
- prediction models
- behavioural realism

The objective is not to model reality.

The objective is to define the legal transition space of the simulation environment.

This ontology acts as the authoritative source for situation evolution.

---

# Design Principles

## Ontology-Driven Evolution

World evolution must occur through explicit transitions.

A situation may only appear if:

- it is initialized by a scenario

or

- it is activated by a valid transition

No situation may emerge spontaneously.

---

## Deterministic Interpretation

A transition rule specifies a valid evolution path.

The ontology defines possibility.

The execution engine determines when a transition is applied.

This separation avoids mixing:

- ontology
- execution semantics

---

## Explicit Traceability

Every activated situation should be traceable to:

- a previous situation
- one or more events
- an explicit transition rule

This guarantees reproducibility.

---

## Scenario Independence

Transition rules must remain independent from scenarios.

A scenario defines:

- initial conditions

The transition ontology defines:

- legal future evolution

---

# Transition Pattern

All transitions follow the form:

Current Situation

+

Trigger Event

+

Optional Condition

=

New Situation

---

# Transition Components

## Current Situation

The situation currently active within the world state.

The current situation must be a valid value from SituationOntology.

---

## Trigger Event

The event that enables the transition.

The trigger event must be a valid value from EventOntology.

---

## Optional Condition

Additional requirements that must be satisfied before the transition becomes eligible.

Conditions are deterministic.

Conditions are not probabilities.

Examples:

- repeated contact exists
- previous trust established
- corroborating observation available
- intervention applied

A transition may omit this component.

---

## New Situation

The situation activated by the transition.

The resulting situation must be a valid SituationOntology value.

---

# Relationship Formation Transitions

These transitions describe the evolution of social relationships.

---

## Initial Contact

No relationship

+

Friend request accepted

=

New online friendship

---

## Relationship Stabilization

New online friendship

+

Conversation continued

+

Repeated conversations

=

Established online friendship

---

## Trust Development

Established online friendship

+

Trust-building conversation

=

Trust building

---

## Relationship Reinforcement

Trust building

+

Emotional support offered

=

Trust building

The situation remains active while additional trust-building activity occurs.

---

## Relationship Deepening

Trust building

+

Repeated personal disclosure

=

Dependency formation

---

# Information Disclosure Transitions

These transitions describe evolution related to information sharing.

---

## Initial Disclosure

Trust building

+

Personal information shared

=

Dependency formation

---

## Sensitive Disclosure

Dependency formation

+

Photo shared

=

Dependency formation

The dependency situation remains active.

---

## High-Risk Disclosure

Dependency formation

+

Location shared

=

Dependency formation

The relationship continues to deepen without introducing a new ontology state.

---

# Manipulation Transitions

These transitions describe manipulative interaction evolution.

---

## Secrecy Initiation

Trust building

+

Secrecy requested

=

Secrecy request

---

## Secrecy Reinforcement

Secrecy request

+

Secrecy agreement expressed

=

Dependency formation

---

## Compliance Escalation

Dependency formation

+

Coercive request

=

Emotional pressure

---

## Emotional Manipulation

Dependency formation

+

Emotional pressure applied

=

Emotional pressure

---

## Guilt-Based Manipulation

Dependency formation

+

Guilt induction applied

=

Emotional pressure

---

## Authority-Based Manipulation

Dependency formation

+

Authority claim made

=

Emotional pressure

---

## Coercion Escalation

Emotional pressure

+

Threat delivered

=

Coercion

---

## Blackmail Escalation

Emotional pressure

+

Blackmail attempt

=

Coercion

---

# Protection Signal Transitions

These transitions describe how protection actors become aware of concerns.

---

## Initial Observation

No relevant signals

+

Behavioural change observed

=

Ambiguous signals

---

## Activity Concern

No relevant signals

+

Increased online activity observed

=

Ambiguous signals

---

## Disclosure Concern

No relevant signals

+

Personal disclosure observed

=

Ambiguous signals

---

## Help-Seeking Concern

No relevant signals

+

Help-seeking behaviour observed

=

Ambiguous signals

---

## Child Report Signal

No relevant signals

+

Child report submitted

=

Ambiguous signals

---

## Corroboration

Ambiguous signals

+

Corroborating observation

=

Coordinated protection effort

---

## Multi-Source Escalation

Ambiguous signals

+

Parent notified

+

Teacher informed

=

Coordinated protection effort

---

## Professional Escalation

Ambiguous signals

+

Psychologist informed

=

Coordinated protection effort

---

## Signal Conflict

Ambiguous signals

+

Contradictory observation

=

Conflicting signals

---

# Intervention-Induced Transitions

These transitions are triggered by interventions rather than direct interaction events.

---

## Teacher Support Effect

Secrecy request

+

Teacher support

=

Coordinated protection effort

---

## Parent Support Effect

Secrecy request

+

Parent notification

=

Coordinated protection effort

---

## Psychologist Support Effect

Secrecy request

+

Psychologist provides support

=

Coordinated protection effort

---

## Educational Recovery

Trust building

+

Educational content delivered

=

Trust building

The existing trust situation remains active but no escalation occurs.

---

## Restriction Effect

Established online friendship

+

Contact limitation applied

=

Contact terminated

---

## Platform Restriction Effect

Dependency formation

+

Messaging restriction applied

=

Contact terminated

---

# Reporting Transitions

These transitions formalize escalation through reporting.

---

## Child Self-Reporting

Dependency formation

+

Child seeks help

=

Coordinated protection effort

---

## Trusted Adult Reporting

Secrecy request

+

Trusted adult contacted

=

Coordinated protection effort

---

## External Referral

Ambiguous signals

+

External referral initiated

=

Coordinated protection effort

---

# Situation Persistence Rules

Some situations may persist after relevant events occur.

Persistence does not create a new situation.

Persistence maintains the existing situation.

---

## Trust Persistence

Trust building

+

Compliment delivered

=

Trust building

---

## Dependency Persistence

Dependency formation

+

Conversation continued

=

Dependency formation

---

## Emotional Pressure Persistence

Emotional pressure

+

Conversation continued

=

Emotional pressure

---

# Situation Replacement Rules

Certain transitions deactivate the previous situation.

---

## Friendship Evolution

New online friendship

→

Established online friendship

The previous situation becomes inactive.

---

## Escalation Evolution

Trust building

→

Dependency formation

The previous situation becomes inactive.

---

## Manipulation Evolution

Emotional pressure

→

Coercion

The previous situation becomes inactive.

---

# Concurrent Situation Rules

Multiple situations may coexist.

---

## Example

Active situations:

- Established online friendship
- Dependency formation
- Ambiguous signals

This is valid.

Relationship situations and protection situations are not mutually exclusive.

---

## Example

Active situations:

- Emotional pressure
- Ambiguous signals
- Coordinated protection effort

This is valid.

Protection processes may occur while harmful interaction continues.

---

# Invalid Transitions

The following transitions are not permitted.

---

## Undefined Events

A transition may not reference a non-existent event.

All events must belong to EventOntology.

---

## Undefined Situations

A transition may not create a situation not defined in SituationOntology.

---

## Direct Teleportation

The simulator may not skip required situation evolution.

Example:

No relationship

+

Friend request accepted

≠

Coercion

The intermediate progression must occur through valid transitions.

---

# Terminal Situations

Terminal situations represent the end of an interaction pathway.

---

## Contact Terminated

The relationship pathway has ended.

Typical triggers:

- Contact limitation applied
- Account restricted
- Contact blocked

---

## Coercion

Represents the most severe manipulation state currently defined.

---

## Coordinated Protection Effort

Represents successful coordination among protection actors.

---

# Consistency Requirements

## Situation Consistency

Every referenced situation must exist in SituationOntology.

---

## Event Consistency

Every trigger event must exist in EventOntology.

---

## Trace Consistency

Every activated situation must be explainable through:

- scenario initialization

or

- a valid transition rule

---

## Reproducibility Requirement

Given:

- the same scenario
- the same events
- the same transition ontology

the same set of eligible state transitions must be produced.

---

## Ontology Separation Requirement

This ontology defines:

- legal transitions

This ontology does not define:

- when transitions are evaluated
- transition selection algorithms
- intervention policies
- execution order

Those responsibilities belong to execution specifications.