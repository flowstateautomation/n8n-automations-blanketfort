# n8n-automations-blanketfort
A repository of automations &amp; experiments
What’s included

# n8n-automations-blanketfort

A small collection of n8n automations built as **training + mentoring examples**.

These workflows are structured to be easy to teach in office hours:
- clear node responsibilities
- common failure modes handled with branching
- “production-ish” patterns (validation, idempotency, logging placeholders)

## What’s in this repo

### 1) AI Newsletter Workflow (v2)
**File:** `Amits Newsletter Workflow v2`  [oai_citation:1‡GitHub](https://github.com/flowstateautomation/n8n-automations-blanketfort/tree/main)

**Goal:** Generate a newsletter using an agentic flow:
**research → plan → write sections → edit → send**

**What it demonstrates**
- scheduled runs
- multi-step LLM usage (planner + writers + editor)
- structured outputs (schema parsing)
- fan-out / fan-in orchestration (split topics, aggregate sections)
- email delivery

**Why this is useful for training**
Most beginners can “make it work once”.
This workflow is useful because it shows the next step: how to keep it stable when:
- sources are empty or low quality
- LLM output format breaks
- APIs time out or rate-limit

**v2 additions (vs a basic newsletter)**
- branching + fallback search path
- placeholder “internal/proprietary context” step (brand rules / internal notes)
- placeholder run logging step (so debugging is faster)

---

### 2) Proprietary Data Ingest Demo
**File:** `Claritas - Proprietary Data Ingest Demo.json`  [oai_citation:2‡GitHub](https://github.com/flowstateautomation/n8n-automations-blanketfort/tree/main)

**Goal:** Ingest internal CSV data and run it through a practical pipeline:
**download → parse → validate → dedupe → upsert → quarantine → log/notify**

**What it demonstrates**
- batch processing (so it scales)
- schema validation + quarantine path (don’t fail the whole run)
- idempotency (prevent duplicates using a deterministic key)
- retry/backoff-ready HTTP patterns (for fragile APIs)
- basic observability (logging placeholder)

**Why this matters**
This is the kind of workflow finance/sales/marketing teams actually end up needing:
messy data, duplicates, partial rows, and downstream systems that fail in annoying ways.

---

## How to use these workflows

### Import into n8n
1. Open n8n
2. Go to **Workflows → Import from File**
3. Import one of the JSON files in this repo

### Connect credentials
These exports are intended to be shareable.
You’ll need to connect your own credentials on import (examples):
- LLM provider (OpenRouter/OpenAI/etc.)
- web research tool (Tavily or equivalent)
- email provider (Gmail/SMTP/etc.)
- datastore/CRM (Airtable/HubSpot/Postgres/etc.)

### Replace placeholders
Some nodes use placeholder URLs like:
- `https://internal.example.com/brand-context`
- `https://internal.example.com/workflow-logs`
- `https://internal.example.com/crm/upsert`
- `https://internal.example.com/data/quarantine`

Swap these to match your stack (Drive/Notion/Sheets/DB, Slack/Teams logging, etc.).

---

## Patterns used (the “office hours” bits)

- **Branching logic:** route execution paths based on conditions
- **Structured output parsing:** schemas to validate LLM output (less guesswork)
- **Idempotency:** avoid duplicates (keyed upsert pattern)
- **Quarantine path:** isolate bad inputs instead of failing everything
- **Batching:** safe processing for larger datasets
- **Observability:** log runs so debugging is calm and quick

---

## Suggested next additions
If you want to take these from “demo” to “production-like”:

- add a global **Error Trigger** workflow that alerts with execution URL + failed node
- add a dead-letter retry process for quarantined rows
- redact PII from logs (depending on compliance needs)
- add source quality scoring + dedupe for newsletter research

---

## Notes
These workflows are provided as examples.
They may include opinionated prompt styles and placeholder endpoints that you should adapt for your environment.
