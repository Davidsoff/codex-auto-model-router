# Community launch kit

Use these drafts as starting points. Keep the final posts personal and answer early feedback yourself.

## GitHub settings

**Description**

> Capability-based GPT-6 model, reasoning, and concurrency routing for OpenAI Codex—no external API required.

**Topics**

`openai-codex`, `codex`, `codex-skill`, `gpt-6`, `model-routing`, `reasoning`, `ai-coding-agent`, `developer-tools`

## v0.2 release

**Suggested tag:** `v0.2.0`

**Title:** `v0.2.0 — Fail-open benefit-gated routing`

**Notes**

> Version 2 is a reliability-focused redesign of Codex Auto Model Router. The original version taught me an uncomfortable lesson: a router that blocks the real work is worse than no router at all.
>
> - Offers economy, balanced, and quality profiles across GPT-6 Luna, GPT-6.1 Sol, and GPT-6 Astra. Balanced preserves the existing lanes; quality uses Astra for high-consequence work and classified complex failures. Ultra disables Router-managed parallelism.
> - Re-evaluates every applicable request instead of inheriting the previous route.
> - Keeps sufficient work in the current coordinator; recommendations never claim to switch an already-running conversation's model or reasoning effort.
> - Removes hashes, cursors, environment guards, blocking ledgers, and rebuilt envelopes from the default execution path.
> - Runs independent safe tools or processes concurrently in the coordinator without creating child-agent UI entries.
> - Automatically delegates, reuses, or applies multi-model agent parallelism when route benefit clearly exceeds bounded startup and aggregation overhead; no extra permission prompt is required.
> - Supports `--no-subagents` as an explicit opt-out and retains bounded executor lifecycle, finalization, and reuse safeguards.
> - Provides economy, balanced, and quality profiles for Luna, Sol, and Astra, with customizable per-lane model and reasoning-effort overrides.
> - Allows a Luna route to fall back to Sol at the same effort; Sol never downgrades to Luna. Retired model IDs and GPT-5.5 are rejected for routing, while historical records remain readable.
> - Retains the `latency_priority` compatibility lane as Luna/max for cost/value; the dated Artificial Analysis comparison shows lower cost but slower completion than Terra/xhigh.
> - Uses deterministic capability policy informed by a bounded current comparison, preserves historical benchmark snapshots, and keeps task evidence and supported user overrides primary.
> - Fails open to local execution when routing fails; subagent startup failures also fall back locally when safe.
> - Records routing and concurrency outcomes after completion on a best-effort basis, without prompts, source code, telemetry, or external APIs.
> - Validated with local tests, distribution checks, Skill validation, and native Codex evidence.
>
> This is my first open-source project. If it sends a task down the wrong path or makes a clumsy split, that concrete example is the feedback I would value most.

## Reddit or OpenAI Developer Community

**Title**

> I built a model-capability router for GPT-6 in Codex

**Post**

