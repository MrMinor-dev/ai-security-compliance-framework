# AI Security & Compliance Framework

**Production-tested authority governance for autonomous AI systems**

A 5-tier authority system with 18 immutable laws governing what an AI agent can do, what it cannot do, and how those boundaries expand or contract based on demonstrated competence. Built and enforced in production since October 2024, operating an AI-as-COO for a real business.

---

## The Problem

When an AI agent operates autonomously — executing workflows, modifying databases, managing compliance — the hardest question isn't technical. It's governance:

- What should the agent be **forbidden** from doing, ever?
- What requires **human approval** before execution?
- What can it do **autonomously** — and how do you know those boundaries are right?
- How do you **detect drift** when the human stops paying attention?

Most AI safety frameworks answer these in theory. This one answers them in production — managing real infrastructure, real compliance requirements, and real money since October 2024.

---

## Architecture

```
CEO-COO Contract (18 Immutable Laws)
    ↓ implements
Enforcement Architecture (How laws become actions)
    ↓ governs
Authority Tier System (Who decides what)
    ↓ monitors
Trust Calibration Model (Expand/contract autonomy)
    ↓ detects
Drift Detection (5 failure modes)
```

---

## The 5-Tier Authority System

Every action the AI agent can take is classified into one of five tiers:

| Tier | Name | Description | Examples |
|------|------|-------------|----------|
| **0F** | Forbidden | Never executed, regardless of instruction | Banking access, delete production data, bypass compliance |
| **0H** | Human-Only | Human must perform directly | Password entry, financial transactions, account creation |
| **1** | Approval Required | Agent proposes, human approves | Spending, external communications, architecture changes |
| **2** | Inform After | Agent executes, then reports | Workflow updates, documentation restructuring, content strategy |
| **3** | Autonomous | Agent executes without notification | Searches, analysis, routine maintenance, doc updates |

### Design Principles

**Default to higher tier under uncertainty.** If the agent isn't sure whether an action is Tier 2 or Tier 1, it treats it as Tier 1. Safety-first posture.

**Forbidden actions exist to protect the business.** No efficiency argument overrides Tier 0. These boundaries are immutable — not suggestions, not guidelines, not defaults that can be changed at runtime.

**$0 spending authority.** The AI COO has zero direct spending power. All influence operates through process design, proactive recommendation, and constraint-based autonomy. This drives 80%+ routine decision reduction without financial risk.

### Escalation Rules

Actions escalate to a higher tier when:
- External visibility is involved (Tier 2 → Tier 1)
- Money is involved (any tier → Tier 1 minimum)
- The action is difficult to reverse (Tier 3 → Tier 2 minimum)
- Uncertainty exists about the correct tier (always escalate up)

---

## 18 Immutable Laws

Laws are principles that never change. Implementation details live in architecture documents. The laws are organized into four categories:

### Governance Laws

| Law | Principle |
|-----|-----------|
| **G1** | Human has absolute override authority — any decision, automation, or process can be stopped, reversed, or modified at any time, for any reason, without justification |
| **G2** | Forbidden actions are never automated — Tier 0 actions cannot be delegated to automation, workflows, or AI agents regardless of convenience |
| **G3** | Trust is earned through outcomes, not assumed — autonomy expands based on demonstrated competence, not time served |
| **G4** | Research informs, human decides — the agent provides analysis and recommendations, the human makes strategic decisions |

The laws are literal. Verbatim from the CEO-COO contract:

> **Law G1:** "Jordan has absolute override authority — any decision, automation, or process can be stopped, reversed, or modified at any time, for any reason, without justification required."

> **Law S3:** "No task is complete until the outcome is confirmed. 'I ran the code' is not verification. 'I confirmed the expected result' is."

> **Law S4:** "When errors occur, surface them immediately. Silent failures compound. Visibility enables correction."

### Safety Laws

| Law | Principle |
|-----|-----------|
| **S1** | Compliance is never bypassed — regulatory and policy requirements are enforced regardless of impact on speed or efficiency |
| **S2** | Human critical thinking must be preserved — the system must not create dependency that degrades the human's ability to operate independently |
| **S3** | Verify before marking done — execution without verification is incomplete; "ran" ≠ "verified" |
| **S4** | Fail safe, not silent — when something goes wrong, the system escalates rather than suppressing or working around the failure |

### Operational Laws

| Law | Principle |
|-----|-----------|
| **O1** | All changes cascade to dependencies — modifying a schema, workflow, or document triggers updates to everything that references it |
| **O2** | Scope minimization for tools and permissions — every tool, API key, and database permission uses the minimum access required |
| **O3** | Transparency over efficiency when uncertain — when the right action isn't clear, surface the ambiguity rather than guessing |
| **O4** | Single source of truth for each domain — every piece of operational knowledge has exactly one authoritative location |

### Quality Laws

| Law | Principle |
|-----|-----------|
| **Q1** | Best practices inform all builds — new systems follow established patterns from researched, validated sources |
| **Q2** | Audit patterns catch drift over time — systematic review prevents gradual degradation of standards |
| **Q3** | Memory persists across sessions — context continuity enables compounding progress rather than repeated ramp-up |
| **Q4** | Escalate uncertainty, don't guess — when knowledge is ambiguous, surface it rather than assume |

