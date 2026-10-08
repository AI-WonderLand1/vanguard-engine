# Fix transitive uuid #2 — October 8, 2026

This change targets Dependabot alert #2 (GHSA-w5hq-g745-h8pq, invalid output buffer bounds in v3/v5/v6).

Two copies are present in `package-lock.json`, both installed through Firebase tooling:
- `node_modules/uuid` 9.0.1 via `gaxios`.
- `node_modules/universal-analytics/node_modules/uuid` 8.3.2 via `universal-analytics`.

Both are changed to **uuid 11.1.1**, a patched release. Package tarball integrity and `resolved` source values are taken from an existing npm lockfile. The overrides match the upstream Firebase CLI project's scoped `uuid: ^11.1.1` approach.

**Required tests:** `npm ci`, `npm run lint`, `npm run build`, and Firebase CLI smoke test (`npx firebase --version`; `npx firebase --help`). These are major changes across transitive version ranges; verify installation and CLI operation before merge. A green Next.js build alone does not prove Firebase CLI compatibility.

Unresolved: `braces@3.0.3` has no patched upstream release. It comes from `chokidar` via `firebase-tools` and `micromatch` via Next ESLint `fast-glob`. Do not pass user-controlled glob expressions into build tools. Do not manually dismiss the braces alert.
