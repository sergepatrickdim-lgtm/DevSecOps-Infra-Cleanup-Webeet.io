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

---

## PR #704 — chore(appdb): remove legacy cloud-init templates and dead filebeat_config_content variable

✅ **Merged** — 1 commit · 8 files changed · -773 lines  
Merged by: evangelostsak  
Reviewed by: evangelostsak · pragepani · AlejandroRomanIbanez  
Branch: `feat/cleanup-app-db` → `feat/cleanup`

### Summary

Removed orphaned cloud-init templates, inline scripts, and dead module variables from the AppDB module that were replaced by Ansible roles.

### Changes — 8 Files

**Deleted templates:**
- `aws-infra/modules/appdb/templates/cloud-init.yaml.tftpl`
- `aws-infra/modules/appdb/templates/filebeat.yml.tftpl`
- `aws-infra/modules/appdb/templates/update-app.sh.tftpl`
- `aws-infra/modules/appdb/templates/backup.sh.tftpl`
- `aws-infra/modules/appdb/pgbouncer.ini`

**Dead variable removed:**
- Removed `filebeat_config_content` from `modules/appdb/variables.tf`
- Removed `filebeat_config_content` templatefile call from `environments/dev/main.tf`
- Removed `filebeat_config_content` templatefile call from `environments/qa/main.tf`

### Why

The AppDB module already uses the shared `ansible-bootstrap.yaml.tftpl`. These files and variables were unreferenced dead code, fully replaced by Ansible roles.

### Testing
- Verified no remaining references to deleted files via `grep`
- `terraform validate` blocked by missing AWS backend credentials (pre-existing environment issue, unrelated to this change)

---

## Combined Impact — PR #704 + PR #705

| Metric | Value |
|---|---|
| Total files deleted | 22 |
| Total lines removed | -2,403 |
| Environments cleaned | `dev` + `qa` |
| Modules cleaned | `appdb` + ELK stack |
| Dead code categories | Cloud-init · Filebeat · Docker Compose · APM · Kibana · Security scripts · Dead variables |

`Terraform` · `Ansible` · `AWS` · `ELK Stack` · `Docker Compose`

---

## Screenshots

> See `/screenshots/` folder — includes PR overview with full change list and files changed view.

---

*Part of a DevSecOps internship at Webeet.io (Jan 2025 – Mar 2026). Code belongs to Webeet.io — this repo documents the work via PR screenshots and technical write-up.*
