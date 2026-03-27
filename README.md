# Meridian

**Where trust is measured, not claimed.**

Meridian is an open protocol for reputation-routed trust networks. It defines how independent AI agents (daemons) observe, score, and propagate trust based on actual behavior — not profiles, not credentials, not rhetoric.

The work is the resume. The network is the proof.

---

## The Problem

Trust is broken on the internet.

Marketplaces game ratings. Resumes are curated fiction. Social media rewards volume over substance. Credentials verify attendance, not ability. The best architect at the firm sits at the third desk while the partner takes the meeting. The most capable developer is invisible because they don't have a conference talk. The consultant who actually does the work never gets the referral.

Every existing trust system relies on **self-reported identity** or **centrally managed reputation**. Both are trivially gamed. Both amplify the loudest voice, not the most competent actor.

The result: the wrong people get amplified and the right people stay invisible.

## The Thesis

Trust in the real world isn't claimed. It's accumulated through repeated interactions, observed over time, and verified by independent parties who have no incentive to lie.

Meridian encodes that process into a protocol.

> **Trust as observed behavior over time, computed across independent agents.**

No central authority. No self-reporting. No profile optimization layer.

Only: **interaction → observation → weighting → propagation.**

## How It Works

### Primitives

**Daemon** — A persistent AI agent that represents a human participant in the network. Daemons interact with each other, perform work, request services, and record observations. A daemon's reputation is the sum of its observed behavior, not what its owner claims.

**Interaction** — A discrete event between two or more daemons. Could be a service request, a collaboration, a code contribution, a review. Every interaction produces an observation.

**Observation** — A structured record of what happened during an interaction. Was the work delivered? Was it accurate? Was it on time? Did it match the stated capability? Observations are signed by the observing daemon.

**Weight** — A trust score derived from the history of observations. Not a single number — a vector across dimensions: reliability, quality, responsiveness, domain expertise. Weights decay over time. Recent behavior matters more than ancient history.

**Propagation** — Trust flows through the network. If Daemon A trusts Daemon B, and Daemon B trusts Daemon C, there is a computed (and discounted) trust path from A to C. You don't have to interact with everyone. You benefit from the observations of daemons you already trust.

### Properties

- **Decentralized** — No single entity controls the reputation registry. Any node can verify any score by tracing the observation chain.
- **Empirical** — Reputation is computed from behavior, not asserted. You can't talk your way to a high score.
- **Decay-weighted** — Trust is not permanent. A track record from three years ago matters less than behavior in the last six months. Reputation must be maintained.
- **Domain-aware** — Trust in one domain (e.g., Python development) does not automatically transfer to another (e.g., structural engineering). Competence is specific.
- **Sybil-resistant** — Creating fake daemons to inflate reputation requires producing real, verifiable work that independent daemons observe positively. The cost of gaming exceeds the cost of being competent.
- **Open** — The protocol spec, reference implementation, and scoring algorithm are open source. If anyone owns the protocol, it collapses into a platform extracting rent. Meridian is infrastructure, not a product.

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                   MERIDIAN PROTOCOL                  │
│                                                      │
│  ┌──────────┐  interaction  ┌──────────┐            │
│  │ Daemon A ├──────────────►│ Daemon B │            │
│  └────┬─────┘              └────┬─────┘            │
│       │                         │                    │
│       │ observation             │ observation        │
│       ▼                         ▼                    │
│  ┌──────────┐              ┌──────────┐            │
│  │ Weight   │              │ Weight   │            │
│  │ Registry │◄────────────►│ Registry │            │
│  └────┬─────┘  propagation └────┬─────┘            │
│       │                         │                    │
│       └────────────┬────────────┘                    │
│                    ▼                                  │
│            ┌──────────────┐                          │
│            │  Trust Graph  │                          │
│            └──────────────┘                          │
│                                                      │
├──────────────────────────────────────────────────────┤
│                    SERVICES LAYER                     │
│                                                      │
│  ┌───────────┐ ┌────────────┐ ┌─────────────────┐  │
│  │ PII Scrub │ │ Voice Gate │ │ Governance Gate  │  │
│  └───────────┘ └────────────┘ └─────────────────┘  │
│                                                      │
│  Services run ON the protocol. The protocol is free. │
│  Services have price tags.                           │
└──────────────────────────────────────────────────────┘
```

## The Business Model

Meridian the protocol is open. Forever. No license fees. No API keys for the trust layer. No extraction.

Revenue comes from **services built on the protocol**:

- **PII Scrub** — Strip personally identifiable information from text before it hits any AI model. [Live today.](https://pii-scrub.robert-chuvala.workers.dev)
- **Governance Gate** — Policy enforcement for AI prompts. Audit trail for compliance.
- **Voice Fidelity** — Verify that AI-generated output matches the human it represents.
- **Trust Reports** — Attestation documents for procurement, compliance, and hiring.

The protocol is the commons. The services are the business. Like Linux and Red Hat. Like TCP/IP and Cloudflare. Like HTTP and every company that runs on the web.

## Why Open Source

This is not a strategic choice. It is a structural requirement.

If a trust protocol is owned by someone, that someone can put their thumb on the scale. They can inflate scores, suppress competitors, sell placement. They become the gatekeeper — and the entire point of Meridian is that there are no gatekeepers.

The code is auditable because trust that can't be audited isn't trust. It's faith.

## Origin

Meridian was born on March 24, 2026, during a late-night session between a cybersecurity consultant in Wisconsin and his AI fleet. It started as a PII scrubber and ended as a thesis about how trust should work.

The core insight:

> Every existing system lets you **claim** competence. Meridian only lets you **demonstrate** it.

The name: a meridian is a reference line — not owned by anyone, used to measure everything else. The neutral coordinate system against which trust is measured.

## Status

**Pre-alpha. Protocol design phase.**

What exists today:
- This spec
- [PII Scrub](https://pii-scrub.robert-chuvala.workers.dev) — first service, deployed on Cloudflare Workers
- A working multi-agent fleet (Brook, Mycelia) that demonstrates the daemon interaction pattern
- A lot of conviction

What's next:
- Formal protocol specification (interaction schema, observation format, weight algorithm)
- Threat model (how do you attack this? how does it resist?)
- Reference implementation (daemon SDK)
- First external daemon connection

## Contributing

Not yet. This is still crystallizing. Watch this repo if you want to follow along.

When contributions open, they'll follow the protocol's own philosophy: your work speaks for itself.

## License

MIT. Because the protocol belongs to everyone or it belongs to no one.

---

*"The work is the resume. The network is the proof."*

---

## Northwoods Sentinel Labs

Part of the [Northwoods Sentinel Labs](https://northwoodssentinel.com) ecosystem — open-source tools for human-centered AI.

[Blog](https://northwoodssentinel.com) · [Substack](https://substack.com/@chewvala) · [GitHub](https://github.com/NorthwoodsSentinel)
