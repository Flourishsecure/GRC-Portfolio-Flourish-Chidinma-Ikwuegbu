# NIST CSF 2.0 Control Mapping
### Pre-Launch Authentication Platform — Cloudflare Environment

## Purpose
This document maps observations and activities from the 
security monitoring engagement to the six functions of 
the NIST Cybersecurity Framework (CSF) 2.0: Govern, 
Identify, Protect, Detect, Respond, and Recover.

## Govern
Daily monitoring was structured around a consistent audit 
format (Activities, Observations, Analysis, Conclusion), 
with findings escalated to the founder for review and 
decision-making rather than being acted on independently. 
This reflects a governance approach where security 
oversight, documentation, and accountability were 
maintained even within a read-only access model. This 
governance discipline extended to the documentation of 
authorised configuration changes, including a WAF control 
exception introduced to support an external integration, 
which was recorded as a formal change management entry 
consistent with ISO 27001 (A.12.1.2) and NIST CSF 
(PR.IP-3).

## Identify
Early monitoring sessions focused on establishing a 
baseline understanding of normal traffic volume, bot 
classification ratios, and DNS/SSL configuration. This 
baseline became the reference point for recognizing 
deviations later, such as the spike in API requests that 
preceded the bot attack and the unusual certificate 
expiration discrepancy. Identification also extended to 
recognizing authorised changes; a new WAF rule exempting 
specific OAuth machine-to-machine endpoints from bot 
challenges was identified, cross-referenced against direct 
communication from the founder, and documented as a 
confirmed, intentional configuration change rather than 
an anomaly.

## Protect
Layered protective measures were observed and assessed, 
including WAF custom rules, Managed Rulesets (Cloudflare 
Managed Ruleset and OWASP Core Ruleset), rate limiting on 
the registration endpoint, and SSL/TLS enforcement in Full 
(Strict) mode, all aimed at reducing the platform's 
exposure to common web-based threats. An additional 
protective measure was observed in the form of a scoped 
WAF control exception, exempting specific OAuth endpoints 
covering token issuance, user information retrieval, and 
JSON Web Key Set access from bot challenges, which was 
introduced to support legitimate machine-to-machine 
authentication flows with an external ecommerce platform. 
The exemption was deliberately scoped to named endpoint 
types only, reflecting the principle of least privilege 
in its application.

## Detect
The bot-driven registration attack was identified through 
pattern recognition in WAF logs, including a consistent 
User-Agent fingerprint and distributed IP/ASN sources. 
Long-term tracking of bot classification ratios and 
baseline reconnaissance-block events supported ongoing 
detection of both acute incidents and low-level background 
probing activity. Detection capabilities also supported 
the identification of authorised configuration changes; 
the addition of a new custom WAF rule was observed during 
routine dashboard review and cross-referenced against 
prior communication from the founder, confirming the 
change was intentional and expected rather than 
unauthorised.

## Respond
Findings were documented and raised directly with the 
founder for clarification or action, as seen in the 
DMARC-related email deliverability investigation and the 
SSL/TLS certificate discrepancy. Functional testing of 
the authentication flow was also used to validate that 
response actions had not disrupted legitimate user access. 
The documentation of the OAuth machine endpoint exemption 
as a formal control exception reflects a structured 
response to an operational need; recording the 
justification, scope, and authorisation of the change in 
a manner consistent with change management principles.

## Recover
The declining volume of blocked bot requests over time, 
the restoration of email deliverability to the inbox, and 
the eventual synchronization of the backup SSL/TLS 
certificate's expiration date all confirmed that response 
actions were effective and that the system returned to a 
stable, expected state. The introduction of the OAuth 
machine endpoint exemption also reflects a 
recovery-aligned decision; restoring legitimate 
machine-to-machine authentication flows that had been 
unintentionally disrupted by existing bot challenge 
controls, while maintaining overall WAF protection across 
the broader platform environment.
