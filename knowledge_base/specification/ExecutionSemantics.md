# ExecutionSemantics.md

## Purpose

The purpose of this specification is to formally define how simulations execute within the Child Online Protection policy evaluation environment.

The environment contains:

- agents
- situations
- events
- observations
- interventions
- outcomes

The ontologies define the available building blocks of the environment.

The execution semantics define how those building blocks interact over time.

This document does not define:

- realism
- probabilities
- predictive validity
- causal truth
- utility functions
- reward functions
- machine learning algorithms
- optimization objectives

The goal is not to reproduce reality.

The goal is to provide a configurable, auditable, and reproducible environment in which alternative policy configurations can be evaluated under identical conditions. 

---

# Core Execution Principles

## Explicit State Principle

Every simulation-relevant element must be explicitly represented.

The simulator must not rely on hidden assumptions.

Information affecting execution must appear in one of the following forms:

- agent attributes
- situations
- events
- observations
- interventions
- outcomes

All state changes must be observable within the execution trace.

---

## Reproducibility Principle

Two executions using:

- the same scenario
- the same agents
- the same policies
- the same configuration
- the same random seed (if randomness exists)

must produce the same trace.

Reproducibility is considered a first-class requirement.

The simulation trace is the authoritative record of the execution.

---

## Ontology-Constrained Evolution Principle

The simulator may only create:

- situations defined by SituationOntology
- events defined by EventOntology
- observations defined by ObservationOntology
- interventions defined by InterventionOntology
- outcomes defined by OutcomeOntology

The execution engine cannot invent additional concepts during runtime. 

---

## Information Asymmetry Principle

Agents do not possess omniscient knowledge.

Every agent can only observe information explicitly permitted by the Visibility Ontology.

Consequently:

- different agents may hold different beliefs
- observations may be incomplete
- interventions may be based on partial information
- coordination may fail

Information asymmetry is a deliberate property of the environment. 

---

# Simulation State

## World State

At every timestep the environment contains a World State.

The World State is composed of:

### Agent State

The instantiated agents participating in the simulation.

Examples:

- Child
- ThreatActor
- ParentUnit
- Teacher
- Psychologist
- Platform
- ProtectionSystem

Each agent maintains its own configuration as defined by its specification. 

---

### Situation State

The collection of all currently active situations.

Examples:

- Social isolation
- New online friendship
- Trust building
- Secrecy request
- Ambiguous signals
- Coordinated protection effort

Multiple situations may simultaneously exist. 

---

### Event History

The ordered sequence of events generated since simulation start.

Events are immutable.

Once generated they remain part of the execution record. 

---

### Observation History

The ordered sequence of observations generated during execution.

Observation history provides the perceptual record available to actors. 

---

### Intervention History

The ordered sequence of interventions applied during the simulation.

Interventions become permanent trace elements. 

---

# Simulation Clock

## Discrete Time

Execution progresses through discrete timesteps.

Examples:

- T0
- T1
- T2
- T3
- T4

A timestep represents ordering.

A timestep is not required to correspond to:

- minutes
- hours
- days
- weeks

Different implementations may interpret timesteps differently.

---

## Simulation Horizon

Every scenario defines a maximum execution length.

Examples:

- 40 turns
- 50 turns

Execution terminates when the horizon is reached unless an earlier terminal condition occurs. 

---

# Initialization Semantics

## Scenario Loading

Execution begins by loading a scenario.

The scenario provides:

- participating agents
- initial situations
- constraints

The scenario defines the starting world state. 

---

## Agent Instantiation

Each participating actor is instantiated using its corresponding agent specification.

Examples:

Child instances are instantiated from ChildAgent.

Teacher instances are instantiated from TeacherAgent.

Protection systems are instantiated from ProtectionSystemAgent.

The agent specifications define the attributes available to the instantiated agent. 

---

## Initial Situation Activation

The simulator activates all situations declared by the scenario.

Examples:

- Social isolation
- No relevant signals
- No relationship

These situations become active before any event generation occurs. 

---

# Simulation Loop

At each timestep the following execution cycle is performed.

---

## Step 1: Actor Evaluation

Every participating actor evaluates the current world state.

Actor evaluation is local.

An actor may only evaluate:

- its own configuration
- visible observations
- active situations
- historical information available to that actor

Visibility restrictions remain in effect. 

---

## Step 2: Action Generation

Actors generate candidate actions.

Examples include:

Child:

- share information
- report concerns
- seek help
- block contacts

ThreatActor:

- initiate contact
- build trust
- request information
- request secrecy

Platform:

- show warning
- review account
- restrict account

ProtectionSystem:

- perform assessment
- recommend intervention
- initiate escalation

The simulator may generate multiple candidate actions simultaneously. 

---

## Step 3: Event Construction

Candidate actions are translated into ontology-compliant events.

Examples:

Actor Action

"request age"

becomes

Event

Age shared

or

Personal information requested

depending on context.

Only valid Event Ontology values may be emitted. 

---

## Step 4: Constraint Validation

Generated events are validated.

The simulator verifies:

- scenario constraints
- visibility constraints
- relationship constraints
- termination constraints

