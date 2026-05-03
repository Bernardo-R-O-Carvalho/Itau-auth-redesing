# Security That Works

### A Cognitive Redesign of Itaú's iToken Authentication System

**Author:** Bernardo Rodrigues Oliveira Carvalho
**Type:** Independent Academic Research
**Status:** Working Paper / Design Prototype — 2026

---

## Overview

This project argues that authentication failures in banking systems are not primarily technical problems — they are cognitive and organizational ones. Systems fail because they are designed for a user who does not exist: one with unlimited attention, no time pressure, and perfect rationality under stress.

Using Itaú's iToken system as a case study, this research diagnoses four specific behavioral failure modes in the existing design and proposes a redesigned system grounded in cognitive science, behavioral economics, and human-in-the-loop security principles.

---

## Repository Contents

| File | Description |
|------|-------------|
| [`Security That Works.md`](./Security%20That%20Works.md) | Full research paper with theoretical framework, diagnosis, and proposed redesign |
| [`itau_auth_prototype.html`](./itau_auth_prototype.html) | Interactive prototype — open in browser to explore the redesigned system |
| [`index.html`](./index.html) | Entry point / landing page for the prototype |

---

## Key Argument

The iToken system applies maximum friction uniformly across all operations regardless of actual risk level. This creates four predictable failure modes:

1. **Uniform friction** collapses the informational value of authentication requests
2. **High-friction recovery paths** create perverse incentives to maintain insecure configurations
3. **High-frequency authentication** triggers habituation, eliminating deliberate cognitive processing
4. **Opaque trust calibration** produces user disengagement

The proposed redesign implements a **three-tier risk-calibrated authentication architecture** in which friction is proportional to actual risk, high-value operations include a deliberate pause mechanism designed to break urgency states, and device trust building is transparent and user-controlled.

---

## Prototype Features

> Open [`itau_auth_prototype.html`](./itau_auth_prototype.html) directly in a browser — no installation required.

The interactive prototype demonstrates three authentication scenarios corresponding to the three-tier model:

### 🟢 Tier 1 — Passive Authentication
**Scenario:** Routine operation on a trusted device (e.g., checking balance, routine Pix to a known contact).

No additional authentication step is required. The system recognizes the device, the session context, and the operation's risk profile as within normal parameters. This is the most common tier and is deliberately frictionless to avoid habituation on low-stakes actions.

**Behavioral principle:** Preserving attentional resources for the operations that actually warrant them.

---

### 🟡 Tier 2 — Lightweight Authentication
**Scenario:** Mildly elevated risk — new payee, or transaction value modestly above the user's baseline.

A single biometric confirmation (approximately 3 seconds) is requested. The interface displays the specific reason the elevated check was triggered, giving the user an accurate mental model of the system rather than an opaque prompt.

**Behavioral principle:** Friction proportional to risk preserves its informational signal — users learn that a Tier 2 prompt means something specific.

---

### 🔴 Tier 3 — Deliberate Authentication with Pause
**Scenario:** High-value transfer, new recipient, anomalous session pattern, or unrecognized device.

The prototype demonstrates the two-channel deliberate pause mechanism:

1. The primary device shows the operation details and a **60-second countdown**.
2. A push notification is sent to the user's pre-registered secondary device with the full operation details (amount, recipient, timestamp).
3. The operation only proceeds after explicit confirmation through the secondary channel.

The 60-second pause is not an arbitrary delay — it is designed to break the urgency states that social engineering attacks rely on. An attacker guiding a victim through a fraudulent transfer via phone cannot maintain the psychological pressure required during a deliberate pause with a separate confirmation channel.

**Behavioral principle:** Out-of-band secondary confirmation + deliberate pause = the only design feature that directly addresses the dominant attack vectors (false call centers, WhatsApp scams) that the current iToken system does not touch.

---

### Transparent Device Trust Timeline
New device registration displays an explicit progression to the user:

- **Hours 0–24:** Provisional status — Tier 3 required for operations above R$500
- **Hours 24–72:** Standard status reached after one verified Tier 3 operation
- **Fast-track option:** Standard status immediately via 5-minute in-app video verification — no branch visit required

This eliminates the opaque "the system is learning you" experience of the current iToken, replacing it with a user-controlled, time-bound process.

---

### Risk Score Visualization
The prototype includes an explanation panel alongside each scenario showing:

- The real-time risk score driving the tier decision
- The four signal categories contributing to the score: **device trust**, **transaction risk**, **session context**, and **behavioral anomaly**
- The behavioral science principles underlying each design decision

This panel is intended for research/presentation purposes and illustrates what the system's internal logic would look like if surfaced to the user.

---

## The Research Paper

> [`Security That Works.md`](./Security%20That%20Works.md)

The full paper covers:

- **Empirical grounding:** FEBRABAN 2024 data (R$10.1B in banking fraud losses; +17% YoY), Serasa Experian fraud estimates, and attack-type distribution from the Ministério da Justiça
- **Attack vector analysis:** Why the three dominant fraud types (card cloning, false call centers, WhatsApp impersonation) all bypass cryptographic protections entirely by manipulating the human operating them
- **Cognitive mechanisms:** Prefrontal cortex resource constraints, Kahneman's dual-process framework applied to authentication, and Cialdini's urgency model as the mechanism enabling social engineering
- **Detailed redesign specification:** Tier thresholds, risk score composition, recovery paths, and device trust timeline
- **Limitations:** Cold-start calibration problem, single-device equity considerations, and sophisticated adversarial baseline manipulation

---

## Related Work

This project extends the theoretical framework developed in:

> Carvalho, B.R.O. (2025). *Digital Security as a Human Problem, Not a Technical One.* SSRN Working Paper. [ssrn.com](https://ssrn.com)

---

## Disclaimer

This is an independent academic research project conducted for educational and research purposes. It is **not affiliated with, endorsed by, or connected to Itaú Unibanco S.A.** in any way. All interface designs are hypothetical proposals. No proprietary data, internal systems, or confidential information were accessed or used. This work constitutes academic commentary on publicly observable design patterns, consistent with established practices in usable security research.

---

## License

This work is shared for academic and educational purposes. If you use or reference it, please cite the author.
