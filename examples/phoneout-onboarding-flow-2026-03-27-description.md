# PhoneOut Onboarding Flow

> Text description of the diagram [phoneout-onboarding-flow-2026-03-27.html](phoneout-onboarding-flow-2026-03-27.html)

---

## Why This Diagram

PhoneOut gives new users 2 free demo calls per special number before asking for payment. If a user calls any non-demo number at any point (balance = 0), they immediately hit a 300⭐ payment wall. This diagram maps the complete onboarding journey.

---

## Full Flow

### 1. Start: /start
User opens the bot → Welcome greeting + 2 buttons (Louvre + Rickroll) + 2-second delayed tip.

### 2. User Choice
After welcome, user either:
- **Dials a demo number** → enters the free calls flow
- **Dials any other number** → immediately hits the payment wall (Non-Demo Number block)

### 3. Non-Demo Number (any time, balance = 0)
User dials a number not in `DEMO_NUMBERS`. `isDemo = false`, `balance = 0`. Guard triggers → 5s timer → `endCall()` → `openStarsPayment(300)`. This can happen at any point during onboarding — dotted arrows show this path is available after every demo call.

### 4. Louvre Call #1
`demo_check` → `used: 0 < 2 → free: true`. Twilio WebRTC call (max 50s). After call: `demo_use` INCR counter to 1. Bot sends summary with friendly message #1.

### 5. Louvre Call #2
`demo_check` → `used: 1 < 2 → free: true`. Counter to 2. Friendly message #2.

### 6. Rickroll Call #1
`demo_check` for +12484345508: `used: 0 < 2 → free: true`. After call: counter to 1. Bot sends summary #3. **Easter egg:** `notify.js` checks `rickroll_sent` → null → sends photo + caption → sets flag to `1`.

### 7. Rickroll Call #2
Counter to 2. Friendly message #4 ("Last freebie!"). Easter egg: `rickroll_sent = 1` → skip photo.

### 8. Call #5 — Payment Wall (demo exhausted)
`demo_check` → `used: 2 ≥ 2 → free: false`. Same payment wall as non-demo: 5s → 300⭐ invoice.

---

## Key Numbers

| Parameter | Value |
|-----------|-------|
| Free calls per demo number | 2 |
| Demo auto-cutoff | 50 seconds |
| Demo numbers | +33140205317, +12484345508 |
| Rickroll photo per user | 1 (ever) |
| Post-demo / non-demo invoice | 300⭐ |
| Friendly messages | 4 variants (RU/EN) |

---

## Full Pipeline in One Line

**/start → Welcome → [Demo number: 2× Louvre + 2× Rickroll (+ easter egg)] OR [Non-demo number: instant payment wall] → 300⭐ invoice**
