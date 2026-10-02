---
type: concept
title: "OP-TEE Contribution Workflow"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - contribution
  - github-workflow
complexity: beginner
domain: trusted-execution
status: developing
address: c-000059
related:
  - "[[optee-contribute-guide]]"
  - "[[OP-TEE Coding Standards]]"
sources:
  - "[[optee-contribute-guide]]"
---

# OP-TEE Contribution Workflow

Practical summary: full detail in [[optee-contribute-guide]].

## End-to-end

1. **Fork** the target repo (e.g. `OP-TEE/optee_os`): no one outside the project has direct write access.
2. **Branch, commit.** Every commit needs `Signed-off-by: Real Name <email>` (DCO: real identity required, no pseudonyms). Subject line ≤80 chars, often prefixed by area (`core: pta: ...`, `plat-qemu: ...`); body wrapped at 72 chars (URLs/error strings exempt); blank line, then tags.
3. **Run checkpatch** before opening the PR: see [[OP-TEE Coding Standards]].
4. **Open a PR** against the upstream repo. Mention in the PR description if AI assistance was used to write/generate any part of the patch (separate from any commit-level AI-attribution tag).
5. **Review loop**: address feedback with *fixup* commits on top: do **not** squash or force-push yet. Ping reviewers once addressed. Wait for `Reviewed-by:`/`Acked-by:` (and optionally `Tested-by:`) from each reviewer.
6. **Finalize**: once approved, `git rebase -i` to squash fixups into the real commits, add the reviewers' tags into the commit messages, force-push the cleaned-up branch, tell the maintainer it's ready.
7. A maintainer merges to `master`: merge access is restricted to maintainers (see `optee_os/MAINTAINERS`; patches are **not** sent by email, only via GitHub PR).

## First-contribution tips

- Check `MAINTAINERS` for who actually owns the area you're touching (platform-specific code has sub-maintainers): mention them (`@handle`) on the PR if it stalls.
- Security-sensitive areas (anything in [[Secure Boot Chain of Trust]]'s territory, crypto, memory isolation) warrant discussing the approach in an issue *before* investing in a full patch.
