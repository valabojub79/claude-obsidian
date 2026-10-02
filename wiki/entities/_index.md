---
type: meta
title: "Entities Index"
updated: 2026-04-07
tags:
  - meta
  - index
  - entity
status: evergreen
related:
  - "[[index]]"
  - "[[Andrej Karpathy]]"
  - "[[hot]]"
  - "[[LLM Wiki Pattern]]"
---

# Entities Index

Navigation: [[index]] | [[concepts/_index|Concepts]] | [[sources/_index|Sources]]

All entity pages — people, organizations, products, and tools.

---

## People

- [[Andrej Karpathy]] — AI researcher, educator; originated the LLM Wiki pattern
- [[Alfred Adler]] — Austrian psychiatrist (1870-1937); founder of Individual Psychology (Adlerian Psychology)
- [[Ichiro Kishimi]] — Japanese philosopher; Adlerian counselor and translator; co-author of The Courage to be Disliked
- [[Fumitake Koga]] — Japanese writer; co-author of The Courage to be Disliked
- [[Kurt Lewin]] — social psychologist; 1939 study founding the study of leadership styles
- [[Bernard M. Bass]] — formalized transformational vs transactional leadership
- [[Robert K. Greenleaf]] — coined servant leadership ("The Servant as Leader", 1970)

---

## Organizations

- [[NVM Express Consortium]] — standards body publishing NVMe specifications (nvmexpress.org)

---

## Products & Tools

<!-- Add tool and product pages here -->

---

## OP-TEE

Pages live in `wiki/entities/optee/`. Ground truth: this machine's real checkout at `/home/bhaskarv/optee/` (the `OP-TEE/build` repo manifest).

- [[OP-TEE Build Repo]] — github.com/OP-TEE/build; repo-tool manifest + Makefiles orchestrating the whole checkout
- [[Trusted Firmware-A]] — BL1/BL2(/BL31); ARM's reference secure-boot firmware
- [[OP-TEE OS]] — the TEE itself, BL32
- [[U-Boot]] — BL33, normal-world bootloader
- [[Buildroot]] — normal-world rootfs builder for the QEMU target
- [[optee_client]] — libteec + tee-supplicant, GP Client API
- [[QEMU]] — emulated qemu_armv8a target board
- [[optee_test]] — xtest runner + ta/ test-TA collection
- [[optee_examples]] — reference host/TA example pairs (hello_world, aes, acipher, secure_storage, ...)

---

## Add new entities here as they are identified during ingests.
