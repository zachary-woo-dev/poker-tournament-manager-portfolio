# Publication Audit

## Decision

**PUBLIC PORTFOLIO PACKAGE: PASS FOR FRESH REPOSITORY CREATION**

## Publication Strategy

The full development repository remains private.

A fresh public repository should be created from this curated package so the public history does not expose unpublished source mappings or internal policy material.

## Checks Completed

- Current repository searched for common secret patterns
- Git history searched for common token, password, and private-key patterns
- Commit identities reviewed for personal email exposure
- Current and historical filenames reviewed for databases, logs, backups, exports, and credential files
- `appsettings.json` reviewed
- Windows publish profile reviewed
- Local application-data path implementation reviewed
- Screenshots reviewed visually
- PNG metadata checked and found empty
- Public package assembled without source history, databases, logs, backups, exports, or release ZIPs

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
- QA and release summary
- Privacy and data-design summary
- v1.1.1 release notes
- v1.1.1 final acceptance report
- Four sanitized screenshots
- Security reporting policy

## Ongoing Protection

The package includes a GitHub Actions workflow that scans the full repository history with Gitleaks on pushes and pull requests.

No audit can prove the mathematical absence of all sensitive information, so future additions should still receive manual review before publication.
