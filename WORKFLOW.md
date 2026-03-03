# DOTW Workflow

This document defines the minimal, repeatable workflow for the DOTW ecosystem:
independent module repos + one integration repo that pins stable versions.

---

## Repo Roles

### Module repositories (`dotw-*`)

Examples: `dotw-platformctl`, `dotw-vagrant`, `dotw-ai`, `dotw-kubernetes`, etc.

- Developed independently
- Each module ships releases via **tags** (SemVer-style)

### Integration repository (`dotw-integration`)

- Integrates module repos via **git submodules**
- Pins each module to a chosen stable release tag/commit
- Acts as the “single entry point” for cloning the DOTW ecosystem

---

## Branching (module repos)

- `main` — active development line
- `feature/<short-description>` — feature branches

Example branch names:

- `feature/add-lab-status`
- `feature/openshift-bootstrap`

---

## Merge policy (module repos)

1. Create feature branch from `main`
2. Develop + commit locally
3. Merge feature branch into `main` (PR optional, but recommended even for solo)
4. `main` stays releasable (or at least “not trash”)

---

## Releases (module repos)

- Releases are **tags on `main`**
- Tag format: `vMAJOR.MINOR.PATCH` (example: `v0.1.0`)

Typical flow:

1. Merge work into `main`
2. When you decide it’s stable → create a tag
3. Push the tag to origin

---

## Integration updates (dotw-integration)

When a module publishes a new stable tag, `dotw-integration` is updated by:

1. Enter the module submodule directory
2. Fetch tags
3. Checkout the desired tag (detached HEAD is expected)
4. Return to repo root
5. Commit the updated submodule pointer in `dotw-integration`

**Important:** The integration repo commits the *pointer*, not the module repo history.

---

## Optional: Stack releases (dotw-integration)

The integration repo may publish stack-level tags like:

- `stack-v0.2.0`
- `stack-2026.03`

These represent a complete pinned ecosystem snapshot.
