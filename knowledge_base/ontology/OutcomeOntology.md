# OutcomeOntology.md

## Purpose

The outcome ontology does not evaluate success.

It records observable end states.

Researchers can later compare which policies produce which outcomes.

---

# Interaction Outcomes

```
No contact established
```

```
Contact established
```

```
Contact maintained
```

```
Contact terminated
```

---

# Information Outcomes

```
No personal information disclosed
```

```
Limited personal information disclosed
```

```
Extensive personal information disclosed
```

```
Photo disclosed
```

```
Location disclosed
```

---

# Support Outcomes

```
No adult involved
```

```
Parent involved
```

```
Teacher involved
```

```
Psychologist involved
```

```
Multiple adults involved
```

---

# Protection Outcomes

```
No intervention
```

```
Educational intervention
```

```
Support intervention
```

```
Escalation intervention
```

```
Restriction intervention
```

---

# Interaction-State Outcomes

```
Trust building reached
```

```
Dependency formation reached
```

```
Secrecy request reached
```

```
Emotional pressure reached
```

```
Coercion reached
```

---

# System Outcomes

```
No actor observed signals
```

```
Single actor observed signals
```

```
Multiple actors observed signals
```

```
Coordinated protection effort achieved
```

---

# Trace Outcome

Every simulation run must generate:

```
simulation_id
initial_agents
event_sequence
situation_sequence
observations
interventions
final_outcomes
```

This guarantees reproducibility.