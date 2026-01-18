# n8n-automations-blanketfort
A repository of automations &amp; experiments
What’s included

1) AI Newsletter Workflow (v2)

Goal: Generate a weekly newsletter from researched sources using an agentic workflow (plan → write sections → edit → send).

High-level flow
	•	Scheduled trigger runs weekly
	•	Pulls research results (web search)
	•	Planning step selects a theme and generates exactly 3 topics (structured output)
	•	Splits into 3 parallel topic paths
	•	Research + section-writing per topic
	•	Aggregates sections
	•	Final editor agent merges into one cohesive HTML email (structured output)
	•	Sends via email

Why it matters
This is a realistic “starter → intermediate” example because it combines:
	•	Multi-step LLM usage (planner + writers + editor)
	•	Structured output parsing (schema-based validation)
	•	Fan-out / fan-in orchestration
	•	Real delivery (email output)

Reliability upgrades in v2 (office-hours ready)
	•	Branching/fallbacks for empty research results
	•	Placeholder for internal/proprietary context (e.g., brand voice rules, internal notes)
	•	Basic run logging placeholder (so teams can debug what happened)
	•	Clear separation of responsibilities between nodes (planner vs writer vs editor)

Note: The JSON is intended to be shared and imported. Credentials are not included in the sanitized version; you remap them on import.

⸻

2) Proprietary Data Ingest Demo

Goal: Ingest internal CSV data, validate and clean it, dedupe via an idempotency key, then upsert into a datastore/CRM. Quarantine bad rows for review.

High-level flow
	•	Trigger (manual for demo; typically Cron or file trigger in production)
	•	Download internal CSV (placeholder URL or Drive/Dropbox/DB connector)
	•	Parse into rows
	•	Process in batches (so it scales)
	•	Normalize fields (trim, lower-case email, standardise names)
	•	Generate an idempotency key to prevent duplicates
	•	Validate required fields
	•	Valid rows → Upsert path
	•	Invalid rows → Quarantine path
	•	Log each processed row and send a completion notification

Why it matters
This is the “real business” automation pattern that finance/sales/marketing teams actually use:
	•	messy inputs
	•	schema drift
	•	duplicates
	•	partial records
	•	fragile downstream APIs
	•	audit requirements

It demonstrates the exact mentoring moments that usually cause blockers:
	•	parsing + data typing
	•	IF logic and routing
	•	retries/backoff
	•	idempotency/upserts
	•	debugging with logs

⸻

Key patterns demonstrated (the stuff that wins office hours)
	•	Branching logic: route execution paths based on conditions (missing fields, empty results, invalid model output)
	•	Structured outputs: schema-driven parsing so LLM output is validated, not guessed
	•	Idempotency: avoid duplicates using a deterministic key (e.g., lead:<email>)
	•	Quarantine pattern: don’t “fail the whole run” because one row is bad
	•	Batch processing: scale safely with Split In Batches
	•	Retries/backoff: reduce breakage from rate limits and flaky APIs
	•	Observability: basic logging so debugging is fast and calm during live troubleshooting

⸻

Setup notes

Credentials

These workflows are designed to be shared. On import, you will need to:
	•	connect your own API keys (LLM provider, search tool, email provider, datastore/CRM)
	•	replace placeholder endpoints (e.g., internal context, logging, upsert/quarantine endpoints)

Placeholders to replace

You’ll see URLs like:
	•	https://internal.example.com/brand-context
	•	https://internal.example.com/workflow-logs
	•	https://internal.example.com/crm/upsert
	•	https://internal.example.com/data/quarantine

Swap these for:
	•	Google Drive/Notion/DB lookups for internal context
	•	Slack/Teams + a logging table (Sheets/Airtable/Postgres) for visibility
	•	Airtable/HubSpot/Postgres for upsert/quarantine destinations

⸻

Suggested extensions (if you want to take it from demo → production)
	•	Add a global error workflow (n8n Error Trigger) that posts failures with execution URLs
	•	Add a “dead letter queue” (quarantine store) with retry ability after fixes
	•	Add source deduplication + quality scoring in the newsletter research step
	•	Add PII handling rules and redaction before logs (if needed for compliance)

⸻

Who this is for
	•	teams learning n8n + LLM workflows in a structured certification program
	•	mentors running office hours where people debug live in front of others
	•	orgs moving from “cool demo” to “reliable workflows that run every week”

⸻

If you want, I can also rewrite this as a tighter README (shorter, more “product-y”) or as a trainer-focused README (more emphasis on teaching points and common failure modes).
