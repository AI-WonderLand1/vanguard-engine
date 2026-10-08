# Dependency security update (October 8, 2026)

Next.js updated from 15.5.25 to **15.5.27**, addressing reported SSG/ISR cache poisoning advisories #70 and #71.
`source-map-js` updated from 1.2.1 to **1.2.2**, addressing event-loop DoS alert #67.
`fast-uri` updated from 3.1.7 to **3.1.8** alongside the parent dependency refresh.

Updated lockfile metadata (including integrity) comes from GitHub Dependabot's existing mobile Vanguard PR #3. Both projects use the same npm dependency graph. Use **npm ci**, **npm run lint**, and **npm run build** in CI to confirm before merge.

### Still requires follow-up / verification

- Scoped npm override forces Next.js's bundled PostCSS from vulnerable 8.4.31 to patched **8.5.27** (alerts #1, #5, #6, #9). This changes Next's upstream dependency resolution: **do not merge unless `npm ci`, lint, and build pass**, and confirm no runtime regression.
- `braces@3.0.3` still has no upstream patched version; avoid accepting user-controlled glob patterns in affected tools.
- Old `uuid@9.0.1` and `universal-analytics/uuid@8.3.2` remain transitive. Major upgrades require parent compatibility checks.
- Any other outstanding GHSA findings should be validated against the GitHub Dependabot alert page; no alerts have been dismissed manually.
