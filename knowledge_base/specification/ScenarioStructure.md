# ScenarioStructure.md

## Purpose

Defines the canonical structure of scenario files.

A scenario specifies the initial conditions of a simulation before any events occur.

Different scenarios allow policies to be evaluated under different conditions.

## Scenario Structure

```text
Scenario
  identifier
  name
  description
  agents
  initial_situations
  constraints
```

## Fields

### identifier

Unique scenario identifier.

Example:

```text
S-001
```

### name

Human-readable scenario name.

Examples:

```text
Lonely Teen
Cyberbullying Case
Misinformation Case
Grooming Attempt
```

### description

Brief description of the scenario objective.

### agents

Initial agent configuration.

May include:

```text
Child
ThreatActor
ParentUnit
Teacher
Psychologist
Platform
ProtectionSystem
```

Each agent is instantiated from its corresponding specification.

### initial_situations

Starting situations.

Must be selected from SituationOntology.

Examples:

```text
No relevant signals
Social isolation
New online friendship
```

### constraints

Optional conditions restricting simulation evolution.

Examples:

```text
Parent unavailable
No platform moderation
No teacher involvement
```

## Example

```text
Scenario
  identifier: S-004
  name: Grooming Attempt
  description: Child is approached by an unknown online contact.
  agents:
    Child
    ThreatActor
    ParentUnit
    Platform
    ProtectionSystem
  initial_situations:
    Social isolation
    No relevant signals
```