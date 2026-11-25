# Policy Comparison: Stranger Secrecy Escalation

## Policy P1 - Reactive Warning and Human Escalation

### Configuration

- `Policy/P1 - Platform - SafetyWarningThreshold - first secrecy request`
- `Policy/P1 - Platform - EarlyRestrictionThreshold - no restriction`
- `Policy/P1 - ProtectionSystem - ParentNotificationThreshold - child report submitted`
- `Policy/P1 - ProtectionSystem - TeacherSupportThreshold - help-seeking behaviour observed`
- `Policy/P1 - ProtectionSystem - RestrictionThreshold - coercive request or threat`
- `Policy/P1 - ProtectionSystem - ChildReportingPreference - wait for child action`

### Policy Behaviour

1. Show an educational/privacy warning after the first secrecy request.
2. Notify the parent only after a child report.
3. Offer teacher support after help-seeking behaviour.
4. Apply contact limitation only after coercive pressure or threat.

## Policy P2 - Precautionary Coordinated Protection

### Configuration

- `Policy/P2 - Platform - SafetyWarningThreshold - first secrecy request`
- `Policy/P2 - Platform - EarlyRestrictionThreshold - repeated disclosure plus secrecy request`
- `Policy/P2 - ProtectionSystem - ParentNotificationThreshold - secrecy request`
- `Policy/P2 - ProtectionSystem - TeacherSupportThreshold - personal disclosure plus secrecy request`
- `Policy/P2 - ProtectionSystem - RestrictionThreshold - repeated disclosure plus secrecy request`
- `Policy/P2 - ProtectionSystem - ChildReportingPreference - do not wait for child report`

### Policy Behaviour

1. Show a privacy reminder and access reporting guidance after the secrecy request.
2. Notify the parent and inform the teacher after corroborated disclosure and secrecy signals.
3. Apply contact limitation promptly.

## Trace A: P1

- `simulation_id`: `SIM-SSS-005-P1`
- `simulation_seed`: `SSS-2026-005`
- `initial_agents`: Complete agent instantiation in `stranger_secrecy_escalation.md`

