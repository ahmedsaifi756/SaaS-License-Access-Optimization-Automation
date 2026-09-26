# SaaS License / Access Optimization Automation

A lightweight n8n automation that identifies potentially underutilized SaaS licenses by reconciling license assignment data with user activity data.

The workflow helps IT teams identify licenses that may require review without automatically revoking user access.

---

## Business Problem

Organizations often assign SaaS licenses to employees, but not every assigned license is actively used.

This can create unnecessary software access and potentially avoidable SaaS spending.

The challenge is that license assignment data alone does not tell us whether a user is actually using the software.

This workflow combines:

- License assignment data
- User usage/activity data

and evaluates them using deterministic business rules.

---

## Workflow

```text
Manual Trigger
      ↓
License API
      ↓
License JSON
      ↓
                 ┌───────────────┐
Usage API ─────→ │ Merge License │
      ↓          │    + Usage    │
Usage JSON       └───────┬───────┘
                         ↓
               Evaluate License Usage
                         ↓
                  Prepare Findings
                         ↓
                PostgreSQL Database
                         ↓
                       Switch
                    ↙         ↘
               REVIEW       DATA_CHECK
                  ↓             ↓
               Slack          Slack
