# Turing Pi Repo Family — README Convention

A shared convention so the four **Turing Pi** repositories read as one family:
consistent look, feel, and language, with the inter-relationship between them made
obvious on every repo's front page.

**Repos in scope**

| Repo | Layer | What it is |
|------|-------|------------|
| [terraform-provider-turingpi](https://github.com/freed-dev-llc/terraform-provider-turingpi) | Provider | Terraform/OpenTofu provider for the Turing Pi 2/2.5 BMC API |
| [terraform-turingpi-modules](https://github.com/freed-dev-llc/terraform-turingpi-modules) | Modules | Reusable Terraform modules built on the provider |
| [turing-ansible-cluster](https://github.com/freed-dev-llc/turing-ansible-cluster) | Cluster (K3s) | K3s-on-Armbian cluster, Terraform + Ansible |
| [turing-rk1-cluster](https://github.com/freed-dev-llc/turing-rk1-cluster) | Cluster (Talos) | Talos Linux bare-metal Kubernetes cluster |

> `turing-rk1-cluster` is the **reference implementation** of this convention.

---

## The canonical stack relationship

Every repo describes the relationship the same way, so a reader landing on any one
of them understands where it sits. Use this wording (adapt the emphasis to the repo):

> **Part of the Turing Pi cluster stack:** the **provider** talks to the Turing Pi
> BMC, the **modules** wrap it into reusable Terraform, and the **cluster** repos
> deploy Kubernetes on top — **Talos** ([turing-rk1-cluster]) or **K3s**
> ([turing-ansible-cluster]).

```
provider (BMC API)  →  modules (reusable Terraform)  →  cluster: Talos | K3s
```

---

## Required header block

Same order in every repo, top to bottom:

1. **`# Title`** — the repo's human title.
2. **Horizontal logo** — the repo's own logo from the shared palette (see
   [Branding assets](#branding-assets)). Do not force one shared logo; each repo keeps
   its own.
3. **Status badges** — **Release** and **License: Apache 2.0** are required; add
   tech/registry badges (Talos, K3s, Kubernetes, Go, Terraform Registry, …) as relevant.
4. **One-sentence description** of what the repo is.
5. **Stack callout + sibling buttons** — the relationship blurb above, followed by the
   button row linking to the **other three** repos. This lives at the **top** (not a
   bottom "Related" section) so the family is visible immediately.

### Header skeleton (copy/paste)

```markdown
# <Repo Title>

![<Repo Title>](docs/assets/<logo-path-horizontal>.svg)

[![Release](https://img.shields.io/github/v/release/freed-dev-llc/<repo>)](https://github.com/freed-dev-llc/<repo>/releases)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
<!-- + tech/registry badges as relevant -->

<One sentence: what this repo is.>

> **Part of the Turing Pi cluster stack** — provider → modules → cluster (Talos / K3s).

[![Terraform Provider — freed-dev-llc/terraform-provider-turingpi](docs/assets/buttons/btn_terraform_provider_turingpi.svg)](https://github.com/freed-dev-llc/terraform-provider-turingpi)
[![Terraform Modules — freed-dev-llc/terraform-turingpi-modules](docs/assets/buttons/btn_terraform_turingpi_modules.svg)](https://github.com/freed-dev-llc/terraform-turingpi-modules)
[![Turing RK1 Ansible — freed-dev-llc/turing-ansible-cluster](docs/assets/buttons/btn_turing_ansible_cluster.svg)](https://github.com/freed-dev-llc/turing-ansible-cluster)
[![Turing RK1 Cluster — freed-dev-llc/turing-rk1-cluster](docs/assets/buttons/btn_turing_rk1_cluster.svg)](https://github.com/freed-dev-llc/turing-rk1-cluster)
```

Show the buttons for the **other three** repos (drop the row for the current repo).

---

## Standard section vocabulary

Same concept → same H2 in every repo. Pick the canonical name on the left.

| Canonical H2 | Use for | Don't use |
|--------------|---------|-----------|
| `## Contents` | Table of contents (see [TOC rule](#toc-rule)) | "Table of Contents", "Index" |
| `## Quick Start` | Minimal get-it-running steps | "Usage" / "Installation" as the entry point |
| `## Documentation` | Links to `docs/` guides (sub-tables OK) | "Documentation Map", "Docs" |
| `## Repository Structure` | Annotated repo tree | "Directory Structure", "Project Layout" |
| `## Prerequisites` | What you need before starting | "Requirements" |
| `## Related Projects` | Sibling repos — **only if** you need more than the top buttons | "Related Repositories", "Related Turing Pi projects" |
| `## License` | License | — |

Repo-specific sections (Features, Resources, Data Sources, Addons, NPU Support, …) keep
their natural names — the convention only standardizes the **shared** ones above.

### Recommended order

```
Header (title · logo · badges · description · stack callout + buttons)
## Contents            (if long — see TOC rule)
## <Overview/Features> (repo-specific, optional)
## Quick Start
## Documentation
## Repository Structure
## <domain sections>   (repo-specific)
## Prerequisites
## License
```

The **related-projects buttons live in the header**, so a bottom "Related Projects"
section is redundant — omit it unless a repo needs extra context per sibling.

---

## TOC rule

Add a `## Contents` section (right after the header) when the README has **≥ 8 H2
sections** or **≥ ~200 lines**. Keep it to the H2s; link with GitHub anchor slugs
(lowercase, spaces → `-`, punctuation dropped; `&` becomes a doubled `-`, e.g.
`## Access & Networking` → `#access--networking`).

---

## Branding assets

All shared graphics must be **compatible across every repo** — same source, same size,
referenced the same way — so a button or logo looks identical wherever it appears.

### Sibling buttons

- Live under `docs/assets/buttons/` as `btn_<repo>.svg` and are referenced **relatively**.
  Never use raw `<img>`/`<a>` HTML and never hotlink another repo's asset from
  `raw.githubusercontent.com`.
- **Uniform dimensions:** every button is **`viewBox="0 0 372 72"`, 372×72**. Don't
  resize per repo.
- **Byte-identical:** each repo vendors its own copy, but every copy of a given button
  must be **identical** to the canonical one (verify with `md5sum`). The canonical,
  complete set of all four buttons lives in
  [`turing-rk1-cluster/docs/assets/buttons/`](https://github.com/freed-dev-llc/turing-rk1-cluster/tree/main/docs/assets/buttons) —
  copy any you are missing from there rather than regenerating.
- Each repo vendors the **three sibling** buttons (not its own).

### Logos

- Live under `docs/assets/<family>/logos/` and are referenced **relatively**. Each repo
  keeps its **own** horizontal logo (cluster repos use the `turing-cluster` family with a
  per-repo variant suffix; the Terraform tooling uses its `turingpi` product logo) — this
  is intentional, not drift.
- **Consistent aspect ratio:** horizontal logos are `800` wide. Keep the height
  consistent within a family so they render at the same scale; prefer `800×260` for the
  cluster-variant logos. (Base logos are currently `800×240`; align when convenient.)

### Compatibility checklist

- [ ] Every `btn_*.svg` referenced by the README exists locally under `docs/assets/buttons/`.
- [ ] Each button's `md5sum` matches the canonical copy in `turing-rk1-cluster`.
- [ ] All buttons are `372×72`; no raw-HTML or hotlinked image tags in the header.
- [ ] The repo's own logo is present locally and referenced relatively.

---

## Voice & tone

- Concise and scannable. Prefer **tables** over long prose for specs, versions, and maps.
- Present tense, factual, no marketing fluff ("blazing-fast", "powerful").
- State pinned versions explicitly; for "tracks latest" components say so once rather
  than repeating "Latest" per row.
- Don't duplicate facts (IPs, sizes, versions) across sections — state once, reference.
