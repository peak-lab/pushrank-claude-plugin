---
name: manage-keywords
description: Inspect and manage the keywords a PushRank project targets. Use when the user asks which keywords they track, their volume, difficulty or intent, which ones lack an article, or wants to add, prioritise, or archive keywords.
---

# Manage keywords with PushRank

Answer in the user's language.

## Read

- `list_keywords` returns metrics, status, priority, intent and article coverage. Highlight keywords
  with high priority and no article: they feed the `generate-article` skill.
- `get_keyword_metrics` returns stored metrics for up to 20 terms. It never calls a data provider; a
  `missing` or `stale` state means PushRank has no fresh data, so say so instead of guessing.

## Change (writes)

`manage_keywords` adds keywords, updates one, or changes statuses in bulk.

1. Call it in preview mode and show exactly what will change.
2. After the user confirms, apply with the same payload and one idempotency key reused from the
   preview.

Adding keywords never spends provider credits. A missing `mcp:keywords:write` scope means the user must
reconnect PushRank and grant it.
