# Eylema first-release roadmap

Revision **0.3.0**, 11 October 2026. English is canonical; [Türkçe](https://github.com/eylema-dev/eylema-docs-tr/blob/main/docs/roadmap.md). Target: **v0.1.0 experimental**, not a production-ready universal framework. Milestones are acceptance gates, not delivery-date promises. Only repository documents and tooling exist today. The M0 foundation and repository split are merged; G02 documentation/implementation stage gates passed separate review and current PR/main CI. This is repository-tooling evidence, not application execution.

## The selected first working application

The maintainer selected the task core and web interface: create, run, inspect, stop, save and reopen a task. M1 establishes deterministic execution and M2 completes the saved-task browser flow. The [component proposal and acceptance scenarios](project-structure.md) make that goal reviewable before implementation. No model or GPU is required for this first proof.

The later experimental release extends the same application with a small 3D placement environment, learned policy/world dynamics, one supported local language model, permitted learning and the development-team PR flow. Each capability has its own acceptance gate; selecting the first proof does not claim those later capabilities are available.

The first experimental release targets one Apple M4 Pro MacBook Pro with 24 GB unified memory, native macOS CPU/Metal and browser Wasm/WebGPU on that same device. macOS 27.0.1 is observed; G04 verifies the actual tools/SDK/browser. Linux support and second physical-device acceptance are deferred. Assignment compares at least two measured WorkloadProfiles bound to that single HardwareProfile; these never count as two devices. Record actual memory, latency/frame-time and quality baselines before approving numerical limits; do not invent them before hardware and workload selection.

| ID | Release gate | Scope | Acceptance evidence | Depends on |
|---|---|---|---|---|
| M0 | Contribution foundation | Agent contract, bilingual docs, issue/PR templates, read-only CI | Validators reject negative fixtures; PR and main CI are observed; maintainer review/ruleset status is explicit | None |
| M1 | `v0.1.0-alpha.1` | Owned Rust workspace, typed task/state/action contracts, deterministic executor | Rust 1.99.0; zero external production Cargo dependencies; native aarch64-apple-darwin build/test and selected portable-library Wasm build; native unit/recovery, bounds and denied-action tests; implementation CI activated with Rust source | M0 |
| M2 | `v0.1.0-alpha.2` | First task console: owned web UI, local server and durable state | Create/run/inspect/stop/save/restart/reopen; duplicate requests, authority denial, effective stop; loopback session, Host/Origin, CSRF and bounded input; durable acknowledgement and recovery errors | M1 |
| M3 | `v0.1.0-alpha.3` | Native Metal worker plus browser WebGPU and small 3D scene | Actual compute/readback on M4; named browser/driver WebGPU; worker/device-loss and unsupported errors; shared memory/job budgets; combined load/frame-time measurements; host, Metal shader and WGSL inventory | M2 |
| M4 | `v0.1.0-beta.1` | CPU/Metal tensor references, learned policy and small world model for bounded 8×8 placement | CPU/Metal parity at predefined tolerances; held-out closed-loop success and prediction error; constraints; honest comparison with deterministic baseline | M3 |
| M5 | `v0.1.0-beta.2` | Pinned Qwen3-0.6B candidate in owned runtime | G27 fixes exact artifacts/tokenizer/operators/rights; FP32 CPU reference and FP16 Metal execution; quantization optional; load/first-result/warm and held-out quality; combined scene/policy/LLM budgets; explicit unsupported error, no hosted fallback | M4 |
| M6 | `v0.1.0-rc.1` | Versioned model assignment and permitted local learning | At least two measured workloads on one M4 device; model-set 0.2.0 physical/workload bindings; accepted manifest, canary/rollback; consent/provenance/deduplication/holdout; bounded pinned local Unsloth Studio/MLX run; export reaccepted in owned Rust | M5 |
| M7 | `v0.1.0` | Need-to-PR protocol and experimental release | Real task through intake/plan/code/checks/separate review; actual Codex and Claude adapters on the same contract, explicit online GitHub/provider access and idempotent PR retry; license decision and G44 full Mac acceptance before reproducible release packaging | M6 |

## First executable backlog

These EYL IDs remain planning references. Accepted G00–G45/W01 cards refine them into bounded work; individual Goal issues link exact scope and acceptance. Create a scoped issue before each implementation. Historical initial Goal proposals are not live completion records.

| ID | Next work item | Done when |
|---|---|---|
| EYL-001 | Select license and contribution terms | Maintainer records the decision and provenance rules; no implied contributor agreement |
| EYL-002 | Fix first workload/hardware matrix | G03 contracts name one M4 Pro/24 GB Mac and separate native/browser workloads; G04 inventories tools; G18 measures reproducible tasks/scene; Linux and second physical device are future scope; unavailable execution stays `not_run` |
| EYL-003 | Bootstrap owned Rust workspace and CI | Rust 1.99.0, lockfile, native macOS build/tests and selected portable Wasm libraries; no external runtime crates; G02 stage rules and G07 actual implementation gates |
| EYL-004 | Implement task state machine | Success, failure, denied action, timeout, duplicate delivery and cancellation behavior covered, with no exactly-once claim for external effects |
| EYL-005 | Implement durable local task journal | Truncated record, crash/restart and incompatible-format paths tested; explicit version and recovery behavior |
| EYL-006 | Build first web task screen | Create/run/inspect/stop/save/reopen journey is demonstrated in a browser with bounded permissions and visible errors |
| EYL-007 | Prototype native Metal and WebGPU resource boundaries | Real M4 compute/readback and browser 3D scene, CPU reference, unsupported/device-loss errors and combined memory/job limits |
| EYL-008 | Fix first model contracts | Qwen3-0.6B is the accepted initial candidate, with FP32 CPU and FP16 Metal paths and optional quantization; G27 pins artifacts/rights/operator scope; policy/world model contracts and measured resource limits still need acceptance; candidate selection is not support |

## Goal ordering and evidence boundaries

G03 aligns these contracts; G04 verifies the actual Rust/macOS/SDK/browser environment. G07 enables runtime source with implementation CI. F1–F7 remain the M1/M2 flow; G17 proves its external example against accepted core. The accepted action plan permits G38–G43 development orchestration after that base and before GPU work; the M7 release gate still depends on M6. G18 measures workloads before numerical resource limits are accepted. G27 fixes the model contract before tensors/loader/model execution, and G35/G36 separately prove local training and owned-engine export. G44 must exercise the full twelve-step journey on this Mac before G45 packaging. W01 may prepare truthful website content; deployment needs separate authority and matching live evidence.

The added model-set schema is 0.2.0; runtime/NeedSpec remain 0.1.0. Synthetic schema fixtures, document CI, build success, GPU execution, trained model quality and release acceptance are distinct evidence. No runtime, GPU or training result is established by this roadmap.

## v0.1.0 release checklist

- Every milestone's required checks has current evidence on the exact release candidate; skipped required hardware checks block the affected support claim.
- Quality thresholds, p95/p99 latency/frame time, memory budgets and startup behavior are defined and met for the declared profiles. Report failures as well as gains.
- HITL/HOTL/HIC contracts, revocation, intervention and rollback limitations are exercised. A model's output cannot widen authority.
- English and Turkish guides reproduce the first application and report supported/unsupported targets. API/code/schema versions agree.
- Distribution license, model/data rights, toolchain/driver/browser inventory and known limitations are recorded. No kernel rewrite, production crypto implementation or hardware access beyond platform permissions is implied.
- A maintainer accepts the release. CI alone cannot promote models, merge changes or publish a release.

## Deliberately outside the first release

Linux support, second physical-device acceptance, a general CAD kernel, every model architecture, distributed training, a Rust-only Linux kernel, arbitrary GPU driver support, automated procurement, unattended privileged self-modification and complete production web feature parity are later decisions. The roadmap preserves the long-term architecture while proving one bounded vertical slice first.
