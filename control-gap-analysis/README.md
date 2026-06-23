# Control Gap Analysis
### Pre-Launch Authentication Platform — Cloudflare Environment

## Purpose
This document summarizes control gaps observed during the 
monitoring period and recommends improvements to strengthen 
the platform's security posture ahead of public launch.

## 1. Reactive Rather Than Proactive WAF Configuration
At the start of the monitoring period, no Managed Rulesets 
(including the OWASP Core Ruleset) were enabled, and the 
registration endpoint had no rate limiting in place. These 
protections were only introduced after a bot-driven attack 
was already underway.

**Recommendation:** Enable Managed Rulesets and rate 
limiting on sensitive endpoints (registration, login, 
password recovery) by default before launch, rather than 
waiting for an active incident to trigger their 
implementation.

## 2. Inconsistent Custom Rule Status
Early review identified five custom firewall rules, only 
four of which were active; one rule (configured with a 
Managed Challenge action) remained disabled with no 
documented reason.

**Recommendation:** Conduct a full review of all custom 
rules before launch to confirm each rule's intended status 
(active/disabled) is deliberate, and document the rationale 
for any rules left disabled.

## 3. Limited Page Rule Coverage
Only one Page Rule was configured during the early 
monitoring period, which may leave certain 
traffic-handling scenarios (caching exceptions, redirects, 
security overrides for specific paths) unaddressed.

**Recommendation:** Review whether additional Page Rules 
are needed to handle edge cases such as sensitive endpoint 
protection, redirect logic, or caching exceptions for 
authenticated routes.

## 4. Certificate Renewal Visibility Gap
A discrepancy between the edge and backup SSL/TLS 
certificate expiration dates following an automatic renewal 
was only identified through manual dashboard review, with 
no automated alert flagging the temporary mismatch.

**Recommendation:** Establish a process or alert to verify 
that both edge and backup certificates update successfully 
and consistently following renewal, rather than relying on 
manual spot-checks.

## 5. Authorised Control Exception — OAuth Machine Endpoint Exemption
A WAF control exception was introduced to exempt specific 
OAuth machine-to-machine endpoints from Cloudflare's bot 
challenge, in order to support legitimate authentication 
flows between the platform and an external ecommerce 
integration. While the exemption was authorised, 
intentional, and scoped to named endpoint types only, it 
represents a deliberate relaxation of an existing security 
control; a gap that requires ongoing monitoring and 
periodic review.

This is not a remediation failure but rather an 
intentional operational trade-off, documented here as a 
formal control exception consistent with change management 
principles under ISO 27001 (A.12.1.2) and NIST CSF 
(PR.IP-3). The gap exists for a justified business reason 
and is accepted with awareness of the residual risk.

**Recommendation:** Periodically review the scope of the 
OAuth endpoint exemption as integrations develop, and 
confirm that the exempted endpoints are adequately 
protected at the application layer. Where possible, 
tighten the exemption scope on a case-by-case basis as 
each integration matures. Consider formally documenting 
an accepted risk entry for this exception in the risk 
register.
