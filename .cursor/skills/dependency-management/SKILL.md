---
name: dependency-management
description: Manage third-party dependencies—upgrades, semver, lockfiles, and risk reduction. Use when adding packages, bumping versions, or auditing supply chain.
---

# Dependency management

## When to Use

- Adding or removing a library
- Planning major version upgrades
- Responding to security advisories

## Instructions

1. **Need vs want.** Prefer stdlib or existing deps; add a dependency only when it clearly reduces long-term cost.
2. **Evaluate.** Check maintenance (releases, issues), license, bundle size (for frontends), and transitive footprint.
3. **Pinning.** Use lockfiles in applications; libraries may declare ranges—follow ecosystem norms.
4. **Upgrades.** Read changelogs; upgrade incrementally for large jumps; run full test suite and smoke critical flows.
5. **Security.** Monitor advisories; automate updates where safe; document exceptions when you cannot upgrade yet.
6. **Supply chain.** Prefer signed or provenance-backed packages when available; audit post-install scripts.

## Checklist

- [ ] License is compatible with the project
- [ ] Upgrade path and rollback are considered for production services
