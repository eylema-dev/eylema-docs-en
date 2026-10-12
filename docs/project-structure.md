# Project structure and accepted first-product decisions

Revision **0.3.0**, 12 October 2026. [Turkish companion](https://github.com/eylema-dev/eylema-docs-tr/blob/main/docs/project-structure.md).

The maintainer accepted recommendations 1, 2, 4, 5, 6 and 8, supplied the three-device inventory below and selected Apache-2.0 on 12 October 2026. These decisions update the current product direction. They do not rewrite historical Goal records or claim that remaining runtime, model or hardware acceptance has passed.

## First user and product outcome

The first user is a developer building a local agent application. The first deliverable is a single-user task console: create a task, execute bounded deterministic steps, inspect progress/results, stop authorized remaining work, restart the service and reopen the same durable task. Initial steps change only application-owned task state. Remote administration, multiple tenants and arbitrary filesystem/process/network actions are outside this first product.

A usable task-console preview is evaluated at M2 without waiting for GPU, models or training. A small real need-to-PR proof follows the accepted core/example base and precedes the optional learning work. Full autonomous development/provider acceptance and the complete experimental release keep their separate M7/G44/G45 gates. The small 3D placement environment is a reference application for later capabilities, not a prerequisite for the first user's task console.

Core already contains Rust task/runtime/journal/host/web components and a CLI. See [current core status](https://github.com/eylema-dev/eylema/blob/main/README.md) and its revision-bound evidence. Real person authentication remains an explicit limitation: the stock non-human session cannot prove the effective human-authorized stop scenario by receiving FORBIDDEN. This decision does not waive F3 or authorize weakening that check.

## Language, ownership and component boundaries

English is canonical; Turkish is the synchronized companion. Code, identifiers, templates and task records remain English. The [repository map](https://github.com/eylema-dev/devguide/blob/main/docs/en/repository-map.md) owns repository boundaries. Product contracts stay in the language repositories, shared contribution policy in devguide, and implementation/schemas in core.

Use one owned Rust workspace and one local native host process. Add a module/crate only for a tested boundary and an actual consumer.

| Component | Responsibility |
|---|---|
| `crates/eylema-contracts` | Canonical Rust domain types, versioned transitions, bounded EYL wire records and approval payload construction |
| `crates/eylema-runtime` | Scoped admission, deterministic steps, authority, budgets, observations and effective cancellation |
| `crates/eylema-journal` | Bounded EYLJ append/replay, explicit durability and corruption errors |
| `crates/eylema-platform` | Narrow standard host crypto/entropy/synchronization and native GPU bindings |
| `crates/eylema-host` | Runtime/journal composition, durable recovery and local service boundary |
| `crates/eylema-web` | Local browser interface and bounded presentation/transport adapters |
| `apps/eylema` | Native CLI/service composition and configuration |
| `eylema-examples/task-console` | External consumer pinned to a core revision; no fork of runtime code |

Dependencies point toward contracts. The host owns execution, authority and persistence. The browser presents state and uses declared GPU capabilities; it cannot directly modify the journal or confer native authority. Browser closure leaves native work alive; reopening reads snapshots/events. Rust 1.99.0 and aarch64-apple-darwin remain the native baseline; selected portable libraries compile to wasm32-unknown-unknown. Compilation and actual target execution are separate evidence.

## Available test inventory

These aliases record the maintainer's available equipment, not accepted runtime HardwareProfile IDs. Materialize each measured HardwareProfile and its WorkloadProfiles with exact OS, CPU/GPU, SDK/driver/browser versions, workload hashes and code revision. One device with two workloads is still one physical device.

| Inventory alias | Owner-reported equipment | Initial role | Evidence boundary |
|---|---|---|---|
| `mbp-m4-pro-24` | MacBook Pro, Apple M4 Pro, 24 GB unified memory | Primary local task-console acceptance; later CPU/Metal and browser WebGPU measurements | Existing core evidence is scoped to this device; this decision change does not rerun hardware acceptance |
| `mini-m4-24` | Mac mini, Apple M4, 24 GB unified memory | Second physical Mac compatibility and resource comparison | OS/tools/browser and all Eylema execution on this device: not_run |
| `rtx4070ti-super-16-32` | NVIDIA RTX 4070 Ti Super, 16 GB VRAM, 32 GB system RAM | Later discrete-GPU comparison and training feasibility | Linux owner-confirmed; CPU/distribution/kernel unconfirmed; driver/backend/access and all Eylema execution: not_run |

The two additional machines do not block the primary task-console preview. Their acceptance is a separate bounded task; an inventory row does not enable a Linux/Windows backend or authorize remote access, installation or training. Apple unified memory and RTX dedicated VRAM/system RAM are recorded separately, never combined into an invented interchangeable budget.

First measure the same versioned deterministic task with fixed inputs, cold/warm startup, task latency p95/p99, peak memory and successful/incorrect action counts. For GPU work add reference-output tolerance, frame-time distribution and combined workload memory. Freeze numerical quality/resource thresholds after baseline measurement and before candidate comparison. Unavailable observations remain unknown/not_run.

## Fixed task, storage and API decisions

| Concern | Accepted first implementation contract |
|---|---|
| Semantic source | Owned Rust types and constructors in eylema-contracts; HTTP/CLI/browser adapters use the same semantics. OpenAPI/JSON Schema/MCP generation is future work, with parity fixtures required before claiming generated support |
| State and authority | Task and execution identities remain separate; stale revisions and unauthorized effects fail; success, failure, effective cancellation and unknown outcome remain distinct |
| Canonical approval | Existing EYL codec v1 and canonical_approval_payload bind typed task/proposal/action fields; standard host SHA-256 hashes those bytes. Maps/sets have deterministic ordering; transport request/correlation IDs are excluded; no implicit text normalization or float encoding |
| Persistence | Existing EYLJ v1 journal in a host-owned local directory, intent/commit records and durable acknowledgement; corrupt/torn/incompatible input fails without silent repair or migration |
| Replay retention | Retained admission keys/results survive validated journal replay; no automatic eviction, rotation or time-based expiry is added. Finite capacity exhaustion fails explicitly rather than admitting a duplicate |
| Restart | Confirmed identities/results/effects survive. Unfinished execution becomes OutcomeUnknown; old sessions retire and require fresh trusted enrollment. Uncertain external effects are never silently repeated |
| Compatibility | Existing runtime 0.1.0, EYL v1 and EYLJ v1 remain unchanged. Future incompatible changes require a new version and explicit migration/rejection tests |

Implementation details and executed scopes: [typed contracts](https://github.com/eylema-dev/eylema/blob/main/docs/en/typed-contracts.md), [canonical codec/platform](https://github.com/eylema-dev/eylema/blob/main/docs/en/codec-platform.md), [journal](https://github.com/eylema-dev/eylema/blob/main/docs/en/local-journal.md), [recovery](https://github.com/eylema-dev/eylema/blob/main/docs/en/runtime-recovery.md). The wider [API catalogue](api-reference.md) still contains proposed operations; this decision does not declare every route implemented.

## Local authority and explicit platform dependencies

The initial service is single-user and loopback-only. Enforce scoped sessions, Host/Origin and CSRF checks, bounded requests and host-verified principal/approval records. A model or claimed human field cannot create authority. Already authorized routine actions do not need repeated approval; designated checkpoints, governance and stop permissions remain enforced. Public/LAN exposure, remote identity and TLS termination require a separate accepted design; the local prototype makes no remote/TLS support claim.

The zero third-party production Cargo policy is unchanged. macOS CommonCrypto/Security/libSystem provide standard hash, entropy and synchronization services through narrow reviewed bindings; owned code does not implement cryptography. Metal/SDK bindings and Metal shader sources, minimal browser host JavaScript, WebAssembly/WebCrypto, WebGPU and WGSL are explicit platform inputs. Native Metal and browser WebGPU have separate device contexts; no shared GPU buffer or universal zero-copy guarantee is implied. Python/Unsloth and packaging converters stay in separately pinned development/training inventories.

## Acceptance for the first browser demonstration

| ID | Scenario | Required evidence | Roadmap |
|---|---|---|---|
| F1 | Create a valid task and inspect it | Stable task ID, scope, budget and revision; invalid input rejected | M1–M2 / EYL-004, EYL-006 |
| F2 | Run an authorized deterministic task | Recorded execution, ordered progress and result; denied action has no unauthorized effect | M1–M2 / EYL-004 |
| F3 | Stop an execution while work remains | Receipt and effective stop are distinct; remaining steps stop; completed effects stay visible; late stop preserves a completed result | M1–M2 / EYL-004, EYL-006 |
| F4 | Restart and reopen saved state | Same task/execution IDs, revisions, outcomes and events; in-flight recovery policy exercised | M2 / EYL-005, EYL-006 |
| F5 | Repeat a request or submit a stale revision | Identical replay returns the original reference; changed payload and stale revision fail explicitly | M1–M2 / EYL-004, EYL-005 |
| F6 | Interrupt a write or encounter an incompatible record | Declared recovery or explicit failure; no fabricated completion and no silent data loss | M2 / EYL-005 |
| F7 | Exceed limits or encounter an unavailable capability | Bounded input/queue/work, explicit errors and truthful outcome after deadline expiry | M1–M2 / EYL-003, EYL-004, EYL-006 |

F1–F7 must be demonstrated at the same candidate revision on the primary device, with actual person verification distinguished from trusted-host test fixtures. A cancellation receipt is not an effective stop, and a deadline is not physical termination evidence. The first product has no external task effects; negative cases still preserve truthful partial/unknown outcomes. No check is waived by this scope decision.

## License and first learning experiment

First-party source and documentation use Apache-2.0, selected by the maintainer. See [license and contribution scope](https://github.com/eylema-dev/devguide/blob/main/docs/en/licensing.md). Third-party model/data terms remain independent.

Keep the existing Qwen3-0.6B choice as a candidate, not an execution/support claim. Fix exact operators/artifacts and measure the deterministic baseline on the selected hardware before accepting models. Limit the first learning experiment to one permitted task, a human correction, a pinned recipe and an independent held-out comparison within a finite budget. The [learning protocol](learning-and-training.md) requires permission, retention and resource decisions before collection/training. Neither new data collection nor a training run is authorized by publishing these decisions.
