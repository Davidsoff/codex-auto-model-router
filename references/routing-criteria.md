# Routing criteria

Choose a semantic task lane from task evidence, then resolve it through the selected `economy`, `balanced`, or `quality` table and three-model catalog. `balanced` is the default and preserves the original table. See [benchmark evidence](benchmark-evidence.md) for the supplied Artificial Analysis graph and its limits. The older GPT-5.6 snapshot is retained as history and does not calibrate these routes.

Assess and Retune default to GPT-6.1 Sol/high. Supported explicit model and effort overrides win. Recommendations remain advisory until execution is observed; the coordinator model stays fixed, and a routed leaf runs as a separate task.

## Model tiers and automatic lanes

| Work | Route |
|---|---|
| Mechanical and deterministic work | GPT-6 Luna/medium |
| Ordinary bounded implementation | GPT-6 Luna/high |
| Large bounded scans or reviews | GPT-6 Luna/xhigh |
| Deep deterministic work | GPT-6 Luna/max |
| latency_priority compatibility lane | GPT-6 Luna/max; cost/value choice, not a speed claim |
| Bounded complex work | GPT-6.1 Sol/low |
| High ambiguity or coupling | GPT-6.1 Sol/medium |
| High-consequence work | GPT-6.1 Sol/high in balanced; GPT-6 Astra/high in quality |
| Classified reasoning or verification failure on complex work | GPT-6.1 Sol/xhigh in balanced; GPT-6 Astra/xhigh in quality |

Sol/max remains available only by explicit override. Ultra is never automatic; explicit Ultra uses native orchestration and disables Router-managed parallelism. Luna does not support Ultra.

## Route validation and fallback

The routable IDs are gpt-6-astra, gpt-6.1-sol, and gpt-6-luna. The shorthand `astra` means GPT-6 Astra and `sol` means GPT-6.1 Sol. Reject retired GPT-6 Sol, GPT-5.6, and GPT-5.5 as route requests. Preserve historical names when reading prior ledger entries or coordinator metadata.

When Luna or Astra is unavailable, its lane may use Sol at the same effort. Sol routes never fall back to another model. If Sol is unavailable, retain the preferred recommendation and follow the normal local fail-open behavior. GPT-5.5 is never an availability fallback. Unknown availability keeps the preferred route advisory.

## Task signals

Score each task qualitatively; do not invent numeric precision.

1. Ambiguity: are the desired behavior and acceptance criteria clear?
2. Scope: is the change mechanical, localized, multi-file, cross-module, or architectural?
3. Coupling: how many state, data, service, platform, or lifecycle boundaries interact?
4. Verification: can correctness be checked deterministically, or does it require broad judgment?
5. Consequence: would failure be cosmetic, reversible, user-visible, production-impacting, or security/data-loss sensitive?
6. Latency priority: did the user explicitly request a quick return, and is that supported by evidence for the task?

Use the task signals to choose among the lanes above. High ambiguity or coupling uses Sol/medium; high consequence uses Sol/high. Verification=judgment alone does not escalate. Infrastructure and unclassified failures do not trigger Sol/xhigh.

## Common patterns

| Work pattern | Starting recommendation |
|---|---|
| Tiny literal replacement or metadata edit | GPT-6 Luna/medium |
| Documentation, localization, or a repeated config edit | GPT-6 Luna/high |
| Clear bounded implementation with deterministic checks | GPT-6 Luna/high |
| Large bounded source scan or review | GPT-6 Luna/xhigh |
| Deep deterministic implementation where latency is acceptable | GPT-6 Luna/max |
| Bounded multi-file or cross-layer change | GPT-6.1 Sol/low |
| Unclear bug across async state, persistence, networking, or lifecycle | GPT-6.1 Sol/medium |
| High-consequence security, privacy, payment, or destructive migration | GPT-6.1 Sol/high |
| Classified complex reasoning or verification failure | GPT-6.1 Sol/xhigh |

Prefer safe direct tool concurrency when it is sufficient. Use a model-specific leaf only when route-fit benefit clears startup and aggregation cost; preserve the bounded delegation and parallel-execution gates in the Skill. Never claim that the chart proves faster Codex work: it contains cost and Intelligence Index values, not latency or subscription pricing.
