# chore(elk): remove legacy cloud-init templates, docker-compose and security scripts — PR #705

**Webeet.io · DevSecOps Internship · Mar 2026**  
✅ **Merged** — 1 commit · 14 files changed · -1,630 lines  
Merged by: evangelostsak  
Reviewed by: pragepani · evangelostsak · AlejandroRomanIbanez  
Branch: `feat/cleanup-elk-templates` → `feat/cleanup`

---

## Summary

Removed orphaned ELK cloud-init files, inline Docker Compose templates, and legacy security deployment scripts that had been superseded by the `elk_stack` and `elk_config` Ansible roles — improving audit readiness, reducing codebase noise, and eliminating 1,630 lines of dead infrastructure code.

---

## Problem

The infrastructure codebase contained a large volume of unreferenced dead code — legacy cloud-init templates, inline Docker Compose ELK templates, APM server configs, Kibana dashboard definitions, and security scripts — all superseded by proper Ansible roles but never cleaned up. This created confusion, audit risk, and maintenance overhead.

---

## Changes — 14 Files Deleted

### Cloud-Init Templates
- `aws-infra/environments/dev/cloud-init-elk.tpl`
- `aws-infra/environments/qa/cloud-init-elk.tpl`

### Docker Compose Templates
- `aws-infra/environments/dev/templates/docker-compose.elk.yml.tftpl`
- `aws-infra/environments/qa/templates/docker-compose.elk.yml.tftpl`

### APM Server Templates
- `aws-infra/environments/dev/templates/apm-server.yml.tftpl`
- `aws-infra/environments/qa/templates/apm-server.yml.tftpl`

### ELK Security Rules
- `aws-infra/environments/dev/templates/elk-security-rules.yml`
- `aws-infra/environments/qa/templates/elk-security-rules.yml`

### Kibana Dashboard Definitions
- `aws-infra/environments/dev/templates/kibana-dashboards.ndjson`
- `aws-infra/environments/qa/templates/kibana-dashboards.ndjson`
- `aws-infra/environments/dev/templates/kibana-security-dashboard.ndjson`
- `aws-infra/environments/qa/templates/kibana-security-dashboard.ndjson`

### Legacy Security Scripts
- `scripts/security/deploy-siem.sh`
- `scripts/security/convert-rules.py`

---

## Why

These files were unreferenced dead code fully superseded by the `elk_stack` and `elk_config` Ansible roles. Keeping them created:
- **Audit risk** — outdated configs could be mistaken for active infrastructure
- **Maintenance overhead** — dead code requires review during every change
- **Codebase integrity** — orphaned templates inflate the codebase without adding value

---

## Impact

| Metric | Value |
|---|---|
| Files deleted | 14 |
| Lines removed | -1,630 |
| Environments cleaned | `dev` + `qa` |
| Dead code categories | Cloud-init · Docker Compose · APM · Kibana · Security scripts |

---

## Tech Stack

`Terraform` · `Ansible` · `AWS` · `ELK Stack` · `Docker Compose`

---

## Screenshots

> See `/screenshots/` folder — includes PR overview with full change list and files changed view.

---

*Part of a DevSecOps internship at Webeet.io (Jan 2025 – Mar 2026). Code belongs to Webeet.io — this repo documents the work via PR screenshots and technical write-up.*
