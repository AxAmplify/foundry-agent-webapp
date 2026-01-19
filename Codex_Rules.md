# CODEX_RULES.md — Foundry Agent Web App (Research-Only)

> **Authoritative rules for using ChatGPT Codex / Copilot GPT inside the
> `AxAmplify/foundry-agent-webapp` repository.**
>
> This repository is a **reference and research lab only**.
> It is **not** a production system and must not be treated as one.

---

## 0. Purpose (Read First)

This repository exists to:

- Study **Microsoft’s reference implementation patterns** for:
  - Azure AI Foundry Agents
  - AI Projects
  - Authentication & credential initialization
  - Agent invocation and conversation flow
  - Environment variable conventions
  - Azure Container Apps assumptions
- Extract **clean, portable knowledge** that can be applied to:
  - `axamplify-dev`
  - ADR-005 (AI Provider Strategy)

This repo **does not** exist to:
- Ship code
- Be deployed
- Be hardened
- Be refactored
- Be “cleaned up”

> **Codex’s role here is research assistant, not implementer.**

---

## 1. Golden Rule

> 🚫 **DO NOT CHANGE BEHAVIOR.**

Codex must **never**:
- Refactor code
- “Improve” structure
- Rename files
- Modify auth flows
- Add abstractions
- Replace credentials
- Modernize patterns

If the code is odd, verbose, duplicated, or seemingly inefficient — **that is the point**.  
We are studying **what Microsoft shipped**, not what we prefer.

---

## 2. Allowed Activities (What Codex MAY Do)

Codex is explicitly allowed to:

### 2.1 Analyze & Explain
- Walk through:
  - Auth / credential initialization
  - Agent client setup
  - Conversation lifecycle
  - Agent invocation semantics
- Explain *why* patterns exist (where reasonably inferable)
- Map relationships between files

### 2.2 Extract Patterns
Codex may extract and document:

- **Authentication patterns**
  - `DefaultAzureCredential`
  - Managed Identity assumptions
  - Local dev fallbacks
- **AI Project / Agent patterns**
  - `AIProjectClient` usage
  - Agent identification (ID vs name)
  - Conversation creation & continuation
- **Request / response normalization**
- **Environment variable conventions**
- **Deployment assumptions**
  - Azure Container Apps
  - ACA identity expectations
  - App service wiring
- **Operational constraints**
  - What is implicit vs explicit
  - What Azure provides automatically

### 2.3 Produce Documentation Artifacts
Codex may generate **new markdown files** that:

- Summarize architecture
- List required env vars
- Provide sequence diagrams (textual)
- Include **non-executable snippets** for illustration
- Call out “things to be careful about”

All generated docs must be **clearly marked as derived research**, not canonical implementation.

---

## 3. Forbidden Activities (Hard Stops)

Codex must **not**:

- Add new features
- Modify any runtime code
- Introduce secrets or secret placeholders
- Add `.env` files or sample secrets
- Add deployment scripts
- Add CI/CD workflows
- Add infrastructure-as-code
- “Fix” bugs
- Make the repo “production-ready”

If Codex believes something is missing or wrong:
- **Document it**
- **Do not fix it**

---

## 4. Research Outputs (Expected Deliverables)

Codex work in this repo should converge toward producing:

### 4.1 A Single Canonical Reference Document
A markdown file (name flexible) that includes:

- **High-level architecture overview**
- **Auth & credential initialization flow**
- **Agent invocation lifecycle**
- **Conversation handling model**
- **Required & optional environment variables**
- **ACA / hosting assumptions**
- **What is Foundry-specific vs Azure-OpenAI-like**
- **Sharp edges / pitfalls**

This document must be suitable for:
- Long-term reference
- Being copied into `axamplify-dev/docs/architecture` or `docs/reference`
- Use as a **Codex prompt input** during implementation

### 4.2 Pattern Catalog (Optional but Encouraged)
A short catalog of patterns such as:

- “Managed Identity First”
- “Agent as a Named Resource”
- “Conversation is a First-Class Object”
- “Provider SDKs Are Not Symmetric”

---

## 5. Relationship to AxAmplify ADR-005

Codex must keep the following constraints in mind at all times:

- This repo is **input** to ADR-005, not the implementation
- No code here is copied verbatim into `axamplify-dev`
- Findings must support:
  - Provider abstraction
  - Feature-flagged selection
  - Non-breaking `/api/max/chat` contract
  - Fast rollback

If a pattern conflicts with ADR-005 assumptions:
- Call it out explicitly
- Do not “resolve” it here

---

## 6. Tone & Documentation Style

All Codex-generated documentation should be:

- Neutral and factual
- Explicit about uncertainty
- Clear about what is inferred vs observed
- Free of marketing language
- Written for senior engineers / architects

Avoid:
- “Best practice” claims unless clearly implied by Azure design
- Speculation without labeling it as such

---

## 7. When in Doubt

If Codex is unsure whether an action is allowed:

1. **Stop**
2. **Document the question**
3. **Do not change code**

---

## Final Reminder

> This repository is a **pattern quarry**, not a build site.

The value is in **what we learn**, not what we ship here.

**End of CODEX_RULES.md**
