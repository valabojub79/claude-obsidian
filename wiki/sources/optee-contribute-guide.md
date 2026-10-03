---
type: source
title: "OP-TEE Contribution Process"
source_url: https://optee.readthedocs.io/en/latest/general/contribute.html
author: "OP-TEE project (Linaro)"
format: documentation
date_ingested: 2026-10-02
created: 2026-10-02
updated: 2026-10-02
tags:
  - source
  - optee
  - trusted-execution
  - contribution
  - documentation
status: ingested
address: c-000043
related:
  - "[[OP-TEE Contribution Workflow]]"
  - "[[OP-TEE Coding Standards]]"
sources:
  - "https://optee.readthedocs.io/en/latest/general/contribute.html"
---

# OP-TEE Contribution Process

Canonical contribution-process page from the official OP-TEE docs (optee.readthedocs.io). Fetched 2026-10-02.

## What this source covers

- **DCO / Signed-off-by**: every patch needs `Signed-off-by: Real Name <email>`: pseudonyms/anonymous contributions disallowed. Four Linux-kernel-style DCO certifications apply (own work or right to submit it; based on prior OSS work you can legally modify; passed through unmodified from someone else's certified contribution; understand the record is public/permanent).
- **Commit message format**: subject ≤80 chars, usually prefixed with the affected area (e.g. `core: pta: ...`); body wrapped at 72 chars (exception: error strings, URLs); blank line before trailing tags; commit citations use a 12-digit SHA1 prefix + quoted subject.
- **Tags**: `Signed-off-by:` mandatory; `Tested-by:`, `Acked-by:`, `Suggested-by:`, `Reported-by:` optional.
- **Workflow**: no direct write access: fork, branch, open a PR against the upstream repo (e.g. OP-TEE/optee_os). During review, push fixup commits without squashing/force-pushing; wait for `Acked-by:`/`Reviewed-by:` from reviewers. Once approved: `git rebase -i` to squash fixups into the real commits, add the reviewers' tags, force-push, tell the maintainer it's ready to merge.
- The PR template (seen locally in `optee_os/.github/pull_request_template.md`) additionally asks contributors to disclose in the PR description if AI was used to help write/generate any part of the patch.

## Not covered by this page

checkpatch usage and patch-splitting strategy live on the separate [[optee-coding-standards]] page instead.
