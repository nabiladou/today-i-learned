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
Future requests **depend** on stored state.

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


