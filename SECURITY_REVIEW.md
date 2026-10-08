# Security and build review (2026-10-08)

This is an isolated review branch. Do not claim all dependencies, the native engine, or Android runtime are secured or working until CI and device testing pass.

## Changes

- Pin transitive `@modelcontextprotocol/sdk` to **1.32.1**. The pinned npm archive integrity was copied from an independently published npm lockfile; CI must still validate installation.
- Add CI with `npm ci`, ESLint, Next.js build and an informational `npm audit`. The audit is not a passing security certificate.
- Desktop C++ build remains unverified: the README notes that SDL3, Jolt, ImGui, Tracy and other native dependencies are not fully installed.


## Unresolved risks

- `braces@3.0.3` remains present (under `micromatch` / `chokidar`) and **has no upstream patched release** (GHSA-vfj7-8cjw-p6xm). Never process attacker-controlled deeply nested brace/glob patterns until removed or isolated.
- `app/api/gemini/route.ts` accepts unauthenticated POST prompts, allows caller-supplied system instructions, and relays raw provider error messages. If publicly deployed with `GEMINI_API_KEY`, it is exposed to quota exhaustion/cost abuse. Add authentication, per-user quotas, body caps, and generic error responses before production exposure.
- Verify other `npm audit` findings, supply chain, GitHub Actions security, and C++ dependencies.

