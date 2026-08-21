# Publication Audit

## Decision

**PUBLIC PORTFOLIO REPOSITORY: PASS**

## Publication Strategy

The full development repository remains private.

This public repository was created from a curated package so its history does not expose unpublished source mappings or internal policy material.

## Checks Completed

- Current public branch tree reviewed after publication
- Public commit history reviewed
- Current repository searched for common secret patterns
- Git history searched for common token, password, and private-key patterns
- Commit identities reviewed for personal email exposure
- Current and historical filenames reviewed for databases, logs, backups, exports, and credential files
- `appsettings.json` reviewed in the private source archive before publication
- Windows publish profile reviewed in the private source archive before publication
- Local application-data path implementation reviewed before publication
- Markdown links and screenshot paths validated
- Screenshots reviewed visually
- Uploaded PNG files checked for complete PNG endings
- PNG metadata checked and found empty in the publication package
- Stale publication hash manifest removed after upload
- Public repository assembled without production source history, databases, logs, backups, exports, or release ZIPs

## Private-Only Material Excluded

- Source alignment report
- Historical private source filenames and SHA-256 mappings
- Unpublished user-specific policy material
- Internal UI audit reports containing obsolete policy wording
- Full private development history
- Production source files that embed private source metadata

## Curated Material Included

- Recruiter-facing README
- Product and UX case study
- Architecture overview
- Condensed illustrative code example
- QA and release summary
- Privacy and data-design summary
- v1.1.1 release notes
- v1.1.1 final acceptance report
- Four sanitized screenshots
- Security reporting policy

## Ongoing Protection

The repository includes a GitHub Actions workflow that checks out full history and runs Gitleaks on pushes and pull requests. Third-party actions are pinned to immutable commit SHAs, checkout credentials are not persisted, and the workflow receives read-only repository contents permission.

No audit can prove the mathematical absence of all sensitive information, so future additions should still receive manual review before publication.
