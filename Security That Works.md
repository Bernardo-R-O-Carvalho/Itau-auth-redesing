# Security That Works
### A Cognitive Redesign of Itaú's iToken Authentication System

*Bernardo Rodrigues Oliveira Carvalho · Independent Researcher · 2026*

---

In November 2023, a Brazilian Itaú customer documented a security paradox on Reclame Aqui. He had acquired a new laptop, installed the bank's official application, and followed every recommended procedure. The system then required iToken verification via QR code scan for every single operation — including viewing his income tax statement. After weeks of this, a bank representative told him the system needed to "learn that he was him" through repeated use. There was no defined timeline. The customer described the experience as the bank telling him: *"you are not you."*

This is not an edge case. It is the system working exactly as designed.

---

## The Actual Problem

Banking fraud caused R$10.1 billion in losses in Brazil in 2024 — a 17% increase over 2023, according to FEBRABAN. Pix fraud alone grew 43% over two years. Serasa Experian estimated that prevented fraud attempts, had they succeeded, would have totaled R$51.6 billion. By early 2024, 36% of Brazilians had been victims of fraud or attempted fraud, with people over 60 consistently identified as the most vulnerable group.

The three most common attack types: card cloning or physical swap (44% of incidents), false bank call center impersonation (32%), and WhatsApp money requests posing as known contacts (31%).

None of these attacks break the underlying security protocols. All three work by manipulating the human operating those protocols. False call centers work because the caller creates urgency that bypasses deliberate evaluation. WhatsApp scams work because social familiarity disarms skepticism. Card swaps work because a distracted customer hands over their card.

The iToken system was designed to stop a different threat — a remote attacker attempting to authenticate without valid credentials. Against the actual threat — a legitimate user being manipulated into performing an action they would not endorse under calm reflection — it provides no protection. And as this document argues, it actively degrades the user's capacity to recognize and resist manipulation.

False call center scams doubled in the first half of 2025 alone (CNN Brasil / BioCatch, 2025). The pattern is consistent: fraudsters walk users through every authentication step, bypassing biometrics, passwords, and OTP codes entirely — because the user performs them voluntarily under social pressure. Designing authentication systems that ignore this is not a technical decision. It is a choice to protect against the wrong threat.

---

## Why the iToken Fails

The iToken's underlying cryptographic mechanism — a time-based one-time password rotating every 20 seconds — is sound. The failure is behavioral. The system applies maximum friction uniformly across all operations regardless of risk level. A user checking their balance and a user authorizing a R$50,000 wire transfer encounter the same authentication barrier.

This creates four predictable failure modes.

**Uniform friction collapses the informational value of authentication.** When every operation triggers the same response, users cannot distinguish genuine threats from routine processes. Everything is equally urgent; therefore, nothing is.

**High-friction recovery paths create perverse incentives.** When iToken fails — facial recognition errors, device changes, travel — recovery requires physical presence at an ATM. Users who know this will resist updating devices, avoid traveling, and accept known security problems rather than triggering the recovery process. The secure path becomes the inconvenient one.

**High-frequency authentication triggers habituation.** Behavioral research establishes that repeated identical stimuli produce decreasing neural response over time. An authentication system generating 8–12 verification requests per session is not creating 8–12 moments of deliberate security evaluation. It is creating a habituated response pattern in which anomalous requests — the kind embedded during social engineering — become invisible.

**Opaque trust calibration produces disengagement.** The system builds behavioral trust models through passive observation but communicates nothing about this process to the user. From the user's perspective, the system is opaque and apparently arbitrary. The rational response to an opaque system is to minimize engagement with it — which is the opposite of the attentive behavior that makes authentication effective.

These are not failures of user behavior. They are the predictable consequences of design decisions that treat the user as an obstacle to route around rather than a participant to design for.

---

## The Cognitive Framework

The theoretical foundations of this analysis are developed in *Digital Security as a Human Problem, Not a Technical One* (Carvalho, 2025). Three mechanisms are directly relevant here.

The prefrontal cortex — responsible for careful, sequential analysis — is resource-constrained and fatigable. After the hundredth iToken prompt for a routine operation, it is no longer engaged. The user has learned, correctly from a behavioral conditioning standpoint, that the prompt requires compliance rather than evaluation. This is not negligence. It is the inevitable outcome of a system that generates false positives at a rate that overwhelms deliberate processing capacity.

Kahneman's research on cognitive effort established that when a behavior requires effort exceeding its perceived benefit, people will reliably seek the path of least resistance. Friction is only a security benefit when it is proportional to risk. Friction on a low-risk operation trains avoidance. A system that cannot distinguish between the two will erode its own effectiveness as users develop tolerance or workarounds.

Cialdini's work on influence identifies urgency and time pressure as the primary mechanisms through which social engineers bypass deliberate cognition. An authentication system that applies uniform friction regardless of risk does nothing to interrupt urgency states — it normalizes them. The user conditioned to approve authentication requests quickly, without deliberate evaluation, is precisely the user who will approve a fraudulent request during a social engineering attack.

---

## The Redesign

The proposed system replaces the uniform iToken trigger with a three-tier architecture. Each tier is triggered by the risk profile of the specific operation, calculated in real time.