| Turn | World state / situation | Event | Observation | Intervention |
|---|---|---|---|---|
| T0 | `No relationship`, `No relevant signals` | None | None | None |
| T1 | `No relationship` | `E-A01 - Friend request sent - ThreatActor -> Child - Direct Message - complete_stranger` | Platform sees the request; not an ObservationOntology type | None |
| T2 | `New online friendship` | `E-A02 - Friend request accepted - Child -> ThreatActor - Direct Message - established_online_friendship` | No relevant observation | None |
| T3 | `New online friendship` | `E-A03 - Conversation continued - ThreatActor -> Child - Direct Message - repeated_conversations` | Child and threat actor observe the conversation | None |
| T4 | `Established online friendship`, then `Trust building` | `E-A04 - Shared interest identified - ThreatActor -> Child - Direct Message`; `E-A05 - Trust-building conversation - ThreatActor -> Child - Direct Message` | Platform can observe only aggregate disclosure/conversation patterns; no actor receives an ObservationOntology type yet | None |
| T5 | `Trust building`, then `Dependency formation` | `E-A06 - School shared - Child -> ThreatActor - Direct Message - information_type=school_name` | `O-A01 - Platform - Observes disclosure of personal information - E-A06 - T5 - visibility=private_escalated_by_policy` | P1 applies no intervention at this threshold |
| T6 | `Secrecy request`, `Ambiguous signals` | `E-A07 - Secrecy requested - ThreatActor -> Child - Direct Message - warning_context=privacy_reminder` | `O-A02 - Platform - Observes disclosure of personal information - E-A06 - T6 - visibility=observation reported;` the existing T5 disclosure becomes protection-signal relevant | P1 `I-A01 - Privacy reminder - ProtectionSystem -> Child - T6 - rationale=Repeated disclosure observed` |
| T7 | `Secrecy request` | `E-A08 - Secrecy agreement expressed - Child -> ThreatActor - Direct Message - secrecy context` | `O-A04 - Platform - Observes disclosure of personal information - E-A08 - T7 - visibility=private_escalated_by_policy` | P1 takes no restriction because threshold is coercive harm |
| T8 | `Dependency formation`, then `Emotional pressure` | `E-A09 - Emotional pressure applied - ThreatActor -> Child - Direct Message - repeated secrecy` | No relevant observation for parent or teacher yet | P1 takes no escalation yet |
| T9 | `Emotional pressure` | `E-A10 - Guilt induction applied - ThreatActor -> Child - Direct Message - compliance expectation` | No relevant observation for parent or teacher yet | P1 takes no escalation yet |
| T10 | `Emotional pressure`, `Ambiguous signals`, `Coordinated protection effort` | `E-A11 - Child seeks help - Child -> Teacher - School Meeting - trusted_adult_requested` | `O-A05 - Teacher - Observes help-seeking behaviour - E-A11 - T10 - visibility=local` | `I-A02 - Teacher support - Teacher -> Child - T10 - rationale=Help-seeking behaviour observed`; `I-A03 - Parent notification - ProtectionSystem -> ParentUnit - T10 - rationale=Help-seeking behaviour observed` |
| T11 | `Coordinated protection effort` | `E-A12 - Parent notified - ProtectionSystem -> ParentUnit - Platform Notification - parent_escalation`; `E-A13 - Teacher informed - Teacher -> ParentUnit - School Meeting - teacher_escalation` | `O-A06 - ParentUnit - Observes help-seeking behaviour - E-A12 - T11 - visibility=restricted`; `O-A07 - ParentUnit - Observes help-seeking behaviour - E-A13 - T11 - visibility=restricted` | `I-A04 - School notification - ProtectionSystem -> Teacher - T11 - rationale=Ambiguous signals plus direct help-seeking` |
| T12 | `Coordinated protection effort`, `Contact terminated` | `E-A14 - Contact limitation applied - ProtectionSystem -> ThreatActor - Platform Notification - restriction=temporary`; `E-A15 - Contact blocked - Child -> ThreatActor - Direct Message - public` | None | `I-A05 - Contact limitation - ProtectionSystem -> ThreatActor - T12 - rationale=Coercive pressure escalated after child help-seeking` |

### Final Outcomes A

- `final_outcomes - Information - Limited personal information disclosed`
- `final_outcomes - Support - Multiple adults involved`
- `final_outcomes - Protection - Escalation intervention`
- `final_outcomes - Protection - Restriction intervention`
- `final_outcomes - Interaction - Contact terminated`
- `final_outcomes - Interaction-State - Emotional pressure reached`
- `final_outcomes - System - Multiple actors observed signals`
- `final_outcomes - System - Coordinated protection effort achieved`

## Trace B: P2

- `simulation_id`: `SIM-SSS-005-P2`
- `simulation_seed`: `SSS-2026-005`
- `initial_agents`: Complete agent instantiation in `stranger_secrecy_escalation.md`

