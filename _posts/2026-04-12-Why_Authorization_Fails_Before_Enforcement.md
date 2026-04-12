---
layout: default
title: "Why Authorization Fails Before Enforcement"
---

# Why Authorization Fails Before Enforcement

## Introduction

Over the past years, and especially through hands-on offensive security work, I’ve found myself spending less time looking for isolated technical vulnerabilities, and more time trying to understand how systems are actually designed — and how those design decisions can be used against them.

There has been a clear shift.

Traditional red team approaches often focus on identifying specific weaknesses: a misconfiguration, an injection point, an exposed service. Those still matter. But in modern systems, the most impactful security failures rarely come from a single bug.

They come from how the system behaves as a whole.

More specifically, they emerge from how identity is modeled, how authorization decisions are made, and how trust is distributed across components.

Understanding these aspects has become far more valuable than simply finding technical issues in isolation.

Because once you understand the system, you are no longer just looking for vulnerabilities.

You are looking for ways to break the assumptions it was built on.


Most discussions around authorization failures tend to focus on missing checks, exposed endpoints, or improperly protected resources.

While those issues do exist, they are rarely the root cause.

In modern systems, authorization does not fail at enforcement.

It fails much earlier — at the level of design.

## Authentication vs Authorization: A Quick Context

Before diving deeper, it is important to clarify the distinction (for context):

- **Authentication (AuthN)** answers: *who are you?*  
- **Authorization (AuthZ)** answers: *what are you allowed to do?*

Modern systems rely on a variety of approaches to implement these:

### Authentication models

- **Session-based authentication**  
  - Pros: strong server-side control, easy revocation  
  - Cons: requires centralized state, harder to scale  
  
- **Token-based authentication (e.g., JWT)**  
  - Pros: scalable, portable across services  
  - Cons: introduces stale identity, difficult revocation, hidden state  
  
- **Stateful vs Stateless approaches**  
  - Stateless systems aim to remove server-side state  
  - In practice, they reintroduce state through:
    - token lifetimes  
    - refresh flows  
    - revocation mechanisms  
    - distributed caches  

### Authorization models

- **RBAC (Role-Based Access Control)**  
  - Pros: simple, widely adopted  
  - Cons: role explosion, lack of context  
  
- **ABAC (Attribute-Based Access Control)**  
  - Pros: flexible, context-aware  
  - Cons: complex evaluation, hard to reason about  
  
- **ReBAC (Relationship-Based Access Control)**  
  - Pros: models real-world relationships (e.g., Google Zanzibar)  
  - Cons: graph complexity, performance and consistency challenges  
  
- **Policy-based systems**  
  - Pros: centralized logic, expressive rules  
  - Cons: requires strict discipline and consistency across services  

Each of these models solves part of the problem.

None of them, on their own, guarantees secure authorization.

## Where Authorization Actually Breaks

Authorization failures typically emerge from incorrect assumptions about identity, state, and trust.

### Identity is assumed to be correct

Systems often assume that identity remains valid across requests:

- tokens carrying outdated claims  
- sessions that no longer reflect current permissions  
- roles embedded without revalidation  

#### Example: Stale Identity in Token-Based Authentication

Consider a system using JWT-based authentication where user roles are embedded directly in the token:

```json
{
  "user_id": 123,
  "role": "admin",
  "exp": 1710000000
}
```

The system assumes that the role contained in the token accurately reflects the current privileges of the user.

Now consider the following sequence:

1. A user authenticates and receives a valid token with elevated privileges (`role = admin`)
2. An administrator revokes those privileges in the backend system
3. The previously issued token remains valid until expiration
4. Downstream services continue to trust the token without revalidating the user's current role

From the perspective of the system, authorization checks are functioning as expected.

However, they are operating on outdated identity data.

The issue is not a missing authorization check, but an incorrect assumption:

that identity claims remain valid for the lifetime of the token

This effectively turns identity into a snapshot in time, rather than a reflection of current system state.

In practice, identity is dynamic. Any system that treats it as static introduces a window where authorization decisions are made on stale information

---

### State is assumed to be consistent

