# Event Ontology


The event ontology defines the observable events that may occur within the simulation environment.

Events represent actions, disclosures, interventions, observations, communications, or system operations.

The ontology does not define:
- probabilities
- risk scores
- rewards
- causal relationships

Those aspects are defined elsewhere (if necessary).

The event ontology only defines the permissible event types that may appear during a simulation run.

## Relationship Events

- Friend request sent
- Friend request accepted
- Friend request rejected
- New conversation started
- Conversation continued
- Contact blocked
- Contact unblocked

## Information Disclosure Events

- Personal information requested
- Personal information shared
- Name shared
- Age shared
- School shared
- Location shared
- Contact information shared
- Photo shared
- Video shared
- Live image shared

## Trust and Relationship Events

- Compliment delivered
- Shared interest identified
- Emotional support offered
- Gift or reward offered
- Romantic interest expressed
- Trust-building conversation
- Dependency-building interaction

## Manipulation Events

- Secrecy requested
- Secrecy agreement expressed
- Emotional pressure applied
- Guilt induction applied
- Authority claim made
- Threat delivered
- Blackmail attempt
- Coercive request

## Platform Interaction Events

- Content posted
- Content removed
- Account reported
- Account reviewed
- Account restricted
- Account suspended
- Safety warning shown
- Privacy reminder shown

## Educational Events

- Educational content delivered
- Online safety advice delivered
- Scam awareness content delivered
- Privacy awareness content delivered
- Reporting guidance delivered

## Child Protection Events

- Child report submitted
- Parent notified
- Teacher informed
- Psychologist informed
- Protection system alerted
- External referral initiated

## Observation Events

- Behavioural change observed
- Increased online activity observed
- Personal disclosure observed
- Help-seeking behaviour observed
- Repeated contact observed
- Suspicious interaction observed

## Support Events

- Child seeks help
- Child receives support
- Parent provides guidance
- Teacher provides guidance
- Psychologist provides support
- Trusted adult contacted

## Restriction Events

- Contact limitation applied
- Messaging restriction applied
- Temporary restriction applied
- Account access limited
- Location sharing disabled

## System Events

- Risk assessment performed
- Intervention recommended
- Intervention applied
- Escalation initiated
- Human review requested
- Case closed

## Communication Channels

Possible values:

- Direct Message
- Public Post
- Comment Thread
- Group Chat
- Gaming Chat
- Livestream Chat
- Online Forum
- Voice Chat
- Video Call
- School Meeting
- Phone Call
- Email
- Platform Notification

## Event Participants

Possible actor values:

- Child
- ThreatActor
- ParentUnit
- Teacher
- Psychologist
- Platform
- ProtectionSystem

## Context Attributes

Possible values:

### Information Context

- age
- name
- school_name
- school_location
- home_location
- contact_information
- photograph
- video

### Relationship Context

- complete_stranger
- online_acquaintance
- gaming_teammate
- social_media_follower
- friend_of_friend
- established_online_friendship

### Warning Context

- privacy_reminder
- stranger_contact_warning
- grooming_warning
- scam_warning
- cyberbullying_warning

### Escalation Context

- parent_escalation
- teacher_escalation
- psychologist_escalation
- platform_escalation
- external_service_escalation