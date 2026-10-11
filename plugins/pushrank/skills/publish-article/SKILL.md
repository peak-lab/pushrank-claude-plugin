---
name: publish-article
description: Publish, schedule, or edit a Pushrank article on the user's CMS (WordPress, Webflow, Wix, Shopify, Framer, or webhook). Use when the user wants to put an article online, schedule it, change the automatic publishing cadence, or fix an article before it goes live.
---

# Publish an article with Pushrank

Answer in the user's language. Publishing changes the user's live website: confirm every write.

## 1. Find the article

`list_articles` (no full content), then `get_article` for the one the user means.

## 2. Edit before publishing (optional)

`edit_article` works in two steps:
1. `mode: preview` with the `changes` and the article's `updatedAt` as `expectedUpdatedAt`. Show the
   diff.
2. `mode: apply` with the same changes and `confirmed: true` once the user approves. A version conflict
   means someone edited the article meanwhile: reload it and preview again.

## 3. Check readiness

Call `get_article_publication_readiness`. It reports the quality verdict, CMS connection and whether
the article updates an existing CMS entry. If the CMS is not connected, use the `project-setup` skill.

## 4. Publish now or later

- **Now**: `publish_article_to_cms` with a new UUID `idempotencyKey`. If the quality gate failed, explain
  the failed checks. Set `acknowledgeQualityOverride: true` only when the user explicitly accepts
  publishing despite them. Then poll `get_workflow_status` with the `articleId` until done, and give
  the live URL.
- **Later**: `schedule_article_publication`; `cancel_article_publication_schedule` to undo it before
  the worker claims it. Scheduling keeps the quality gate: a failing article is not published.
- **Already published by hand**: `update_article_status` records it without touching the CMS.

## 5. Automatic cadence

`get_publishing_schedule` shows it. `update_publishing_schedule` previews a change, then applies it
after confirmation. Only drafts that pass the quality gate are published automatically.