> I kept bouncing between GPT-6.1 Sol and GPT-6 Luna in Codex: this task looked small, but was it really? Did it need more reasoning, or was I just overthinking it? After doing that loop one too many times, I decided to turn my own way of choosing into an open-source Skill.
>
> It uses GPT-6 Luna/medium for mechanical work, Luna/high for ordinary work, Luna/xhigh for large bounded scans, and Luna/max for deep deterministic work or the `latency_priority` cost/value choice. Bounded complexity uses GPT-6.1 Sol/low, ambiguity or coupling uses medium, high consequence uses high, and a classified complex reasoning failure uses xhigh. Sol/max is explicit-only. A Luna route may fall back to Sol at the same effort; Sol does not downgrade to Luna. Retired model IDs and GPT-5.5 cannot be routed. Because a Skill cannot switch an already-running main conversation, a different route runs in a separate model-specific leaf only when its benefit clearly exceeds bounded overhead. Independent safe tools still run concurrently without child agents, and no extra permission prompt is required for a justified leaf.
>
> Native Ultra is deliberately off by default. If you explicitly enable it for one bounded task, the Router steps back from its own parallel scheduler instead of stacking two orchestration systems.
>
> The user-provided 2026-09-30 Artificial Analysis graph and [direct comparison](https://artificialanalysis.ai/models/comparisons/gpt-6-luna-vs-gpt-5-6-terra-xhigh) put GPT-6 Luna/max at index 37, $0.07/task, and about 327.5 seconds, versus GPT-5.6 Terra/xhigh at index 38, $0.63/task, and about 220.6 seconds. Luna/max costs about one ninth as much but is about 107 seconds slower, with a one-point index tradeoff. That supports a cost/value choice, not a fastest-route claim or Codex subscription savings. Historical GPT-5.6 snapshots remain unchanged. Task-specific evidence and supported explicit user choices still take priority. The Skill runs entirely inside Codex and does not require an external API, API key, or telemetry service.
>
> This is my first open-source project. If you try it and the route feels like overkill, comes up short, splits the work awkwardly, or gets blocked, I would genuinely like to hear about it. Those real routing mistakes are more useful to me than a star.
>
> Repository: https://github.com/orange-the-weak/codex-auto-model-router

## LINUX DO

**标题**

> 做了一个支持 GPT-6 的 Codex 自动模型路由 Skill

**正文**

> 说实话，Codex 有了 GPT-6.1 Sol、GPT-6 Luna、多档推理强度和并行子任务之后，我常常会在几个选项之间来回切：这个活到底该上哪档？是任务真复杂，还是我有点上头了？这样纠结久了，我干脆把自己这套判断整理成了一个开源 Skill。
>
> 它会按当前任务推荐模型和推理强度：用 GPT-6 Luna/medium 处理机械任务，Luna/high 处理普通任务，Luna/xhigh 处理大型有界扫描，Luna/max 处理大型确定性深度任务或 `latency_priority` 兼容通道的成本与能力取舍；有界复杂任务交给 GPT-6.1 Sol/low，高歧义或高耦合用 medium，高后果用 high，已分类的复杂推理失败用 xhigh。Sol/max 只接受显式指定。Luna 可按相同 effort 回退到 Sol；Sol 不会降级到 Luna。旧模型标识和 GPT-5.5 不可用于路由，但历史记录仍可读取。Skill 不能切换已经开始的主对话，因此不同路由会在收益明确超过有界开销时交给独立的指定模型叶子智能体；独立安全的工具仍直接并发，合理委派无需额外询问许可。
>
> 原生 Ultra 默认关闭。只有用户为单个有界任务显式开启时才使用，同时停掉 Router 自己的并发，避免两套调度互相打架。
>
> 用户提供的 2026-09-30 Artificial Analysis 图表及其[直接对比](https://artificialanalysis.ai/models/comparisons/gpt-6-luna-vs-gpt-5-6-terra-xhigh)显示：GPT-6 Luna/max 指数为 37，每任务 $0.07，约 327.5 秒；GPT-5.6 Terra/xhigh 指数为 38，每任务 $0.63，约 220.6 秒。Luna/max 成本约为后者的九分之一，但慢约 107 秒，指数低 1 点。这支持成本与能力取舍，不代表最快路由，也不能直接换算成 Codex 订阅节省。历史 GPT-5.6 快照保持不变。具体任务证据和受支持的用户指定始终优先。整个过程在 Codex 内完成，不需要外部 API、API Key 或遥测服务。
>
> 这是我的第一个开源项目。要是你用下来发现它选强了、选弱了、拆多了，或者莫名卡住了，欢迎直接告诉我；别光点 Star，这些真实案例对我更有用。
>
> GitHub：https://github.com/orange-the-weak/codex-auto-model-router

## What to ask testers for

Ask for only:

1. The visible one-line routing notice.
2. The route they expected.
3. Task shape, outcome, and whether rework or blocking occurred.
4. Codex surface/version and Router release or commit.

Do not ask for prompts, source code, credentials, personal paths, or private project data.
