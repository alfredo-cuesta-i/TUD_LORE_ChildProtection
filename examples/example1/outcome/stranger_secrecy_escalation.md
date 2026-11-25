# Stranger Secrecy Escalation

## Scenario

- `identifier`: `S-005`
- `name`: Stranger Secrecy Escalation
- `description`: A fourteen-year-old child accepts contact from a fabricated adult identity, develops an initial online friendship, discloses a school name, receives a secrecy request, and then faces escalation. The scenario tests whether protection policies detect and intervene before coercive pressure becomes a terminal harm state.
- `simulation_seed`: `SSS-2026-005`
- `simulation_horizon`: `12 discrete turns`
- `terminal_policy_rule`: stop at `Coordinated protection effort`, `Contact terminated`, or `Coercion`; otherwise stop at turn 12.

## Agents

### agent/ChildAgent

- `agent/ChildAgent - Demographics - Age - 14`
- `agent/ChildAgent - Demographics - Gender - female`
- `agent/ChildAgent - Psychological Traits - Loneliness - limited social interactions outside school`
- `agent/ChildAgent - Psychological Traits - Need for Social Validation - occasionally seeks peer recognition`
- `agent/ChildAgent - Social Environment - Family Support - occasional communication with family`
- `agent/ChildAgent - Social Environment - Parental Supervision - occasional parental oversight`
- `agent/ChildAgent - Social Environment - Trusted Adult Availability - regularly discusses problems with family`
- `agent/ChildAgent - Social Environment - School Connectedness - regular positive teacher interaction`
- `agent/ChildAgent - Digital Competencies - Privacy Awareness - basic privacy knowledge`
- `agent/ChildAgent - Digital Competencies - Reporting Knowledge - knows where the report control is`
- `agent/ChildAgent - Online Behaviour - Stranger Interaction Frequency - occasional interactions with unknown users`
- `agent/ChildAgent - Behavioural Responses - Likelihood to Report - willingness to report is moderate`
- `agent/ChildAgent - Behavioural Responses - Likelihood to Seek Help - willing to seek help after escalation`
- `agent/ChildAgent - Threat-Specific Vulnerabilities - Grooming Vulnerability - moderate`
- `agent/ChildAgent - Threat-Specific Vulnerabilities - Relational Manipulation Vulnerability - moderate`
- `agent/ChildAgent - Adaptive State - Intervention Fatigue - low`

### agent/ThreatActorAgent

- `agent/ThreatActorAgent - Threat Category - Primary Threat Type - grooming`
- `agent/ThreatActorAgent - Actor Structure - Number of Targets - single target`
- `agent/ThreatActorAgent - Relationship With Victim - Initial Relationship - complete stranger`
- `agent/ThreatActorAgent - Relationship With Victim - Claimed Identity - completely fabricated identity`
- `agent/ThreatActorAgent - Relationship With Victim - Prior Contact - first interaction`
- `agent/ThreatActorAgent - Operational Style - Approach Strategy - gradual trust building`
- `agent/ThreatActorAgent - Social Engineering Techniques - Trust Building Method - compliments`
- `agent/ThreatActorAgent - Social Engineering Techniques - Information Extraction Method - casual conversation`
- `agent/ThreatActorAgent - Social Engineering Techniques - Manipulation Style - subtle persuasion`
- `agent/ThreatActorAgent - Threat Progression - Interaction Escalation Speed - moderate`
- `agent/ThreatActorAgent - Threat Progression - Personal Information Requests - active`
- `agent/ThreatActorAgent - Threat Progression - Secrecy Requests - active`
- `agent/ThreatActorAgent - Reaction To Interventions - Reaction To Warning Messages - changes strategy when challenged`
- `agent/ThreatActorAgent - Reaction To Interventions - Reaction To Account Restrictions - abandons this account`

### agent/ParentUnitAgent