Examples:

A conversation cannot continue if no contact exists.

A blocked contact cannot continue messaging.

A teacher cannot observe private conversations directly.

Invalid events are rejected. 

---

## Step 5: Event Commitment

Validated events become part of the official trace.

Committed events are added to:

- event history
- execution log
- future reasoning context

Committed events cannot be removed.

---

## Step 6: Situation Transition Evaluation

The simulator evaluates whether newly committed events trigger situation transitions.

Transitions are defined exclusively by the transition ontology.

Examples:

No relationship

+

Friend request accepted

=

New online friendship

Trust building

+

Secrecy requested

=

Secrecy request

Emotional pressure

+

Threat delivered

=

Coercion

Situation transitions modify the active situation set. 

---

## Step 7: Observation Generation

Actors observe the consequences of events.

Observability is controlled by the Visibility Ontology.

Examples:

The Child may observe:

- warnings
- conversations
- secrecy requests

The ParentUnit may observe:

- notifications
- disclosures
- behavioural changes

The Teacher may observe:

- help-seeking behaviour
- behavioural changes

The Platform may observe:

- uploaded content
- conversations
- reports

The ProtectionSystem may observe:

- reports
- platform signals
- escalation information

Observation generation is therefore actor-dependent. 

---

## Step 8: Observation Recording

Generated observations become formal observation records.

Observation records include:

- observer
- observed event
- timestamp
- context

Observation records are immutable once committed.

---

## Step 9: Risk Assessment Activity

Actors capable of assessment may perform internal evaluations.

Examples:

- Platform moderation systems
- ProtectionSystem
- Teachers
- Parents
- Psychologists

Assessment activities are internal reasoning processes.

The execution semantics require only that resulting actions become visible through events or interventions.

Internal reasoning is not required to be represented. 

---

## Step 10: Intervention Selection

Actors may select interventions based on available observations.

Interventions must belong to the Intervention Ontology.

Possible interventions include:

Educational:

- Educational content
- Privacy reminder

Support:

- Talk to trusted adult
- Teacher support

Escalation:

- Parent notification
- School notification

Restriction:

- Temporary restriction
- Contact limitation

Intervention selection remains policy-dependent. 

---

## Step 11: Intervention Application

Selected interventions are applied.

Applied interventions become part of intervention history.

Interventions may generate further events.

Example:

Parent notification

may create:

Parent notified

Example:

Contact limitation

may create:

Contact limitation applied

Interventions therefore influence subsequent execution cycles. 

---

## Step 12: State Consolidation

At the end of each timestep the simulator updates:

- active situations
- active restrictions
- intervention effects
- available communication channels
- historical records

The resulting state becomes the starting state of the next timestep.

---

# Information Propagation Semantics

## Direct Visibility

Information becomes available immediately to eligible observers.

Example:

A warning shown to the child becomes visible to:

- Child
- Platform

but not automatically to:

- ParentUnit
- Teacher

unless additional events occur. 

---

## Escalated Visibility

Certain events increase visibility.

Examples:

- Parent notified
- Teacher informed
- Psychologist informed

Escalation expands the set of actors with access to relevant information. 

---

## Restricted Information

Some information remains private.

Examples:

- internal moderation reasoning
- platform detection outputs
- protection-system deliberation

Such information may influence actions without becoming observable to other agents. 

---

# Terminal Conditions

## Natural Termination

Execution terminates when the simulation horizon is reached. 

---

## Situation-Based Termination

Execution may terminate when a terminal interaction state is reached.

Examples:

- Contact terminated
- Coercion
- Coordinated protection effort
- No further interaction

These states are defined by the Interaction Ontology. 

---

## Policy-Based Termination

Implementations may define additional stopping rules.

Such rules must be explicitly declared.

Hidden termination conditions are not permitted.

---

# Outcome Determination

## Outcome Extraction

Upon termination the simulator derives outcomes from:

- final world state
- situation history
- event history
- observation history
- intervention history

Outcome generation occurs after execution completes. 

---

## Outcome Categories

Outcomes may include:

### Interaction Outcomes

- Contact established
- Contact maintained
- Contact terminated

### Information Outcomes

- Limited personal information disclosed
- Extensive personal information disclosed

### Support Outcomes

- Parent involved
- Teacher involved
- Multiple adults involved

### Protection Outcomes

- Educational intervention
- Escalation intervention
- Restriction intervention

### Interaction-State Outcomes

- Trust building reached
- Dependency formation reached
- Coercion reached

### System Outcomes

- Single actor observed signals
- Multiple actors observed signals
- Coordinated protection effort achieved

Outcomes describe what happened.

They do not indicate whether the result was good or bad. 

---

# Trace Completeness Requirements

Every simulation execution must generate a complete execution trace.

The trace must contain:

- simulation identifier
- scenario identifier
- participating agents
- initial situations
- timestep sequence
- event sequence
- observation sequence
- intervention sequence
- situation evolution
- final outcomes

A trace missing any of these elements is considered invalid.

The trace serves as the primary artifact used for policy comparison, auditing, and reproducibility analysis. 