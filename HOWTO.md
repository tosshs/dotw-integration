# HOWTO — dotw-integration

Practical operations for the DOTW integration repo.

---

## Clone everything (recommended)

```bash
git clone --recurse-submodules https://github.com/tosshs/dotw-integration.git
```

## If already cloned without submodules

```bash
git submodule update --init --recursive
```

### Add a new module as a submodule

From the root of dotw-integration

1. Add the submodule:

```bash
git submodule add https://github.com/tosshs/<repo>.git <repo>
```

Example:

```bash
git submodule add https://github.com/tosshs/dotw-terraform.git dotw-terraform
```

1. Pin it to a stable release tag:

```bash
cd <repo>
git fetch --tags
git checkout v0.1.0
cd ..
```

1. Commit the integration pointer:

```bash
git add .gitmodules <repo>
git commit -m "Add <repo> submodule pinned to v0.1.0"
git push
```

### Bump ONE module to a new stable tag (example: v0.2.0)

1. In the module repo itself, tag a stable release and push it:

```bash
git checkout main
git pull
git tag v0.2.0
git push origin v0.2.0
```

1. In dotw-integration, move the submodule to that tag:

```bash
cd dotw-platformctl
git fetch --tags
git checkout v0.2.0
cd ..
```

1. Commit the updated pointer:

```bash
git add dotw-platformctl
git commit -m "Bump dotw-platformctl to v0.2.0"
git push
```

### Bump the WHOLE STACK to v0.2.0

Repeat “Bump ONE module…” for every submodule that has a v0.2.0 tag.

1. Then commit once (if you staged multiple bumps before committing):

```bash
git add -A
git commit -m "Bump DOTW stack to v0.2.0"
git push
```

1. Optional: tag the integration repo as a stack release:

```bash
git tag stack-v0.2.0
git push origin stack-v0.2.0
```

### Inspect what is pinned right now

```bash
git submodule status
```

Save and close.

## Step 4 — Commit and push the docs

Back in PowerShell:

```powershell
cd D:\IT\repos\dotw-integration
git add README.md WORKFLOW.md HOWTO.md
git commit -m "Add integration docs (README, workflow, how-to)"
git push
```

## Quick “fancy check”

```bash
git show --name-only --oneline -1
```

## Tag the stack release in dotw-integration

After all bumps:

```bash
git tag stack-m07-v0.2.0
git push origin stack-m07-v0.2.0
```
