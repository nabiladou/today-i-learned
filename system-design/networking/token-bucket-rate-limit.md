# Token Bucket Cheat Sheet

**What it is:** Rate-limiting algorithm that allows bursts but limits average rate.

---

## How It Works
- Bucket holds **tokens** (permissions for requests)
- Tokens **added at a fixed rate** up to max capacity
- **Each request uses a token**
  - ✅ Token available → allow
  - ❌ No token → block/delay

---

## Key Parameters
- **Rate:** tokens/sec
- **Capacity:** max tokens in bucket
- **Cost:** tokens per request (usually 1)

---

## Example
- Rate = 1/sec, Capacity = 5
- After 5 sec idle → 5 requests allowed at once
- 6th request waits for next token

---

## Benefits
- Allows short bursts
- Enforces average rate
- Simple to implement

---

## Use Cases
- API rate limiting
- Network traffic shaping
- Login attempt throttling
- Cloud services (AWS, GCP, NGINX, Envoy)
