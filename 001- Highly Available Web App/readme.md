# Scenario 01: Highly Available Public Web Application 

## Task

You’ve joined a small team that is launching a public-facing web application for a growing organization. The app is currently hosted on a single server and has started experiencing downtime whenever traffic spikes or when the server becomes unhealthy.

Your task is to design and implement an AWS solution that:

1. Keeps the application available even if an EC2 instance fails.
2. Distributes incoming traffic across multiple instances.
3. Automatically scales out during periods of high demand and scales in when demand reduces.
4. Provides basic monitoring and alerting so the team can detect issues early.
5. Follows good security practice by avoiding hardcoded AWS access keys on servers.

## Deliverables

- A working AWS deployment that meets the requirements above.
- An architecture diagram showing the major components and traffic flow.
- Evidence of testing (availability, failover/self-healing, and scaling behavior).
- A cleanup plan to remove resources after validation to avoid unnecessary costs.
