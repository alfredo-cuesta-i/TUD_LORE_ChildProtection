# StateTransitionOntology.md

## Purpose

Defines all legal state transitions inside the simulation.

This ontology is the authoritative source describing how situations may change in response to events, observations, or interventions.

Unlike agent profiles, it does not describe actors.

Unlike scenarios, it does not describe initial conditions.

Its only purpose is to define legal evolution paths inside the synthetic environment.

The ontology does not define:

- probabilities
- rewards
- risk scores
- utility functions
- realism assumptions

A transition may only occur when explicitly defined below.

---

## Transition Structure

current_situation
+
trigger
=
new_situation

---

## Relationship State Transitions

No relationship
+
Friend request accepted
=
New online friendship

New online friendship
+
Conversation continued
=
Established online friendship

Established online friendship
+
Personal information shared
=
Trust building

Established online friendship
+
Trust-building conversation
=
Trust building

---

## Manipulation State Transitions

Trust building
+
Secrecy requested
=
Secrecy request

Trust building
+
Dependency-building interaction
=
Dependency formation

Trust building
+
Personal information shared
=
Dependency formation

Secrecy request
+
Secrecy agreement expressed
=
Dependency formation

Dependency formation
+
Emotional pressure applied
=
Emotional pressure

Emotional pressure
+
Threat delivered
=
Coercion

Emotional pressure
+
Blackmail attempt
=
Coercion

Emotional pressure
+
Coercive request
=
Coercion

---

## Protection State Transitions

No relevant signals
+
Observation reported
=
Ambiguous signals

Ambiguous signals
+
Corroborating observation
=
Coordinated protection effort

Ambiguous signals
+
Contradictory observation
=
Conflicting signals

Conflicting signals
+
Corroborating observation
=
Coordinated protection effort

Conflicting signals
+
Additional contradictory observation
=
Conflicting signals

---

## Intervention State Transitions

Secrecy request
+
Teacher support
=
Coordinated protection effort

Secrecy request
+
Parent notification
=
Coordinated protection effort

Ambiguous signals
+
Teacher support
=
Coordinated protection effort

Ambiguous signals
+
Parent notification
=
Coordinated protection effort

Ambiguous signals
+
School notification
=
Coordinated protection effort

Dependency formation
+
Teacher support
=
Coordinated protection effort

Dependency formation
+
Parent notification
=
Coordinated protection effort

Established online friendship
+
Contact limitation
=
Contact terminated

Trust building
+
Contact limitation
=
Contact terminated

Dependency formation
+
Contact limitation
=
Contact terminated

Secrecy request
+
Contact limitation
=
Contact terminated

---

## Terminal States

Contact terminated

Coercion

Coordinated protection effort

No further transitions may occur after a terminal state is reached.