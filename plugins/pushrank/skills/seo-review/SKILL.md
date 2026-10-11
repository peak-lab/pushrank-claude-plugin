---
name: seo-review
description: Review a Pushrank project's SEO performance and decide what to work on. Use when the user asks how their site is doing, what changed in Google Search Console, what their SEO priorities or quick wins are, or wants a weekly SEO review.
---

# SEO review with Pushrank

Answer in the user's language. Use only the Pushrank connector; never invent metrics.

## 1. Pick the project

- Call `list_projects`. If there is exactly one project, use it. Otherwise ask which one, showing names
  and domains, unless the user already named it.

## 2. Build the picture

1. `get_project_overview` for traffic and status counts.
2. `get_gsc_digest` for the latest weekly digest. If its status is `pending`, `skipped` or `failed`,
   say so plainly instead of summarising stale data.
3. `list_seo_opportunities` with the default `status: active`. Sort by priority, then severity.
   Narrow with `type` (for example `quick_win`, `decay`, `low_ctr`, `cannibalization`) when the user
   asks about one kind of problem.
4. Use `get_gsc_snapshot` only for a precise question (a page, a query, a period comparison). It reads
   retained snapshots, so pick a period from `availablePeriods` and keep `compareTo` the same length.

## 3. Report

- Lead with three to five actions, each naming the page or query, the opportunity type, and why it
  matters (clicks, impressions, position, CTR).
- Group the rest in one short line per type. Do not paste raw tool output.
- Link each action to the next Pushrank step: a `content_creation` opportunity leads to the
  `generate-article` skill; a `decay` or `low_ctr` one to editing the existing article.

## 4. Triage (writes)

`update_seo_opportunity_status` changes Pushrank data. Call it only when the user asks to mark an
opportunity. Allowed transitions: `todo` to `in_progress`, `done` or `ignored`; `ignored` only goes back
to `todo`. When ignoring, pass an `ignoredReason` if the user gave one. A missing
`mcp:actions:write` scope means the user must reconnect Pushrank and grant it.
