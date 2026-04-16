# PhoneOut Demo Call Flow

> Text description of the diagram [phoneout-demo-flow-2026-03-27.html](phoneout-demo-flow-2026-03-27.html)

---

## Why This Diagram

PhoneOut gives new users 2 free demo calls per special number before asking for payment. This diagram maps the entire journey from `/start` to the 300⭐ invoice, including the Rickroll easter egg logic.

## What Each Stage Means

1. **Welcome** — user opens the bot, receives greeting with avatar, 2 call buttons (Louvre + Rickroll), and a delayed tip about sending phone numbers

2. **Louvre Calls (2×)** — two free calls to +33140205317. Each call goes through: `demo_check` (Redis) → Twilio WebRTC (50s max) → `demo_use` (Redis INCR) → bot summary message

3. **Rickroll Calls (2×)** — two free calls to +12484345508. Same flow as Louvre, plus: on the **first** Rickroll call, `notify.js` checks `rickroll_sent` flag in Redis. If null → sends photo + caption easter egg, sets flag to `1`. Second call — flag exists, photo skipped

4. **Payment Wall** — on the 5th call attempt (any demo number), `demo_check` returns `free: false`. App shows 5-second timer, then opens a Telegram Stars invoice for 300⭐

---

## Full Flow

### 1. Start: /start
User opens the bot → Welcome block with greeting + 2 buttons + delayed tip.

### 2. Louvre Call #1
User taps "Call 🇫🇷 Louvre". `demo_check` returns `used: 0 < 2 → free: true`. Twilio WebRTC call starts (max 50s). After call: `demo_use` increments counter to 1. Bot sends summary: phone in monospace, country, duration, stars, balance, friendly message #1.

### 3. Louvre Call #2
Same flow. `demo_check` returns `used: 1 < 2 → free: true`. Counter increments to 2. Bot sends friendly message #2.

### 4. Rickroll Call #1
User calls +12484345508. `demo_check` for this number: `used: 0 < 2 → free: true`. Twilio call. After call: counter increments to 1 (separate counter per number). Bot sends summary with friendly message #3. **Additionally:** `notify.js` detects `12484345508` in text, checks Redis `rickroll_sent` flag → null → sends photo with Rick Astley caption → sets flag to `1`.

### 5. Rickroll Call #2
Same flow. Counter increments to 2. Bot sends friendly message #4 ("Last freebie!"). `notify.js` checks `rickroll_sent` → `1` → skips photo.

### 6. Call #5 — Payment Wall
User tries any demo number. `demo_check` returns `used: 2 ≥ 2 → free: false`. `isDemo = false`, `balance = 0`. Guard condition `balance ≤ 0 AND !isDemo` triggers. 5-second countdown → `endCall()` → `openStarsPayment(300)` → Telegram Stars invoice for 300⭐ (30 min US calls).

---

## External Services

| Service | Role | Connection |
|---------|------|------------|
| **Twilio** | WebRTC + PSTN gateway | All 4 real calls |
| **Upstash Redis** | Demo counters + rickroll flag | demo_check (GET), demo_use (INCR), rickroll_sent (GET/SET) |
| **Telegram Bot API** | User messaging | sendMessage (summaries), sendPhoto (easter egg) |

---

## Key Numbers

| Parameter | Value |
|-----------|-------|
| Free calls per demo number | 2 |
| Demo auto-cutoff | 50 seconds |
| Demo numbers | +33140205317, +12484345508 |
| Rickroll photo sends per user | 1 (ever) |
| Post-demo invoice | 300⭐ |
| Friendly message variants | 4 (RU/EN) |

---

## Full Pipeline in One Line

**/start → Welcome (2 buttons + tip) → 2× Louvre (free) → 2× Rickroll (free + easter egg once) → Payment Wall (300⭐ invoice)**
