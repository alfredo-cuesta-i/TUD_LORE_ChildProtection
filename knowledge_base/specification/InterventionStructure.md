# InterventionStructure.md

## Purpose

Defines the canonical representation of interventions.

Interventions are actions intended to influence the evolution of the simulation after observations or assessments occur.

The Intervention Ontology defines which intervention types are available.

This specification defines how interventions are represented.

## Intervention Structure

```text
Intervention
  identifier
  type
  initiator
  target
  timestamp
  rationale
  context
```

## Fields

### identifier

Unique intervention identifier.

Example:

```text
I-001
```

### type

Intervention type.

Must be a valid value from InterventionOntology.

Examples:

```text
Educational content
Privacy reminder
Teacher support
Parent notification
Temporary restriction
```

### initiator

Entity applying the intervention.

Possible values:

```text
ParentUnit
Teacher
Psychologist
Platform
ProtectionSystem
```

### target

Recipient of the intervention.

Examples:

```text
Child
ThreatActor
ParentUnit
Teacher
```

### timestamp

Simulation timestep.

Example:

```text
T15
```

### rationale

Reason that motivated the intervention.

Examples:

```text
Behavioural change observed
Repeated disclosure observed
Parent request received
Risk assessment performed
```

### context

Optional intervention-specific information.

Examples:

```text
severity = moderate
```

```text
escalation_level = teacher
```

## Example

```text
Intervention
  identifier: I04
  type: Parent notification
  initiator: ProtectionSystem
  target: ParentUnit
  timestamp: T11
  rationale: Repeated disclosure observed
```