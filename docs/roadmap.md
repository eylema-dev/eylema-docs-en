# Eylema first-release roadmap

Revision **0.6.0**, 13 October 2026. English is canonical; [Türkçe](https://github.com/eylema-dev/eylema-docs-tr/blob/main/docs/roadmap.md). Target: **v0.1.0 experimental** with an earlier usable task-console preview at M2. Milestones are acceptance gates, not delivery-date promises. Core now contains task/runtime/journal/service/CLI/browser work and bounded GPU components; [core evidence](https://github.com/eylema-dev/eylema/blob/main/README.md) scopes each implementation. Full human-authenticated, model, learning and autonomous-development acceptance remains separate.

## The selected first working application

The maintainer selected the task core and web interface: create, run, inspect, stop, save and reopen a task. M1 establishes deterministic execution and M2 completes the saved-task browser flow. The [component proposal and acceptance scenarios](project-structure.md) make that goal reviewable before implementation. No model or GPU is required for this first proof.

The later experimental release extends the same application with a small 3D placement environment, learned policy/world dynamics, one supported local language model, permitted learning and the development-team PR flow. Each capability has its own acceptance gate; selecting the first proof does not claim those later capabilities are available.

The primary acceptance device remains the MacBook Pro M4 Pro with 24 GB unified memory. The maintainer also supplied a Mac mini M4 with 24 GB unified memory and a Linux system with RTX 4070 Ti Super 16 GB VRAM plus 32 GB RAM. The [three-device inventory](project-structure.md#available-test-inventory) records primary and later comparison roles, owner-reported facts and unrun checks. Neither an extra device nor two workloads on one device establish new support. Baseline measurements precede frozen numerical quality/resource limits; Linux and second-device execution need their own acceptance.

| ID | Release gate | Scope | Acceptance evidence | Depends on |
|---|---|---|---|---|
| M0 | Contribution foundation | Agent contract, bilingual docs, issue/PR templates, read-only CI | Validators reject negative fixtures; PR and main CI are observed; maintainer review/ruleset status is explicit | None |
| M1 | `v0.1.0-alpha.1` | Owned Rust workspace, typed task/state/action contracts, deterministic executor | Rust 1.99.0; zero external production Cargo dependencies; native aarch64-apple-darwin build/test and selected portable-library Wasm build; native unit/recovery, bounds and denied-action tests; implementation CI activated with Rust source | M0 |
| M2 | `v0.1.0-alpha.2` | First task console: owned web UI, local server and durable state | Create/run/inspect/stop/save/restart/reopen; duplicate requests, authority denial, effective stop; loopback session, Host/Origin, CSRF and bounded input; durable acknowledgement and recovery errors | M1 |
| M3 | `v0.1.0-alpha.3` | Native Metal worker plus browser WebGPU and small 3D scene | Actual compute/readback on M4; named browser/driver WebGPU; worker/device-loss and unsupported errors; shared memory/job budgets; combined load/frame-time measurements; host, Metal shader and WGSL inventory | M2 |
| M4 | `v0.1.0-beta.1` | CPU/Metal tensor references, learned policy and small world model for bounded 8×8 placement | CPU/Metal parity at predefined tolerances; held-out closed-loop success and prediction error; constraints; honest comparison with deterministic baseline | M3 |
| M5 | `v0.1.0-beta.2` | Pinned Qwen3-0.6B candidate in owned runtime | G27 fixes exact artifacts/tokenizer/operators/rights; FP32 CPU reference and FP16 Metal execution; quantization optional; load/first-result/warm and held-out quality; combined scene/policy/LLM budgets; explicit unsupported error, no hosted fallback | M4 |
| M6 | `v0.1.0-rc.1` | Versioned model assignment and permitted local learning | At least two measured workloads on one M4 device; model-set 0.2.0 physical/workload bindings; accepted manifest, canary/rollback; consent/provenance/deduplication/holdout; bounded pinned local Unsloth Studio/MLX run; export reaccepted in owned Rust | M5 |
| M7 | `v0.1.0` | Need-to-PR protocol and experimental release | Real task through intake/plan/code/checks/separate review; actual Codex and Claude adapters on the same contract, explicit online GitHub/provider access and idempotent PR retry; Apache-2.0 notices/artifact-rights review and G44 full Mac acceptance before reproducible release packaging | M6 |

## First executable backlog

These EYL IDs remain planning references. Accepted G00–G45/W01 cards refine them into bounded work; individual Goal issues link exact scope and acceptance. Create a scoped issue before each implementation. Historical initial Goal proposals are not live completion records.

| ID | Next work item | Done when |
|---|---|---|
| EYL-001 | Apply Apache-2.0 and contribution terms | Maintainer selected Apache-2.0 on 12 October 2026 for first-party code/docs; LICENSE/NOTICE, metadata and provenance scope accompany linked PRs; third-party artifact rights and release review remain separate |
| EYL-002 | Measure the available hardware matrix | Primary M4 Pro/24 GB; second Mac mini M4/24 GB; Linux RTX 4070 Ti Super/16 GB VRAM + 32 GB RAM comparison inventory; exact environment/workload binding and actual evidence per device; unrun checks remain not_run |
| EYL-003 | Bootstrap owned Rust workspace and CI | Rust 1.99.0, lockfile, native macOS build/tests and selected portable Wasm libraries; no external runtime crates; G02 stage rules and G07 actual implementation gates |
| EYL-004 | Implement task state machine | Success, failure, denied action, timeout, duplicate delivery and cancellation behavior covered, with no exactly-once claim for external effects |
| EYL-005 | Implement durable local task journal | Truncated record, crash/restart and incompatible-format paths tested; explicit version and recovery behavior |
| EYL-006 | Build first web task screen | Create/run/inspect/stop/save/reopen journey is demonstrated in a browser with bounded permissions and visible errors |
| EYL-007 | Prototype native Metal and WebGPU resource boundaries | Real M4 compute/readback and browser 3D scene, CPU reference, unsupported/device-loss errors and combined memory/job limits |
| EYL-008 | Fix first model contracts | Qwen3-0.6B is the accepted initial candidate, with FP32 CPU and FP16 Metal paths and optional quantization; G27 pins artifacts/rights/operator scope; policy/world model contracts and measured resource limits still need acceptance; candidate selection is not support |

## Goal ordering and evidence boundaries

**Accepted priority:** deliver the developer task-console preview and one bounded real need-to-PR proof after the accepted M2/G17 base, before optional model/training work. The proof must record the task, scoped change, checks, separate review and actual PR response; manually prepared repository PRs do not establish an autonomous coordinator. G38–G43 can then complete the two-provider protocol independently of M3–M6. The full experimental M7/G44/G45 release continues to require its remaining capabilities and acceptance; early delivery does not waive them.

G03 aligns these contracts; G04 verifies the actual Rust/macOS/SDK/browser environment. G07 enables runtime source with implementation CI. F1–F7 remain the M1/M2 flow; G17 proves its external example against accepted core. The accepted action plan permits G38–G43 development orchestration after that base and before GPU work; the M7 release gate still depends on M6. G18 measures workloads before numerical resource limits are accepted. G27 fixes the model contract before tensors/loader/model execution, and G35/G36 separately prove local training and owned-engine export. G44 must exercise the full twelve-step journey on this Mac before G45 packaging. W01 may prepare truthful website content; deployment needs separate authority and matching live evidence.

The added model-set schema is 0.2.0; runtime/NeedSpec remain 0.1.0. Synthetic schema fixtures, document CI, build success, GPU execution, trained model quality and release acceptance are distinct evidence. No runtime, GPU or training result is established by this roadmap.

## Accepted Rust harness Goal revision — 13 October 2026

The maintainer accepted a Rust harness that combines nine model roles, optional explicit external frontier-model assignments and local open-weight inference in owned Rust. The [current action plan](https://github.com/eylema-dev/devguide/blob/main/docs/en/platform-action-plan.md) and [current cards](https://github.com/eylema-dev/devguide/blob/main/records/platform-goal-plan.json) supersede only future execution proposals. Twenty-four accepted original Goal records remain unchanged; twenty-three remaining originals are revised and G46–G86 add forty-one bounded platform slices. They are planned, not completed. G40 remains blocked with its existing privacy/host/call/repair limits and no new allowance.

| Sequence | Deliverable | Required proof |
|---|---|---|
| Foundation | G46, G63, G54, G50: loop/role/model contracts, project boundaries, typed tools and decision evidence | Two contract consumers, incompatible profiles/authority/egress rejected, real owned tools, exact effect/evidence history |
| Model profiles | G27, G56, G49, G59, G67: language, decision, vision, separate STT/TTS and embeddings | Exact artifacts/operators/rights/preprocessing/output semantics; domain and EN/TR evaluation definitions |
| Owned inference | Existing G23–G31 plus G52–G53, G57–G58, G60–G62, G68–G69 | CPU reference then actual M4 Metal; task quality, precision, latency/throughput/memory and effective stop under combined load |
| Composition | G47–G48, G66, G55, G32, G70–G71 | Reviewed XState-only orchestration profile; bounded subflows, explicit external role contract, local-only job and grounded project RAG |
| Learning/ecosystem | G33–G37, G64–G65 | Permitted episodes/derivatives, split/withdrawal, candidate training and owned-Rust reacceptance, inspected share packages and compatible imports |
| Early text proof | G73, G74, G75, G72 | Actual human enrollment/stop, typed skills/router and private local EN/TR source-bound report; no vision/audio/world prerequisite |
| Native improvement | G76–G79, G83–G86 | Per-model profiles, owned Rust gradients/CPU and Metal LoRA/QLoRA, frozen holdout and controlled skill promotion |
| Capacity | G80–G82 | Checked estimates, actual calibration, uncertainty and dated investment scenarios; no automatic spend |
| Reuse/release | G51, remaining G06/G40–G45/W01 | Two applications, compatible model swap and full-loop benefit; all original release/provider/distribution gates retained |

Numerical quality/resource limits are frozen after the baseline and before candidate comparison, not invented from popularity or upstream speed claims. The role table in [architecture](architecture.md#rust-harness-model-roles-and-domain-selection) distinguishes deployment from model role and separates STT, TTS, visual perception and text domains. No open-weight model is assumed universally supported. XState is an explicit proposed workflow dependency, never an inference engine or Rust authority replacement; inventory/profile acceptance precedes integration. One Goal implements at a time, with private usage refresh, exact checks, genuine separate review, current CI and maintainer-authorized merge before dependent work.

## v0.1.0 release checklist

- Every milestone's required checks has current evidence on the exact release candidate; skipped required hardware checks block the affected support claim.
- Quality thresholds, p95/p99 latency/frame time, memory budgets and startup behavior are defined and met for the declared profiles. Report failures as well as gains.
- HITL/HOTL/HIC contracts, revocation, intervention and rollback limitations are exercised. A model's output cannot widen authority.
- English and Turkish guides reproduce the first application and report supported/unsupported targets. API/code/schema versions agree.
- Distribution license, model/data rights, toolchain/driver/browser inventory and known limitations are recorded. No kernel rewrite, production crypto implementation or hardware access beyond platform permissions is implied.
- A maintainer accepts the release. CI alone cannot promote models, merge changes or publish a release.

## Deliberately outside the first release

Accepted Linux runtime/GPU support, second physical-device acceptance, a general CAD kernel, every model architecture, distributed training, a Rust-only Linux kernel, arbitrary GPU driver support, automated procurement, unattended privileged self-modification and complete production web feature parity are later decisions. The roadmap preserves the long-term architecture while proving one bounded vertical slice first.