| Tier | Conditions | Mechanism |
|---|---|---|
| **Tier 1 — Passive** | Trusted device, routine operation, value within normal range | No additional authentication |
| **Tier 2 — Lightweight** | New recipient, or value modestly above baseline | Single biometric confirmation (~3 seconds) |
| **Tier 3 — Deliberate** | High value, new payee, anomalous pattern, or unfamiliar device | Out-of-band verification + 60-second deliberate pause |

The risk score that determines the tier is calculated from four signal categories: device trust (time since registration, historical usage), transaction risk (value relative to norms, recipient familiarity), session context (time since last verified action, operation count), and behavioral anomaly (deviations from established patterns in timing, location, and operation sequences).

This score is not opaque. The interface communicates the current trust level of the session and the approximate reason for any elevated request. This makes anomalous requests visible rather than normalized.

### The Deliberate Pause

For Tier 3 operations, the system implements a human-in-the-loop design: the operation is not processed until a specific deliberate action has been taken through a channel independent from the one initiating the request. When a Tier 3 operation is initiated, the user receives a notification on their pre-registered secondary device stating the specific operation, its value, the recipient, and the time it was initiated. The primary device displays a 60-second countdown during which the operation can be confirmed or cancelled.

This design exploits a key property of social engineering attacks: they depend on urgency. An attacker who has manipulated a user into initiating a fraudulent transfer cannot maintain the psychological pressure required during a 60-second deliberate pause. The pause is not a barrier in the traditional cryptographic sense — it is a behavioral state reset that gives the user time to evaluate what they are actually authorizing.

### Transparent Device Trust

When a new device is registered, the user sees an explicit timeline:

- **Hours 0–24:** Device is provisional. Tier 3 required for operations above R$500.
- **Hours 24–72:** Device reaches standard status after one verified Tier 3 operation.
- **Active option:** Standard status immediately via 5-minute in-app video verification — no physical presence required.

This eliminates the "the system is learning" experience entirely. The user knows exactly what state they are in and has agency over the timeline.

### Recovery

| Path | Method | Time |
|---|---|---|
| Primary | Verification through pre-registered secondary device | ~5 minutes |
| Secondary | Video verification with bank representative, in-app | ~15 minutes, 24/7 |
| Tertiary | In-person at branch or ATM | For users without digital access |

When recovery is a 15-minute remote process with a defined timeline, users no longer have rational motivation to maintain insecure configurations to avoid it.

---

## Why This Works

Each design decision maps to a specific behavioral mechanism.

Tiered friction restores informational value. Tier 3 triggers are rare and specific — users recognize them as meaningful because they are not the default. The behavioral baseline uses the brain's pattern-recognition systems constructively — familiar operations are approved without friction, which means that when friction appears, it carries signal.

The 60-second pause breaks the urgency states that bypass prefrontal processing. Transparent trust levels give users accurate mental models of the system — predictable systems produce engaged users; opaque systems produce frustrated ones who minimize interaction. Remote recovery eliminates perverse incentives to maintain insecure configurations.

Out-of-band secondary channel confirmation means that attacker access to one channel does not enable the operation. This is the single design feature that directly addresses the dominant attack vectors — false call centers and social engineering — that the current system does not touch at all.

---

## Limitations

The risk calibration algorithm requires behavioral data to establish meaningful baselines. False positives during early deployment could reproduce the habituation problem this system is designed to solve — a phased rollout with conservative Tier 3 thresholds is recommended.

The secondary channel confirmation assumes users have registered a secondary device. Users with a single device require an alternative Tier 3 path, which is a meaningful equity consideration given the economic profile of many Brazilian banking customers.

Behavioral baselines may be manipulated by sophisticated attackers who conduct low-value reconnaissance operations before initiating high-value attacks. Risk models must account for temporal pattern shifts, not just cross-sectional deviation.

---

## Conclusion

The iToken system's failures are not evidence that Brazilian bank customers are insufficiently security-conscious. They are evidence that the system was designed by people who understood the threat model but not the user model.

A system that calibrates friction to actual risk, creates deliberate pauses for high-value operations, builds transparent trust models, and provides accessible recovery paths is more secure than the current system — not despite reducing uniform friction, but because of it. Security that users work around provides no protection. Security that users engage with, because it is proportional and intelligible, provides genuine protection.

The Reclame Aqui user who was told "the system needs to learn that you are you" was not a user of the security system. He was a subject of it.

---

## References

Carvalho, B.R.O. (2025). Digital security as a human problem, not a technical one. SSRN.

Cialdini, R.B. (2007). *Influence: The psychology of persuasion.* Harper Business.

Cranor, L.F. (2008). A framework for reasoning about the human in the loop. *Proceedings of UPSEC 2008.*

FEBRABAN (2025). *Pesquisa FEBRABAN de Tecnologia Bancária 2025.*

Kahneman, D. (2011). *Thinking, fast and slow.* Farrar, Straus and Giroux.

Ministério da Justiça e Segurança Pública (2024). *Pesquisa Nacional de Fraudes 2024.*

Rose, S., Borchert, O., Mitchell, S., & Connelly, S. (2020). Zero trust architecture (NIST SP 800-207). NIST.

Serasa Experian (2024). *Indicador de Tentativas de Fraude no Brasil — 2024.*

---

*This is an independent academic research project conducted for educational and research purposes. Not affiliated with Itaú Unibanco S.A. All interface designs are hypothetical proposals. No proprietary data or internal systems were accessed.*