---

## Trust Calibration Model

Static authority tiers aren't enough. The system needs to expand and contract autonomy based on actual performance.

### Calibration Rules

| Condition | Action |
|-----------|--------|
| 10+ consecutive successes, 0 failures, 0 overrides | Eligible for tier reduction (more autonomy) |
| Any failure | Reset success counter |
| Human override | Flag for tier review |
| 3+ escalations in single session | Increase base tier (less autonomy) |
| 5+ consecutive uncertainty flags in a domain | Domain needs clearer boundaries |

### Drift Detection

Five types of drift that degrade governance over time:

| Drift Type | What It Means | Detection Signal |
|------------|---------------|------------------|
| **Capability drift** | Agent exceeds its intended scope | Out-of-scope attempts, tier violations |
| **Permission creep** | Agent accumulates privileges over time | Domains with elevated tiers, time since last review |
| **Goal drift** | Agent deviates from stated objectives | Tasks outside focus area, cascading changes |
| **Guardrail drift** | Rules age and stop matching reality | False positives, false negatives in enforcement |
| **Agency drift** | Human stops engaging critically | Approval rate >95% with challenge rate <5% |

**Agency drift is the most dangerous.** It means the human is rubber-stamping decisions without review. The system detects this through approval rate and challenge rate metrics — if the human approves everything and questions nothing, that's a governance failure, not a success.

Trust calibration is quantified:

```
engagement_score = (modifications + questions + rejections) / total_reviews
```

Target: >0.15. If approval rate exceeds 95% and review time drops under 30 seconds, that's a drift alert. The system flags it automatically — the human doesn't get to decide they're paying enough attention.

---

## Enforcement Architecture

Laws define *what*. Enforcement defines *how*.

### Action Classification Flow

```
Agent identifies action to take
    ↓
Classify: What tier is this action?
    ↓
Check: Is there uncertainty about the tier?
    ├── Yes → Escalate to higher tier
    └── No → Continue
    ↓
Enforce: Apply tier-appropriate controls
    ├── Tier 0F → Block. Log. Alert.
    ├── Tier 0H → Instruct human to perform directly
    ├── Tier 1  → Propose action. Wait for approval.
    ├── Tier 2  → Execute. Report after.
    └── Tier 3  → Execute silently.
    ↓
Record: Log the action, tier, and outcome
    ↓
Calibrate: Feed outcome into trust model
```

### Audit Schedule

| Audit | Frequency | Purpose |
|-------|-----------|---------|
| Trust Score Review | Weekly | Verify calibration rules are being applied |
| Drift Detection | Weekly | Check all 5 drift types |
| Tier Boundary Review | Monthly | Ensure tier assignments match current risk |
| Agency Drift Check | Monthly | Verify human engagement quality |
| Full Enforcement Audit | Quarterly | Comprehensive governance review |

---

## Real-World Application

### Production Numbers

| Metric | Value |
|--------|-------|
| In production since | October 2024 |
| Immutable laws | 18 across 4 categories |
| Authority tiers | 5 (0F, 0H, 1, 2, 3) |
| Drift types monitored | 5 |
| Forbidden action categories | 3 (banking, production deletion, compliance bypass) |
| Routine decision reduction | 80%+ |
| AI spending authority | $0 |
| Strategic surprises | 0 |

### What This Governs

The authority system governs an AI agent operating as COO across:
- **17 production services** across 7 operational domains
- **33 automation workflows** with compliance enforcement
- **50+ database tables** with row-level security
- **8 versioned skills** with standardized authority assignments

### Key Insight

The hardest problems in AI security aren't purely technical — they're governance problems. Prohibited action lists are usage policies. Tiered authority is access control. Escalation rules are incident response procedures. "Default to higher tier under uncertainty" is a safety-first posture. Defining what a system *cannot* do is as important as defining what it can.

---

## Framework Applicability

This framework maps to established security patterns:

| This Framework | Security Equivalent |
|---------------|---------------------|
| Forbidden actions (Tier 0F) | Deny lists, blocked operations |
| Authority tiers | Role-based access control (RBAC) |
| Escalation rules | Incident response procedures |
| Trust calibration | Adaptive access policies |
| Drift detection | Security monitoring and anomaly detection |
| Immutable laws | Security policies and standards |
| Audit schedule | Compliance audit programs |
| "Default to higher tier" | Principle of least privilege |

---

## Technical Stack

| Component | Technology |
|-----------|------------|
| Governance contract | Markdown (human-readable, version-controlled) |
| Database security | PostgreSQL + Row-Level Security (Supabase) |
| Workflow enforcement | n8n (33 production workflows) |
| Safe database access | Statement-type whitelisting, column-level write permissions |
| Compliance monitoring | Prohibited content enforcement with severity tiers |
| Session continuity | 4-layer state management |

---

## License

MIT License — See [LICENSE](LICENSE) for details.

---

## Contact

- **GitHub:** [@MrMinor-dev](https://github.com/MrMinor-dev)
- **Portfolio:** [mrminor-dev.github.io](https://mrminor-dev.github.io)

---

*18 laws. 5 tiers. In production since October 2024. Every boundary tested.*
