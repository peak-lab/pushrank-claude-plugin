---
name: generate-article
description: Generate an SEO article with Pushrank. Use when the user asks to write, create, or generate an article or blog post, to act on a content-creation opportunity, or to produce the next item of their content plan.
---

# Generate an article with Pushrank

Answer in the user's language. Generation consumes article quota, so never start it without an
explicit request from the user.

## 1. Choose the source

- From the content plan: `list_content_plan`, then let the user pick an item.
- From an SEO opportunity: `list_seo_opportunities` with `type: content_creation`; keep its id.
- From scratch: ask for a short brief (topic, target keyword, angle) of at most 1000 characters.

## 2. Check readiness first

Call `get_article_generation_readiness`. Report quota, brief gaps, cannibalization and SERP warnings.

- If `canDispatch` is false, explain why and stop.
- If `projectContext.retry` is `available`, the project context rebuild failed. Offer
  `retry_project_context` (preview, then apply after the user agrees), then poll
  `get_article_generation_readiness` until the context is ready.
- Only set `acknowledgeWarnings: true` after the user has read the warnings and agreed to go ahead.

## 3. Start the generation

- Content-plan item: `generate_article_from_plan_item` with `confirmed: true`.
- Otherwise: `generate_article` with the brief and optional `opportunityId`. Create two UUIDs:
  `generationIntentId` stays the same across retries of this same request; `idempotencyKey` is new for
  each dispatch attempt.

## 4. Follow progress

Generation takes several minutes. Poll `get_workflow_status` with the returned `requestId` at a calm
pace, and tell the user they can come back later. When it completes, `get_article` and summarise the
title, word count, quality verdict and any failed quality checks. Offer the `publish-article` skill
next; do not publish on your own.
