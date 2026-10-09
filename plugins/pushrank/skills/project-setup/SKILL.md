---
name: project-setup
description: Set up or complete a PushRank project. Use when the user is getting started with PushRank, asks what is left to configure, wants to connect their CMS, correct their business profile or brand voice, reanalyse a page, or claim the welcome backlink.
---

# Set up a PushRank project

Answer in the user's language. Start with `whoami` to see the account, organisations, granted scopes
and credits.

## Onboarding

`get_onboarding_checklist` shows the five steps (site analysis, Google Search Console, website
connection, 90-day SEO strategy, first content) and the next one. Google Search Console is connected
from the PushRank dashboard, not from Claude: give the link.

## CMS connection

1. `get_cms_config` shows the current state. Secret values are never returned.
2. `configure_cms` previews a WordPress, Webflow, Wix, Framer or webhook connection, then saves and
   tests it after confirmation. Ask the user to type secrets themselves; omit a secret to keep the
   stored one. Shopify is connected from the PushRank dashboard only. Saving requires the organisation
   owner role.

## Business profile and editorial context

These facts shape every generated article, so keep them accurate.

- `get_business_profile` lists facts with status and provenance. `edit_business_profile` previews a
  patch, then applies it after confirmation. Pass the `revision` read just before and reuse one
  idempotency key from preview to apply.
- `get_editorial_context` returns brand, offer, audience, tone and proofs. `edit_editorial_context`
  previews a diff, then applies it after confirmation.

## Page reanalysis

`get_page_reanalysis_readiness` reports the credit cost and balance. `reanalyze_page` spends credits:
state the cost and wait for an explicit yes.

## Welcome backlink

Once the five steps are done, `claim_welcome_gift` in preview first to validate the target page and
anchor text. Apply with `confirmed: true` only after the user approves both. One gift per organisation.
