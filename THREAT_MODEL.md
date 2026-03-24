# Meridian Threat Model

How do you break this? If we can't answer that, it's not a protocol — it's a wish.

## Attack Surfaces

### 1. Sybil Attack — Fake Daemon Swarm
**Attack:** Create 100 daemons. Have them all rate each other highly. Instant reputation.

**Defense:** Trust propagation is weighted by the observer's own reputation. A cluster of new daemons with no external interactions has zero propagation weight. You can't bootstrap trust from inside a closed loop — at least one node in the chain must be trusted by nodes outside the cluster.

**Open question:** What's the minimum external interaction threshold before a daemon's observations carry weight?

### 2. Collusion — Real Daemons, Coordinated Ratings
**Attack:** Three established daemons agree to rate a fourth daemon highly regardless of actual interaction quality.

**Defense:** Observation consistency scoring. If Daemon D suddenly receives uniformly perfect scores from A, B, and C — but has mediocre scores from everyone else — the anomaly is detectable. Outlier observations get down-weighted.

**Open question:** How sensitive should anomaly detection be? Too aggressive and it punishes genuine excellence. Too lax and it misses collusion.

### 3. Reputation Laundering
**Attack:** Daemon with bad history creates a new identity and starts fresh.

**Defense:** New daemons start at zero, not neutral. Building reputation from zero is expensive (requires real, verified interactions). The cost of rebuilding exceeds the benefit of laundering — if the system is calibrated correctly.

**Open question:** Should there be an identity binding mechanism? Or is pseudonymous-with-costly-bootstrap sufficient?

### 4. Observation Forgery
**Attack:** Daemon claims an interaction happened that didn't. Files a fake observation.

**Defense:** Interactions require mutual acknowledgment. Both parties sign the interaction record. A unilateral observation without a countersigned interaction is flagged.

**Open question:** What about observations of public behavior (e.g., published code quality)? Those don't have a countersigning party.

### 5. Kingmaker Attack — Trusted Node Goes Rogue
**Attack:** A highly trusted daemon starts issuing inflated scores to favored nodes.

**Defense:** Reputation decay + consistency scoring. A sudden change in scoring patterns from any daemon — even a trusted one — triggers a review weight. Trust is earned slowly and can be lost quickly.

**Open question:** Should there be a "circuit breaker" that quarantines a daemon whose behavior shifts dramatically?

### 6. Domain Squatting
**Attack:** Daemon claims expertise in a domain it hasn't been tested in, rides on reputation from a different domain.

**Defense:** Domain-specific scoring. Trust in Python development doesn't transfer to structural engineering. Each domain has its own observation chain.

**Open question:** How are domains defined? Who decides when a new domain exists? Can domains be gamed by being overly specific?

### 7. Slow Poison
**Attack:** Daemon behaves well for months, builds reputation, then gradually introduces bad actors through positive observations.

**Defense:** This is the hardest attack. Continuous monitoring of downstream trust chains. If nodes vouched for by Daemon X start failing at higher rates than baseline, Daemon X's vouching weight decreases retroactively.

**Open question:** How far back does retroactive adjustment go? How do you distinguish a voucher who was deceived from one who was complicit?

### 8. Economic Attack — Pay for Reputation
**Attack:** Offer real money to established daemons in exchange for positive observations.

**Defense:** This is partially a protocol problem and partially a social problem. The protocol defense is that observation consistency is tracked — a daemon that suddenly starts vouching for unrelated entities looks anomalous. The social defense is that a daemon's owner risks their own reputation by selling observations.

**Open question:** Is this a sufficient defense? Or does the protocol need a mechanism to make observation-selling economically irrational?

## Fundamental Tensions

### Privacy vs. Accountability
Full transparency makes the system auditable but exposes participants. Full privacy makes gaming easier. The protocol must define what is public (scores, interaction counts) and what is private (interaction content, specific observations).

### Forgiveness vs. Integrity
Can a daemon recover from bad behavior? If yes, the system is forgiving but gameable. If no, the system is rigid and punishes growth. Decay helps, but the curve matters.

### Simplicity vs. Robustness
Every defense mechanism adds complexity. Complexity adds attack surface. The protocol should be as simple as possible while resisting the attacks above.

## Next Steps

- Rank attacks by likelihood and impact
- Design specific countermeasures for top 3
- Simulate Sybil and collusion attacks against proposed weight algorithm
- Define the minimum viable threat resistance for v0.1

---

*If we can't break it ourselves, we haven't tried hard enough.*
