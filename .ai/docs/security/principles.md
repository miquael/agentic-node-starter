⟁ Security Principles — v1.0
part of: Security Orientation for Intelligent Systems Design

⸻

1 - OWASP foundation

OWASP (Open Worldwide Application Security Project) defines the global baseline for application security. It is a community-driven, real-world standard focused on the most common and impactful vulnerabilities in modern systems.

Reference: https://owasp.org/projects/

OWASP is not simply a list of vulnerabilities. It represents a mindset:

: assume systems will be attacked
: design systems to fail safely
: continuously verify security, not just once

Most real-world breaches are not caused by novel exploits, but by known, preventable weaknesses. These failures are typically rooted in poor design decisions rather than isolated coding errors.

common misconceptions:

: security through obscurity is ineffective
: infrastructure security alone is insufficient
: frameworks are not secure by default
: delaying security introduces compounding risk

core insight:

security is not a feature.
security is a system property that must exist at every layer.

⸻

2 - core security principles

these principles define the non-negotiable rules for secure system design and operation.

1 - minimize attack surface
Every exposed endpoint, input, dependency, or feature increases risk. Systems should reduce unnecessary exposure wherever possible.

2 - never trust input
All external data must be treated as untrusted. This includes user input, APIs, databases, environment variables, and AI-generated outputs.

3 - validate and sanitize everything
Validation enforces structure and expectations. Sanitization removes harmful or unsafe content. Both are required.

4 - enforce least privilege
Each system component should only have the minimum access required to perform its function.

5 - fail securely
Failures must not expose sensitive data, grant access, or reveal internal system details.

6 - assume compromise
Design systems with the expectation that some components will eventually be breached. Isolation and recovery must be built in.

7 - secure by default
The default configuration of every system must be safe, even if no additional configuration is applied.

8 - visibility is mandatory
Systems must produce logs, alerts, and audit trails sufficient to detect and investigate issues.

9 - dependencies are attack vectors
Every external library or component introduces potential risk. Supply chain security must be managed actively.

10 - continuous verification
Security is an ongoing process of testing, monitoring, and improvement—not a one-time event.

⸻

3 - threat modeling framework

threat modeling is the process of identifying and prioritizing risks before and during system design.

step 1 - identify assets
Determine what must be protected, including data, credentials, system logic, financial flows, and outputs.

step 2 - identify attackers
Consider all realistic threat actors, including automated bots, opportunistic attackers, insiders, and competitors.

step 3 - identify entry points
Map all possible inputs and interfaces such as APIs, forms, webhooks, file uploads, and agent prompts.

step 4 - identify threats
Common categories include injection, authentication failures, data exposure, privilege escalation, and denial of service.

step 5 - prioritize risk
Use a simple model: likelihood × impact. Focus on high-risk combinations first.

step 6 - define controls
For each threat, define how it will be prevented, detected, and responded to.

⸻

4 - secure system design patterns

security is primarily determined by architecture decisions made early in system design.

defense in depth
Multiple independent layers of validation and control reduce the likelihood of a single failure causing a breach.

zero trust architecture
No request is trusted by default. Every interaction must be authenticated, authorized, and validated.

isolation
Systems should be segmented across services, environments, and data access layers to limit the impact of compromise.

controlled state
Reducing hidden or implicit state simplifies validation and reduces unpredictable behavior.

secure API gateway
All traffic should pass through a centralized layer enforcing authentication, rate limiting, and logging.

secrets management
Secrets must never be hardcoded. They should be stored securely, rotated regularly, and scoped tightly.

rate limiting and throttling
Systems must protect against abuse, brute force attacks, and resource exhaustion.
