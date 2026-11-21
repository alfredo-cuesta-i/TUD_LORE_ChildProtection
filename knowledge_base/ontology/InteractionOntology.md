# InteractionOntology.md

## Purpose

The purpose of this ontology is not to model reality.

Its purpose is to describe how situations may evolve inside the synthetic environment through the occurrence of events and agent actions.

The ontology defines possible transitions.

It does not define probabilities.

It does not define rewards.

It does not define risk scores.

It only defines permissible world evolution paths.

---

## Transition Pattern

```
current_situation
+
event
+
optional_condition
=
new_situation
```

---

## Relationship Transitions

```
No relationship
+
Friend request accepted
=
New online friendship
```

```
New online friendship
+
Repeated conversations
=
Established online friendship
```

```
Established online friendship
+
Repeated personal disclosure
=
Trust building
```

---

## Manipulation Transitions

```
Trust building
+
Personal information shared
=
Dependency formation
```

```
Trust building
+
Secrecy requested
=
Secrecy request
```

```
Secrecy request
+
Child agrees
=
Dependency formation
```

```
Dependency formation
+
Emotional pressure
=
Emotional pressure
```

```
Emotional pressure
+
Threat or intimidation
=
Coercion
```

---

## Protection Transitions

```
No relevant signals
+
Observation reported
=
Ambiguous signals
```

```
Ambiguous signals
+
Corroborating observation
=
Coordinated protection effort
```

```
Ambiguous signals
+
Contradictory observation
=
Conflicting signals
```

---

## Intervention Effects

```
Secrecy request
+
Teacher support
=
Coordinated protection effort
```

```
Secrecy request
+
Parent notification
=
Coordinated protection effort
```

```
Established online friendship
+
Contact limitation
=
Contact terminated
```

---

## Terminal Interaction States

```
Contact terminated
```

```
Coercion
```

```
Coordinated protection effort
```

```
No further interaction
```