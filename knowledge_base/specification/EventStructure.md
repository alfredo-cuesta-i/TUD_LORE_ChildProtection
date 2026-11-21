# EventStructure.md

## Purpose

Defines the canonical representation of an event within the simulation.

The Event Ontology defines which event types may occur.

This specification defines how individual event instances are represented during a simulation run.

An event is the smallest observable unit of world evolution.

Every event in the simulation must conform to the structure defined below.

## Event Structure

```text
Event
  identifier
  type
  actor
  target
  channel
  timestamp
  context
```

## Fields

### identifier

Unique event identifier.

Example:

```text
E-001
```

### type

Event category.

Must be a valid value from EventOntology.

Examples:

```text
Friend request sent
Personal information shared
Educational content delivered
Parent notified
```

### actor

Agent initiating the event.

Possible values:

```text
Child
ThreatActor
ParentUnit
Teacher
Psychologist
Platform
ProtectionSystem
```

### target

Agent affected by the event.

Possible values:

```text
Child
ThreatActor
ParentUnit
Teacher
Psychologist
Platform
ProtectionSystem
```

Multiple targets are permitted.

Example:

```text
Child + ParentUnit
```

### channel

Location or communication medium where the event occurs.

Possible values are defined by EventOntology.

Examples:

```text
Direct Message
Group Chat
Gaming Chat
Platform Notification
School Meeting
```

### timestamp

Discrete simulation time.

Examples:

```text
T1
T2
T3
...
```

The simulation does not require real-world dates or clocks.

### context

Optional structured information associated with the event.

Examples:

```text
information_type = school_name
```

```text
relationship_context = online_acquaintance
```

```text
warning_type = privacy_reminder
```

Context values should be selected from the context categories defined in EventOntology.

## Example

```text
Event
  identifier: E17
  type: Personal information shared
  actor: Child
  target: ThreatActor
  channel: Direct Message
  timestamp: T8
  context:
    information_type = school_name
```