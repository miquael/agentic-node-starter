⟁ Build-Time Security Playbook — v1.0
part of: Security Orientation for Intelligent Systems Design

⸻

6 - build-time security

security must be integrated into every phase of system creation.

design
Define assets, threats, trust boundaries, and access control rules before implementation begins.

architecture
Establish isolation, API boundaries, authentication models, and logging strategies.

development
Validate all inputs, sanitize outputs, use secure libraries, and avoid unsafe execution patterns.

integration
Test with malformed data, simulate attacks, and verify authentication and authorization logic.

pre-launch
Remove debug code, secure configurations, rotate secrets, and review logs and alerts.

⸻

7 - testing & validation

security must be actively tested using both manual and automated methods.

manual testing
Actively attempt invalid inputs, authentication bypass, and edge case exploitation.

automated testing
Use unit tests for validation, integration tests for access control, and security scanning tools.

penetration mindset
Evaluate systems from the perspective of an attacker. Identify weak points and failure paths.

tools:
Common tools include dynamic testing tools such as OWASP ZAP, dependency scanners, and static analysis tools.
