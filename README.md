# DevOpsTheWay (DOTW, pronounced “dot-wuh”)

**dotw-integration** is the **integration repository** (Git superproject) for the DOTW ecosystem.

It integrates all `dotw-*` repositories via **git submodules**, pinning each repo to a known-good **release tag** (e.g. `v0.1.0`) so the ecosystem can be cloned and reproduced consistently.

---

## What you get here

- One repo to clone that pulls the entire DOTW ecosystem
- Explicit version pinning per module (submodule commit pointers)
- A clean workflow that allows each module repo to evolve independently

---

## Clone the full ecosystem

Clone with submodules:

```bash
git clone --recurse-submodules https://github.com/tosshs/dotw-integration.git