Distributed systems rarely have a single source of truth at all times.

However, many designs assume:

- immediate permission propagation  
- synchronized state across services  
- consistent enforcement everywhere  

In reality:

- caches introduce delay  
- services operate on stale data  
- revocation is not immediate  

This creates windows of unintended access.

These windows are often small, but in distributed systems, even short-lived inconsistencies can be reliably exploited.

Consider a distributed architecture composed of multiple services:


```
User → API Gateway → Service A → Service B
```


Service A is responsible for validating access to a resource, while Service B handles data retrieval.

The system assumes that permission changes are immediately reflected across all services.

Now consider the following sequence:

1. A user has access to a resource
2. Access is revoked in the primary authorization system
3. Service A reflects the updated state immediately
4. Service B continues to rely on cached authorization data
5. A request is routed directly or indirectly to Service B

Because Service B operates on stale state, the user is still able to access the resource.

The system behaves inconsistently depending on which component processes the request.

The underlying assumption is:

> that all services share a consistent and up-to-date view of authorization state

#### Combined Failure Scenario: Stale Identity + Inconsistent State

In many real-world systems, identity and state inconsistencies do not occur in isolation.

Consider the following scenario:

1. A user authenticates and receives a token containing elevated privileges
2. The user's permissions are revoked shortly after
3. The token remains valid and is accepted by multiple services
4. Some services rely on cached authorization data
5. Requests are processed using both stale identity and stale state

At no point is there a missing authorization check.

Every component enforces access control based on the information it has.

However, the information itself is no longer correct.

This leads to a subtle but critical failure mode:

> authorization decisions are technically correct, but semantically wrong

This type of issue is particularly difficult to detect with traditional testing approaches, as it does not manifest as a simple bypass, but as a timing and consistency problem within the system.

---

### Trust boundaries are implicit

A common pattern:

```
User → API Gateway → Service A → Service B
```

Authorization is verified once and then implicitly trusted downstream.

This creates hidden trust zones where:

- services assume upstream validation is sufficient  
- no further checks are performed  
- internal APIs become high-risk surfaces  

This pattern effectively shifts the security model from explicit verification to implicit trust, significantly increasing the attack surface within internal systems.

---

### Authorization logic is incomplete

Even when a model is defined (RBAC, ABAC, ReBAC), implementation often diverges:

- partial enforcement across endpoints  
- inconsistent use of policies  
- missing ownership validation  
- incorrect inheritance of permissions  

At this point, enforcement is present — but unreliable.

The system enforces authorization, but not consistently enough to guarantee correct behavior.

## Why Enforcement Is Already Too Late

By the time an authorization check is executed:

- identity may already be stale  
- permissions may already be outdated  
- trust assumptions may already be violated  

Enforcement mechanisms cannot fix flawed assumptions.

They only operate on the current (and potentially incorrect) state of the system.

## The Missing Piece: Threat Modeling and Risk Analysis

One of the most common patterns in real-world systems is this:

- authentication and authorization mechanisms are implemented  
- systems go to production  
- issues are discovered through incidents or testing  
- fixes are applied incrementally  

Without explicitly modeling how an attacker would interact with the system, these assumptions remain unchallenged until they fail in production.

What is missing is **design-time security thinking**.

Specifically:

- threat modeling  
- adversary behavior analysis  
- identification of trust boundaries  
- analysis of identity propagation  
- evaluation of consistency guarantees  

Without this, systems are designed under optimistic assumptions:

- identity is always valid  
- services always behave correctly  
- permissions are always up to date  

Attackers operate under the opposite assumptions.

## What Security Reviews Should Focus On

Instead of focusing only on endpoints and checks, security assessments should evaluate:

- how identity is propagated across services  
- where authorization decisions are enforced  
- how trust boundaries are defined  
- how state consistency is handled  
- how permission changes propagate  

These aspects define the real security posture of the system.

## Conclusion

Authorization failures are rarely caused by missing checks.

Authorization failures are rarely caused by missing checks.

They are caused by systems making correct decisions based on incorrect assumptions.

Understanding those assumptions — and how they break — is what separates testing inputs from actually assessing security.
