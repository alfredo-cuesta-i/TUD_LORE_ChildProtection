# ObservationGenerationRules.md

## Purpose

Defines when an observation object is created.

The Visibility Ontology defines who may observe information.

This document defines when an observation is formally recorded.

An observation is generated only when:

1. an observable event occurs
2. the observing actor is allowed to see it
3. the event falls within the observation ontology

---

## Observation Structure

An observation object is created when:

observer
+
observable_event
+
visibility_permission
=
observation

---

## Disclosure Observations

Create:

Observes disclosure of personal information

when one of the following events occurs:

- Personal information shared
- Name shared
- Age shared
- School shared
- Location shared
- Contact information shared
- Photo shared
- Video shared
- Live image shared

and the observer is permitted by the Visibility Ontology.

---

## Help-Seeking Observations

Create:

Observes help-seeking behaviour

when one of the following events occurs:

- Child seeks help
- Child report submitted
- Trusted adult contacted

and the observer is permitted by the Visibility Ontology.

---

## Behavioural Change Observations

Create:

Observes behavioural change

when:

- Behavioural change observed

and the observer is permitted by the Visibility Ontology.

---

## Increased Online Activity Observations

Create:

Observes increased online activity

when:

- Increased online activity observed

and the observer is permitted by the Visibility Ontology.

---

## Observation Reporting

Whenever an observation object is created:

Observation reported

is generated for the protection state transition system.

This allows:

No relevant signals
+
Observation reported
=
Ambiguous signals

---

## No Observation Case

If:

- the event is not visible to the actor

or

- the event does not correspond to an observation type

then:

No relevant observation

is recorded.

---

## Visibility Constraint

Observation creation never overrides the Visibility Ontology.

Actors may only generate observations from information they are permitted to observe.