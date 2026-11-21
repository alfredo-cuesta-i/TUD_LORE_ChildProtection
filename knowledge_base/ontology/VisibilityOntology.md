# VisibilityOntology.md

## Purpose

The objective is to explicitly define who can observe what.

This creates information asymmetry.

Different policy configurations can then be evaluated according to how information flows through the ecosystem.

---

# Child

Can observe:

- Friend request sent
- Friend request accepted
- Conversations
- Personal information requests
- Secrecy requests
- Educational content
- Warnings

Cannot directly observe:

- Platform detection processes
- Parent observations
- Teacher observations
- Protection system reasoning

---

# Threat Actor

Can observe:

- Child responses
- Child disclosures
- Child blocking actions
- Warning messages shown to the child

Cannot directly observe:

- Parent decisions
- Teacher observations
- Protection system reasoning

---

# Parent Unit

Can observe:

- Parent notifications
- Teacher communications
- Child disclosures
- Device activity when monitoring exists

Can sometimes observe:

- Behavioural change
- Increased online activity

Cannot directly observe:

- Private platform conversations
- Protection system reasoning

---

# Teacher

Can observe:

- Behavioural change
- Help-seeking behaviour
- Parent communications
- School-relevant disclosures

Can sometimes observe:

- Increased online activity

Cannot directly observe:

- Private messages
- Platform moderation

This follows the role described in the teacher specification. 

---

# Psychologist

Can observe:

- Case reports
- Parent reports
- Teacher reports
- Child disclosures
- Previous interventions

The psychologist is not assumed to continuously observe the child. 

---

# Platform

Can observe:

- Friend requests
- Conversations
- Reports
- Uploaded content
- Shared photos
- Shared location

Depending on configuration:

- suspicious patterns
- disclosure patterns
- repeated contacts

This is consistent with the platform moderation and detection capabilities. 

---

# Protection System

Can observe:

- Child reports
- Parent reports
- Teacher reports
- Platform signals
- External signals

depending on configuration. 

Cannot observe:

- Events not provided through configured channels

---

# Visibility Levels

```
public
```

Visible to all actors.

Example:

```
Contact blocked
```

---

```
local
```

Visible only to participating actors.

Example:

```
Conversation
```

---

```
restricted
```

Visible only after escalation.

Example:

```
Teacher informed
```

---

```
private
```

Visible only to the originating actor.

Example:

```
Internal platform detection
```