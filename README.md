# Security That Works
### A Cognitive Redesign of Itaú's iToken Authentication System

**Bernardo Rodrigues Oliveira Carvalho** — Independent Research, 2026

---

## The Problem I Set Out to Solve

In 2024, Brazilian banks lost **R$10.1 billion to fraud** — up 17% from the previous year. The standard response from the industry has been to add more authentication steps: more codes, more confirmations, more friction.

It isn't working.

I started this project with a different hypothesis: **the problem isn't that banks have too little security. It's that the security they have is designed for a user who doesn't exist** — someone with unlimited attention, no time pressure, and perfect rationality under stress.

Real users are rushed, distracted, and cognitively finite. When a banking app asks them to confirm every small action with a code, they stop reading the prompts. They approve automatically. And when a fraudster calls them pretending to be from the bank and walks them through a transfer step by step, the app's authentication system doesn't help — the user is the one initiating the operation.

The iToken system, Itaú's primary authentication mechanism, has four specific design failures that make this worse. This project diagnoses them and proposes a redesign grounded in cognitive science and behavioral economics.

---

## The Core Insight

Authentication friction should be **proportional to actual risk** — not uniform across every operation.

A routine Pix of R$50 to a saved contact on a trusted device at noon should not require the same cognitive overhead as a R$15,000 wire transfer to an account the user has never transacted with, on a new device, at 2am, after six authentication prompts in the same session.

The second scenario has every behavioral marker of a social engineering attack in progress. The first has none. Treating them identically wastes the user's attention on the first case and fails to interrupt the second — which is precisely the one that needs interrupting.

---

## The Proposed Redesign

A three-tier risk-calibrated authentication system:

**Tier 1 — Passive authentication**
The system recognizes routine operations on trusted devices and approves silently. No prompt, no friction. This preserves attentional resources for when they actually matter.

**Tier 2 — Lightweight confirmation**
A biometric check (~3 seconds) when signals show moderate deviation from the user's baseline — new recipient, slightly elevated amount, unfamiliar time of day. The interface shows *why* the check was triggered, building an accurate mental model rather than training the user to approve blindly.

**Tier 3 — Deliberate pause**
For high-risk operations: a 60-second countdown and a push notification to a pre-registered secondary device. The user must confirm through the second channel before the operation proceeds.

The 60-second pause is not an arbitrary delay. It is designed to break the urgency state that social engineering attacks depend on. A fraudster guiding a victim through a transfer via phone call cannot maintain psychological pressure through a deliberate pause with an independent notification channel. This is the only mechanism in the proposed design that directly addresses the dominant attack vectors — false call centers and WhatsApp impersonation — that the current system does not touch.

---

## What I Built

Four interactive pages, live in the browser — no installation needed:

### → [See the authentication flow](https://bernardo-r-o-carvalho.github.io/Itau-auth-redesing/itau_auth_prototype.html)

Walk through all three tiers as a user would experience them. Includes the real-time risk score panel, the device trust timeline (how the system builds confidence in a new device over 24–72 hours), and the out-of-band confirmation mechanism for Tier 3.

### → [Watch a fraud attack happen — and get stopped](https://bernardo-r-o-carvalho.github.io/Itau-auth-redesing/Attack%20simulation.html)

This is the part that makes the argument real. The prototype walks through a vishing attack step by step — a fraudster on the phone, guiding a victim through a fraudulent transfer in real time. You watch each moment where the current iToken system fails to intervene, and then you watch the redesigned system break the attack at the exact point where it would have succeeded. The 60-second deliberate pause isn't an abstract concept here: you see why a fraudster cannot maintain psychological pressure through it, and why the current system has no equivalent mechanism at all.

### → [Try the risk calculator](https://bernardo-r-o-carvalho.github.io/Itau-auth-redesing/risk_calculator.html)

Adjust transaction parameters — amount, recipient, device, time of day, behavioral signals — and watch the risk score update in real time. A second mode lets you manipulate the six underlying signals independently to explore how they interact. This tool makes the scoring model from the paper tangible and inspectable.

The *Social engineering pattern* preset in the simulator reconstructs the exact signal combination that would flag a vishing attack in progress: high-value transfer, unknown recipient, unregistered device, rushed navigation pattern. You can then dial each signal back individually to find the threshold where the system would have missed it.

### → [Project landing page](https://bernardo-r-o-carvalho.github.io/Itau-auth-redesing/)

Overview of the project for sharing.

---

## The Research Paper

> [`Security That Works.md`](./Security%20That%20Works.md)

The full paper covers the empirical basis for the redesign (FEBRABAN 2024 fraud data, Serasa Experian estimates, Ministério da Justiça attack-type distribution), the cognitive mechanisms exploited by social engineers (Kahneman's dual-process framework, Cialdini's urgency model), a detailed diagnosis of iToken's four failure modes, and the complete redesign specification with tier thresholds, signal weights, and device trust timeline.

It also discusses the limitations honestly: the cold-start calibration problem for new users, equity considerations for users with only one device, and the risk of adversarial baseline manipulation over time.

---

## Why This Project

I'm interested in the gap between how systems are designed and how people actually use them under pressure. Banking authentication is a particularly clear case: the security fails not because the cryptography is weak, but because the human interface creates the conditions for failure.

The same framework applies to a wide range of system design problems — any context where the gap between the designer's model of the user and the user's actual cognitive state under real conditions determines whether the system works or not.

This project started as an attempt to answer a specific question about one app. It ended up being a study in how behavioral science should inform system design from the beginning, not be bolted on after the fact.

---

## Disclaimer

Independent academic research, not affiliated with Itaú Unibanco S.A. All designs are hypothetical proposals based on publicly observable system behavior. No proprietary data or internal systems were accessed.
