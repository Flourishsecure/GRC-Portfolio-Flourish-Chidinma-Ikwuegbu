# Security Monitoring Case Study — Pre-Launch Startup Environment

## Summary
A remote, part-time cybersecurity internship at a pre-launch,
Cloudflare-based authentication platform, conducted under
read-only access and direct founder supervision. The role
involved daily security monitoring, audit-style documentation,
and hands-on tracking of a live bot-driven account registration
attack, an email deliverability issue linked to DMARC
configuration, an SSL/TLS certificate renewal discrepancy,
and an authorised WAF control exception introduced to support
OAuth machine-to-machine integration with an external ecommerce
platform. Findings throughout this case study are mapped to
NIST CSF 2.0 functions to demonstrate the practical application
of GRC principles in a real, evolving environment.

## Overview
This case study summarizes a remote, part-time cybersecurity
internship at a pre-launch, Cloudflare-based authentication
platform, working under the direct supervision of the founder.
With read-only access to the Cloudflare dashboard, the role
involved daily monitoring and audit-style documentation of WAF
activity, bot traffic, HTTP and API traffic patterns, and
SSL/TLS certificate status. During this period, the monitoring
work contributed to identifying and tracking an active
bot-driven account registration attack, supported analysis of
an email deliverability issue linked to DMARC configuration,
surfaced a discrepancy in SSL/TLS certificate renewal timing
that was raised with and clarified by the founder, and
documented an authorised control exception introduced to
support OAuth machine-to-machine integration with an external
ecommerce platform.

## My Role
- **Position:** Cybersecurity Intern (Remote, Part-Time)
- **Duration:** April 6, 2026 – Present
- **Access Level:** Read-only, Cloudflare dashboard
- **Supervision:** Direct, under the founder
- **Core Responsibilities:** Daily WAF and traffic monitoring,
  bot activity classification, DNS and SSL/TLS configuration
  review, audit-style documentation, functional testing of
  authentication flows, escalation of anomalies for founder
  review, and documentation of authorised configuration changes.

## Objectives
The primary objective of this internship was to conduct
ongoing, read-only monitoring and an audit-style review of
the platform's Cloudflare configuration ahead of public
launch. This included daily review of WAF activity, bot
traffic, and HTTP/API traffic patterns, alongside periodic
audits of DNS records, SSL/TLS configuration, Page Rules,
and caching settings for accuracy and adherence to best
practices. Beyond routine monitoring, the role also involved
identifying and tracking emerging security events as they
occurred, escalating anomalies to the founder for
clarification or action, and validating that legitimate user
flows continued to function correctly alongside active
security measures. The overall goal was to produce clear,
structured documentation that gave the founder ongoing
visibility into the platform's security posture and supported
informed decision-making ahead of launch.

## Methodology
Monitoring was conducted daily through read-only access to
the Cloudflare dashboard, and has continued informally beyond
this documented window. Each session followed a structured
audit format covering Activities, Observations, Analysis, and
Conclusion. Early sessions focused on familiarizing with the
dashboard environment and establishing a baseline
understanding of normal traffic and bot activity levels. As
patterns emerged, monitoring shifted toward identifying
deviations from baseline, such as unusual spikes in API
requests, shifts in bot classification ratios, or new WAF
event types, and assessing whether they indicated routine
background activity or required escalation.

Key data points reviewed in each session included HTTP
traffic volume and data transfer, bot classification
(verified bot, automated, likely automated, likely human,
unknown), API request activity and origin, WAF security
events (including custom rule triggers, Managed Ruleset
activity, and rate limiting), DNS record accuracy, and
SSL/TLS certificate status. When anomalies were identified,
including the bot-driven registration attack, the email
deliverability issue, the SSL/TLS certificate discrepancy,
and the OAuth control exception, findings were documented
in detail and raised directly with the founder for
clarification or resolution. Periodic functional testing
of the authentication flow (registration, login, and email
delivery) was also carried out from a user's perspective
to validate that legitimate flows continued operating
correctly alongside active security measures.

## Key Observations

### 1. Bot-Driven Account Registration Attack
A coordinated bot attack targeting the platform's
registration endpoint was identified through a consistent
pattern of fake account creations using gibberish names.
Analysis of WAF logs revealed a distinctive fingerprint:
a single outdated browser User-Agent (Chrome/61, dated
2017), originating from multiple IPs and ASNs across
different hosting providers, indicating distributed
automated activity designed to evade simple IP-based
blocking. Over the following days, the volume of blocked
requests was tracked from over 5,400 initial detections
down to single digits, confirming the effectiveness of
layered mitigations, including a registration endpoint
rate limit, Managed Rulesets, OWASP Core Ruleset, and a
custom rule targeting the specific bot fingerprint.