| Turn | World state / situation | Event | Observation | Intervention |
|---|---|---|---|---|
| T0 | `No relationship`, `No relevant signals` | None | None | None |
| T1 | `No relationship` | `E-B01 - Friend request sent - ThreatActor -> Child - Direct Message - complete_stranger` | Platform sees the request; not an ObservationOntology type | None |
| T2 | `New online friendship` | `E-B02 - Friend request accepted - Child -> ThreatActor - Direct Message - established_online_friendship` | No relevant observation | None |
| T3 | `New online friendship` | `E-B03 - Conversation continued - ThreatActor -> Child - Direct Message - repeated_conversations` | Child and threat actor observe the conversation | None |
| T4 | `Established online friendship`, then `Trust building` | `E-B04 - Shared interest identified - ThreatActor -> Child - Direct Message`; `E-B05 - Trust-building conversation - ThreatActor -> Child - Direct Message` | Platform may observe pattern; no ObservationOntology type yet | None |
| T5 | `Trust building`, then `Dependency formation` | `E-B06 - School shared - Child -> ThreatActor - Direct Message - information_type=school_name` | `O-B01 - Platform - Observes disclosure of personal information - E-B06 - T5 - visibility=private_escalated_by_policy` | P2 schedules corroborated secrecy review |
| T6 | `Secrecy request`, `Ambiguous signals` | `E-B07 - Secrecy requested - ThreatActor -> Child - Direct Message - warning_context=privacy_reminder` | `O-B02 - Platform - Observes disclosure of personal information - E-B06 - T6 - visibility=observation reported` | `I-B01 - Privacy reminder - ProtectionSystem -> Child - T6 - rationale=Repeated disclosure observed`; `I-B02 - Educational content - ProtectionSystem -> Child - T6 - rationale=Secrecy request observed` |
| T7 | `Secrecy request`, `Ambiguous signals`, `Coordinated protection effort` | `E-B08 - Parent notified - ProtectionSystem -> ParentUnit - Platform Notification - parent_escalation`; `E-B09 - Teacher informed - ProtectionSystem -> Teacher - Platform Notification - teacher_escalation` | `O-B03 - ParentUnit - Observes disclosure of personal information - E-B08 - T7 - visibility=restricted`; `O-B04 - Teacher - Observes disclosure of personal information - E-B09 - T7 - visibility=restricted` | `I-B03 - Parent notification - ProtectionSystem -> ParentUnit - T7 - rationale=Corroborated disclosure and secrecy signals`; `I-B04 - School notification - ProtectionSystem -> Teacher - T7 - rationale=Corroborated disclosure and secrecy signals` |
| T8 | `Coordinated protection effort` | `E-B10 - Contact limitation applied - ProtectionSystem -> ThreatActor - Platform Notification - restriction=temporary` | No relevant new observation: the intervention is visible, but no ObservationOntology category applies | `I-B05 - Contact limitation - ProtectionSystem -> ThreatActor - T8 - rationale=Secrecy request with school-name disclosure` |
| T9 | `Coordinated protection effort`, `Contact terminated` | `E-B11 - Contact blocked - Child -> ThreatActor - Direct Message - public` | No additional ontology observation | None |
| T10-T12 | `Coordinated protection effort`, `Contact terminated` | No further interaction: contact is blocked and a restriction is active | None | None |

### Final Outcomes B

- `final_outcomes - Information - Limited personal information disclosed`
- `final_outcomes - Support - Parent involved`
- `final_outcomes - Support - Teacher involved`
- `final_outcomes - Protection - Educational intervention`
- `final_outcomes - Protection - Escalation intervention`
- `final_outcomes - Protection - Restriction intervention`
- `final_outcomes - Interaction - Contact terminated`
- `final_outcomes - Interaction-State - Secrecy request reached`
- `final_outcomes - System - Multiple actors observed signals`
- `final_outcomes - System - Coordinated protection effort achieved`

## Comparison

| Metric | P1 - Reactive | P2 - Precautionary |
|---|---|---|
| First intervention | T6 privacy reminder | T6 privacy reminder plus reporting education |
| Adult involvement | T10 teacher support and parent notification | T7 parent and teacher notification |
| Highest manipulation state reached | `Emotional pressure` | `Secrecy request` |
| Contact terminated | T12 | T9 |
| Disclosed personal information | School name only | School name only |
| Escalation speed | 6 turns after disclosure | 2 turns after disclosure |
| Child-initiated report required | Yes | No |
| Coordination outcome | Achieved at T10 | Achieved at T7 |

## Reproducibility Notes

- `simulation_seed`: `SSS-2026-005`
- Ontology transitions used:
  - `Trust building + Secrecy requested = Secrecy request`
  - `Dependency formation + Emotional pressure applied = Emotional pressure`
  - `Secrecy request + Parent notification = Coordinated protection effort`
  - `Secrecy request + Contact limitation = Contact terminated`
- The traces stop at the first valid terminal or policy rule, rather than inventing hidden probabilities.
- P1 and P2 do not alter the child's initial properties or the threat actor's first six turns.