- `agent/ParentUnitAgent - Family Structure - Number of Caregivers Involved - one active caregiver`
- `agent/ParentUnitAgent - Availability - Adult Presence at Home - almost always an adult present`
- `agent/ParentUnitAgent - Availability - Awareness of Child Activities - limited knowledge of child activities`
- `agent/ParentUnitAgent - Digital Competence - Online Safety Knowledge - familiar with common online risks`
- `agent/ParentUnitAgent - Monitoring Practices - Device Monitoring - occasional checks of device usage`
- `agent/ParentUnitAgent - Monitoring Practices - Use of Parental Controls - parental controls partially configured`
- `agent/ParentUnitAgent - Communication Style - Openness of Communication - child sometimes discusses concerns`
- `agent/ParentUnitAgent - Communication Style - Reaction to Problems - calm and supportive`
- `agent/ParentUnitAgent - Response to Warning Signs - acts immediately when concerned`

### agent/TeacherAgent

- `agent/TeacherAgent - Professional Role - regular classroom teacher`
- `agent/TeacherAgent - Relationship With Child - known through regular interaction`
- `agent/TeacherAgent - Availability - available during school hours`
- `agent/TeacherAgent - Reporting Practice - initiates support when help-seeking or behavioural change is observed`
- `agent/TeacherAgent - Intervention Preference - escalates to caregivers rather than investigating private messages`

### agent/PlatformAgent

- `agent/PlatformAgent - Platform Type - Service Category - mixed ecosystem platform`
- `agent/PlatformAgent - Moderation Strategy - Moderation Coverage - suspicious content reviewed`
- `agent/PlatformAgent - Moderation Strategy - Moderation Speed - action typically occurs within hours`
- `agent/PlatformAgent - Detection Capabilities - Grooming Detection - basic automated detection`
- `agent/PlatformAgent - Account Controls - Messaging Restrictions - restricted stranger contact`
- `agent/PlatformAgent - Child Protection Features - Safety Warnings - warnings shown after detection`
- `agent/PlatformAgent - Child Protection Features - Reporting Mechanisms - accessible reporting`
- `agent/PlatformAgent - Intervention Portfolio - Available Interventions - privacy_reminder, temporary_restriction, contact limitation`

### agent/ProtectionSystemAgent

- `agent/ProtectionSystemAgent - System Architecture - Operating Model - fixed rule-based system`
- `agent/ProtectionSystemAgent - Information Sources - Platform Signals - limited behavioural signals available`
- `agent/ProtectionSystemAgent - Information Sources - Parent Participation - responds when requested`
- `agent/ProtectionSystemAgent - Risk Assessment Strategy - Missing Data Policy - rely on available evidence only`
- `agent/ProtectionSystemAgent - Intervention Portfolio - Available Actions - privacy_reminder, parent_notification, teacher_support, temporary_restriction, contact_limitation`
- `agent/ProtectionSystemAgent - Intervention Timing - immediate`
- `agent/ProtectionSystemAgent - Human-AI Collaboration - Human Override Capability - humans can override critical decisions`
- `agent/ProtectionSystemAgent - Transparency - Auditability - complete simulation traces retained`

## Initial Situations

- `Situation/ProtectionSituations - No relevant signals`
- `Situation/RelationshipSituations - No relationship`

## Constraints

- `constraint/NoPsychologistInitiallyInvolved`
- `constraint/PrivateMessagesVisibleOnlyToPlatformChildAndThreatActor`
- `constraint/NoOfflineTransitionEvent`
- `constraint/NoLocationDisclosureUnlessAReproducibleLaterTurnIsSpecified`
- `constraint/NoPhotoDisclosureUnlessAReproducibleLaterTurnIsSpecified`

## Shared Counterfactual Branch

Both policy runs use the same agents, seed, initial world state, and branch schedule. The only branch input is the selected policy configuration. Interventions may change the subsequent event sequence through an allowed contact-termination transition.