### 2. Email Deliverability Issue Linked to DMARC Configuration
During the bot attack period, authentication emails
(magic login links) began being delivered to recipients'
spam folders instead of their inboxes. Investigation
linked this shift to increased email volume and sending
pattern changes triggered by the bot activity, in
connection with the platform's DMARC configuration. This
observation highlighted a connection between
application-layer security events and email domain
reputation, a factor not immediately obvious from traffic
monitoring alone. Following remediation, functional
testing confirmed that authentication emails were
consistently delivered to the inbox across multiple test
accounts.

### 3. SSL/TLS Certificate Renewal Discrepancy
A discrepancy was observed between the expiration dates
of the platform's edge (universal) SSL/TLS certificate
and its backup certificate following an automatic renewal
event. The edge certificate's expiration date was updated
as expected, while the backup certificate's expiration
date remained unchanged for a period before later
updating. This was raised with the founder for
clarification, who confirmed the renewal was part of
Cloudflare's automatic process and attributed the
temporary discrepancy to a dashboard synchronization
delay between the primary and backup certificates; an
explanation later confirmed when the backup certificate's
expiration date was updated accordingly.

### 4. Long-Term Traffic and Bot Pattern Trends
Traffic volume and bot classification ratios fluctuated
significantly day to day, with automated and
likely-automated traffic consistently representing the
majority of recorded activity. Periods of low likely-human
traffic and elevated baseline reconnaissance blocking were
interpreted as background scanning or probing activity,
while periods of increased API requests and likely-human
traffic generally correlated with confirmed legitimate
activity, such as developer portal testing or direct
authentication flow testing. Tracking these patterns over
time helped distinguish between routine background noise
and activity that warranted closer attention or escalation,
reinforcing the importance of establishing a behavioral
baseline before evaluating anomalies.

### 5. Authorised WAF Control Exception — OAuth Machine Endpoint Exemption
A new custom WAF rule was observed exempting specific
OAuth endpoints from Cloudflare's bot challenge. The
exempted endpoints covered token issuance, user
information retrieval, and JSON Web Key Set access, which
are standard components of an OAuth 2.0 and OpenID
Connect authentication flow. The rule was introduced to
support machine-to-machine authentication between the
platform and an external ecommerce platform being
integrated by the founder, where Cloudflare's managed
challenge was blocking legitimate automated OAuth flows.
The founder confirmed the change was authorised and
intentional, and noted that the exemption would likely
be tightened on a case-by-case basis as integrations
develop. From a GRC perspective, this represents a
documented control exception; a deliberate, scoped
relaxation of a security control for a justified
operational purpose, consistent with change management
principles under ISO 27001 (A.12.1.2) and NIST CSF
(PR.IP-3).

## GRC Framework Application
Observations from this engagement were mapped against
the NIST Cybersecurity Framework (CSF) 2.0, covering
Govern, Identify, Protect, Detect, Respond, and Recover.
A detailed breakdown of this mapping is available in the
accompanying [NIST CSF 2.0 Control Mapping](../nist-csf-mapping/README.md)
document.

## Skills Demonstrated
1. WAF log analysis and bot traffic classification
2. HTTP and API traffic pattern analysis
3. Baseline establishment and anomaly detection
4. DNS and SSL/TLS configuration review
5. Audit-style documentation and structured reporting
6. Incident tracking and resolution monitoring
7. Root cause investigation (e.g., linking email
   deliverability to DMARC configuration)
8. Escalation and stakeholder communication
9. Functional testing of authentication flows from
   a user perspective
10. Application of NIST CSF 2.0 functions to
    real-world security monitoring
11. Sustained, self-directed monitoring
12. Documentation of authorised control exceptions
    and configuration changes

## Reflection
This internship gave me hands-on exposure to what
security monitoring and governance look like in a
real, evolving environment, not just in theory, but
through actual incidents that required pattern
recognition, careful documentation, and clear
communication with stakeholders. Tracking the bot
attack from detection through resolution, learning
how email deliverability connects back to domain
authentication and security posture, and documenting
a real-world control exception introduced to support
a live integration deepened my understanding of how
interconnected security, compliance, and operational
decisions really are. Coming from an accounting
background, I found that skills like attention to
detail, structured documentation, and escalation
discipline translated directly into this work. This
experience has reinforced my decision to pursue a
career in GRC, where I can combine that same rigor
with a growing technical foundation to help
organizations build and maintain trustworthy systems.
