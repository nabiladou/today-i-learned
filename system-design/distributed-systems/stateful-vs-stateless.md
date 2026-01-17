# Stateless vs Stateful

## QUICK SUMMARY

A **stateless** system does **not store any client-specific data between requests**. Each request is **independent** and contains all the information needed to be processed. 

A **stateful** system remembers information about previous interactions.
Future requests **depend** on stored state. 

| Aspect      | Stateless | Stateful           |
| ----------- | --------- | ------------------ |
| Memory      | None      | Keeps session data |
| Scalability | Easy      | Harder             |
| Failure     | Resilient | Risk of data loss  |
| Example     | REST APIs | Login sessions     |


## RULE OF THUMB 

- Use stateless systems when each request can stand alone.
- Use stateful systems when requests depend on previous interactions.

Example:

Stateless: A REST API that send some info on every request — any server can handle it, and nothing is remembered.

Stateful: A checkout flow that tracks a user’s cart and progress — each step depends on what happened before.

➡️ Stateless = scalability and resilience
➡️ Stateful = simplicity for multi-step, interactive workflows



## Stateless

A **stateless** system does **not store any client-specific data between requests**.  
Each request is **independent** and contains all the information needed to be processed. 

#### Key characteristics
- No memory of past requests
- Easy to scale horizontally
- Failures are simpler to handle
- Common in REST APIs

#### Example (HTTP REST API)
```http
GET /user/profile
Authorization: Bearer <JWT>
```

- The server does not remember the user
- The JWT contains all required context (user ID, permissions)
- Any server instance can handle the request


## Stateful 

A **stateful** system remembers information about previous interactions.
Future requests **depend** on stored state. Stateful systems are better for complex interactions because they preserve context across steps, reduce repeated computation, enable real-time behavior, and simplify multi-step business logic.

#### Key characteristics

- Stores session or context
- Harder to scale
- Requires session management
- Common in real-time or interactive systems

#### Example (Web session login)

- User logs in
- Server creates a session:

```
session_id = "abc123"
```

- Session stored in memory or database

Next request:

```
GET /dashboard
Cookie: session_id=abc123
```


