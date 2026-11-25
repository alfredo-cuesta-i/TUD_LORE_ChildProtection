# Knowledge-Base Gap: Post-Intervention Recurrence and Recovery Follow-Up

## Identified Gap

The knowledge base has interventions, restrictions, terminal situations, and intervention history, but it does not contain an explicit post-intervention follow-up state or recurrence event. In particular, it cannot represent:

1. whether a temporary restriction or contact limitation remains effective;
2. whether the same threat actor returns under a second account;
3. whether the child reports renewed contact;
4. whether the original intervention failed or needs escalation;
5. whether the child recovered support, or whether repeated interventions are causing fatigue.

The threat actor specification has `Account replacement behaviour` and `Learning from failure`, but there is no matching ontology event for re-contact after a restriction. The existing system can reach `Contact terminated`, but it has no persistent `restriction effectiveness`, `recontact attempt`, or `follow-up review` state.

## Why This Gap Weakens Child Online Safety

A restriction in a single trace is not evidence that the harm stopped. An actor can replace an account or move to a new channel, and the child may remain exposed. Without recurrence and follow-up, a policy can appear successful only because the trace ends at the first terminal state. The system also lacks an ontology-defined way to learn that the child needs support after the restriction or that repeated restrictions are ineffective.

## Ontology Bridge Needed

Add, under the existing ontology constraints, only values derived from observable child-online-safety mechanisms:

### Events

- `Restriction effectiveness reviewed`
- `Recontact attempt detected`
- `Recontact report submitted`
- `Child follow-up completed`
- `Follow-up concern observed`
- `Intervention outcome reported`
- `Appeal submitted` (if the restriction affected the child, with appropriate privacy constraints)
- `Safety support resumed`

### Situations

- `Restriction effective`
- `Restriction ineffective`
- `Follow-up due`
- `Recovery supported`
- `Renewed risk`

### Observations

- `Observes recontact attempt`
- `Observes failed restriction`
- `Observes follow-up concern`
- `Observes recovery progress`

### Interventions

- `Follow-up check-in`
- `Escalation review`
- `Restriction extension`
- `Alternative-channel monitoring`
- `Intervention fatigue review`

## Valid Transition Examples

```text
Contact terminated
+
Recontact attempt detected
=
Renewed risk
```

```text
Renewed risk
+
Recontact report submitted
=
Coordinated protection effort
```

```text
Coordinated protection effort
+
Follow-up check-in
=
Recovery supported
```

```text
Renewed risk
+
Restriction ineffective
=
Escalation review
```

These proposed values must be approved by the ontology maintainers before implementation. They are bridge requirements, not runtime additions made by the comparison trace.

## Why Bridging It Strengthens Safety

The bridge turns `Contact terminated` from an end of the visible trace into a testable protection lifecycle:

- restrictions are checked instead of assumed effective;
- renewed contact becomes observable and escalation-worthy;
- child follow-up is explicit and can detect trauma, fear, or intervention fatigue;
- the protection system obtains feedback for changing a repeated or ineffective intervention;
- outcome-based comparison can distinguish a temporary contact stop from sustained protection.

This improves the ecosystem under the same principles already used by the knowledge base: explicit state, immutable events, actor visibility, valid ontology transitions, and reproducible traces.
