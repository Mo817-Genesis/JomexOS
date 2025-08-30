# 🧭 Project Structure – JomexOS

This document describes the proposed directory layout for **JomexOS**.  
It’s meant to guide contributors and keep the repository consistent as it grows.

> Note: Some folders may start empty and evolve over time.
> JomexOS/
├─ .github/                     # GitHub workflows, issue/PR templates
│  ├─ ISSUE_TEMPLATE/
│  └─ PULL_REQUEST_TEMPLATE.md
├─ docs/                        # Whitepaper, specs, design notes
│  ├─ whitepaper/               # Theory, vision, governance
│  ├─ architecture/             # Diagrams, component specs
│  ├─ security/                 # PQC + ZKP design docs, audits
│  └─ dev-guides/               # Setup, build, contribution guides
├─ src/                         # Source code (workspaces / modules)
│  ├─ kernel/                   # Microkernel / scheduler / IPC
│  │  ├─ ipc/                   # Message passing, channels
│  │  ├─ sched/                 # Active Inference–inspired scheduling
│  │  └─ mm/                    # Memory mgmt (allocators, paging)
│  ├─ drivers/                  # Device drivers (net, fs, display…)
│  ├─ crypto/                   # Post-quantum primitives + ZKP
│  │  ├─ pqc/                   # KEMs, signatures (e.g., Kyber/Dilithium)
│  │  └─ zkp/                   # Circuits, verifiers, proofs
│  ├─ services/                 # Userland services (init, logging, update)
│  ├─ syslib/                   # System libraries (ABI, syscalls)
│  └─ ui/                       # Shell / UX prototypes (TUI/GUI)
├─ tools/                       # Build tools, codegen, dev scripts
├─ tests/                       # Unit, integration, property-based tests
│  ├─ kernel/
│  ├─ crypto/
│  └─ e2e/
├─ samples/                     # Minimal apps / demos for contributors
├─ benchmarks/                  # Performance + reproducible profiles
├─ assets/                      # Diagrams, icons, media used in docs
├─ .editorconfig                # Cross-editor formatting rules
├─ .gitignore                   # Ignore patterns for repo
├─ BUILDING.md                  # Build-from-source instructions
├─ CODE_OF_CONDUCT.md
├─ CONTRIBUTING.md
├─ LICENSE
├─ PROJECT_STRUCTURE.md         # (this file)
├─ README.md
└─ ROADMAP.md
> ---

## 🧱 Module Boundaries

- **Kernel**: minimal, message-passing first, capability-based where possible.  
- **Crypto**: PQC + ZKP always isolated behind stable interfaces; no direct calls from drivers.  
- **Services**: everything not kernel-level (init, logging, updates, metrics).  
- **UI**: optional at early phases; focus on TUI prototypes before GUI.

---

## 🔐 Security-by-Design

- PQC keys and ZKP proofs live under `src/crypto/`, never embedded in app code.  
- All new components must include a **Threat Model** doc in `docs/security/`.  
- Add tests under `tests/crypto/` and, when relevant, reproducible benches in `benchmarks/`.

---

## 🧪 Testing & CI (suggested)

- Unit tests mirror the code layout under `tests/`.  
- Integration tests go under `tests/e2e/`.  
- Add GitHub Actions later in `.github/workflows/`:  
  - `ci.yml` (build + test)  
  - `lint.yml` (format, lint, security checks)  

---

## 🛠 Developer Setup

- See `BUILDING.md` for toolchains, targets, and platform notes.  
- Use `.editorconfig` for formatting consistency.  
- Propose language-specific configs (e.g., Rust `rustfmt.toml`, C/C++ `clang-format`) via PR.  

---

## ✅ Contribution Tips

- One module per PR when possible.  
- Include diagrams for new subsystems under `docs/architecture/`.  
- For security-sensitive code, open an issue first to discuss design.  

---

*This structure is a living document—refine it as JomexOS evolves.*
