# Eyleme English documentation

**Name update — 14 October 2026:** The product is **Eyleme** (formerly Eylema); the companion product is **Derleme** (formerly Derlema), and **Onama** keeps its name. The GitHub organization is now `eyleme-dev` (formerly `eylema-dev`). The main repository is now `eyleme-dev/eyleme`. On 15 October 2026 the six `eylema-*` child repositories became `eyleme-*`. Domains, commands, crate/package names, environment variables, data paths and protocol/schema identifiers retain their current spelling for compatibility. Historical evidence preserves its original names and URLs.

Canonical English architecture, API and product documentation. [Türkçe](https://github.com/eyleme-dev/eyleme-docs-tr).

**Stage: design and repository tooling.** No Rust application, GPU result, trained model or production deployment is supplied by these documents. The first product direction is a deterministic task console; later milestones add compute, models and learning.

## Read the contracts

- [Architecture](docs/architecture.md)
- [API and human oversight](docs/api-reference.md)
- [Development and operations](docs/development-and-operations.md)
- [Learning and training](docs/learning-and-training.md)
- [Project structure and first application](docs/project-structure.md)
- [Roadmap](docs/roadmap.md)

## Repository boundaries

Runtime source and machine-readable schemas belong to [Eyleme](https://github.com/eyleme-dev/eyleme). Contributor policy and quality gates belong to [devguide](https://github.com/eyleme-dev/devguide); [the repository map](https://github.com/eyleme-dev/devguide/blob/main/docs/en/repository-map.md) names every owner. First-party source and documentation are licensed under [Apache-2.0](LICENSE). Separately identified third-party material, model weights and datasets retain their own terms.

Read [CONTRIBUTING](CONTRIBUTING.md) before editing. Update the Turkish companion and the pinned repository set in devguide together. Local fingerprints record reviewed bytes; the repository-set gate compares both languages, API identifiers, roadmap IDs and cross-repository links. It does not prove semantic translation quality.

Migration provenance and merge order are recorded in [devguide](https://github.com/eyleme-dev/devguide/blob/main/docs/en/repository-migration.md). New default-branch document links become available when the coordinated migration PRs are merged by the maintainer.
