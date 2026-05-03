# Security That Works

### A Cognitive Redesign of Itaú's iToken Authentication System

**Author:** Bernardo Rodrigues Oliveira Carvalho
**Type:** Independent Academic Research
**Status:** Working Paper / Design Prototype — 2026

---

## Live Pages

This repository has three interactive pages hosted on GitHub Pages.
All run entirely in the browser — no installation, no backend.

### 🏠 [Landing Page](https://bernardo-r-o-carvalho.github.io/Itau-auth-redesing/)
`index.html`

Entry point for the project. Introduces the research question, presents the core argument, and links to the other two pages. Designed to be the URL you share when someone asks "what is this project?"

---

### 🔬 [Authentication Prototype](https://bernardo-r-o-carvalho.github.io/Itau-auth-redesing/itau_auth_prototype.html)
`itau_auth_prototype.html`

The main interactive prototype. Demonstrates the three-tier authentication model proposed in the paper:

- **Tier 1 — Passive:** Routine operation on a trusted device. No additional auth prompt. The system approves silently, preserving the user's attentional resources for operations that actually warrant them.
- **Tier 2 — Light biometric:** Mildly elevated risk signal (new payee, slightly above-baseline value). A single biometric confirmation (~3 seconds) is requested, with a visible explanation of why.
- **Tier 3 — Deliberate pause:** High-value transfer, unknown recipient, or anomalous session. Activates a 60-second countdown and sends a push notification to the user's pre-registered secondary device. The operation only proceeds after out-of-band confirmation — the only mechanism that directly interrupts the urgency states created by social engineering attacks.

Also demonstrates the **transparent device trust timeline** (Provisional → Standard status over 24–72h, with a fast-track video verification option) and a **risk score panel** showing the four signal categories in real time.

---

### 🧮 [Risk Calculator](https://bernardo-r-o-carvalho.github.io/Itau-auth-redesing/risk_calculator.html)
`risk_calculator.html`

Interactive companion to the paper's scoring model. Two modes:

**Calculator mode** — fill in a transaction scenario (amount, recipient, device status, time of day, behavioral pattern, location) and see the resulting risk score, tier decision, and a breakdown of how each signal contributed. The explanation updates in real time as you adjust the inputs.

**Signal Simulator mode** — adjust the six underlying signals independently via sliders to explore how they interact. Includes three pre-configured scenario presets: *Everyday use* (Tier 1), *Moderate signal* (Tier 2), and *Social engineering pattern* (Tier 3). Useful for presentations — lets you show an audience exactly which combination of signals crosses each threshold.

The scoring model implements the architecture proposed in the paper: six weighted signals summing to a score from 0–100, with Tier 2 activating at ≥40 and Tier 3 at ≥70. Weights are documented inline in the source code.

---

## Repository Contents

| File | Description |
|------|-------------|
| [`README.md`](./README.md) | This file |
| [`Security That Works.md`](./Security%20That%20Works.md) | Full research paper |
| [`index.html`](./index.html) | Landing page |
| [`itau_auth_prototype.html`](./itau_auth_prototype.html) | Authentication prototype |
| [`risk_calculator.html`](./risk_calculator.html) | Risk score calculator |

---

## The Research Paper

> [`Security That Works.md`](./Security%20That%20Works.md)

The paper covers:

- **Empirical grounding:** FEBRABAN 2024 data (R$10.1B in banking fraud losses; +17% YoY) and attack-type distribution from the Ministério da Justiça
- **Why cryptography is not the problem:** The three dominant fraud vectors (card cloning, false call centers, WhatsApp impersonation) all bypass cryptographic protections by manipulating the human operating them
- **Cognitive mechanisms:** Prefrontal cortex resource constraints under urgency, Kahneman's dual-process framework applied to authentication prompts, and Cialdini's urgency model as the mechanism enabling social engineering
- **The four failure modes of iToken:** Uniform friction, high-friction recovery paths, high-frequency authentication habituation, and opaque trust calibration
- **Detailed redesign:** Tier thresholds, risk signal composition, recovery paths, and device trust timeline

---

## Key Argument

The iToken system applies maximum friction uniformly across all operations regardless of actual risk level. This creates four predictable failure modes:

1. **Uniform friction** collapses the informational value of authentication requests
2. **High-friction recovery paths** create perverse incentives to maintain insecure configurations
3. **High-frequency authentication** triggers habituation, eliminating deliberate cognitive processing
4. **Opaque trust calibration** produces user disengagement

The proposed redesign implements a **three-tier risk-calibrated authentication architecture** in which friction is proportional to actual risk, high-value operations include a deliberate pause mechanism designed to break urgency states, and device trust building is transparent and user-controlled.

---

## Related Work

> Carvalho, B.R.O. (2025). *Digital Security as a Human Problem, Not a Technical One.* SSRN Working Paper. [ssrn.com](https://ssrn.com)

---

## Disclaimer

This is an independent academic research project conducted for educational and research purposes. It is **not affiliated with, endorsed by, or connected to Itaú Unibanco S.A.** in any way. All interface designs are hypothetical proposals. No proprietary data, internal systems, or confidential information were accessed or used.

---

## License

Shared for academic and educational purposes. If you use or reference this work, please cite the author.
