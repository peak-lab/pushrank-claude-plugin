# Pushrank for Claude

Pushrank is an SEO platform that turns your Google Search Console data into prioritised actions and
quality-gated articles, then publishes them to your CMS. This plugin connects Claude to your Pushrank
account and teaches it the Pushrank workflows, so you can run your SEO from a conversation.

## What it contains

- **Pushrank connector** — the remote MCP server at `https://ai.pushrank.io/mcp`. You sign in with your
  own Pushrank account through OAuth; Claude only sees the projects and scopes you grant.
- **Skills**
  - `seo-review` — weekly review of traffic, the GSC digest, and SEO opportunities.
  - `generate-article` — readiness checks, generation, and progress tracking.
  - `publish-article` — publication readiness, CMS publishing, scheduling, and cadence.
  - `manage-keywords` — keyword list, stored metrics, and safe bulk changes.
  - `project-setup` — onboarding checklist, business profile, editorial context, and CMS connection.

## Getting started

1. Add the plugin from **Customize > Plugins** in claude.ai.
2. Open the plugin's **Connectors** tab and connect Pushrank. Sign in and approve the requested scopes.
3. Ask Claude something like "What are my top SEO opportunities this week?".

In Claude Code:

```
/plugin install pushrank --marketplace peak-lab/pushrank-claude-plugin
```

A Pushrank account is required. Create one at [pushrank.io](https://pushrank.io).

## Safety

Every tool that writes (generation, publishing, edits, keyword changes, credit-metered analysis) asks
for your explicit confirmation first, and most show a preview before applying. Publishing never
bypasses the Pushrank quality gate unless you explicitly acknowledge the override.

## Data

The connector reads your Pushrank projects, retained Google Search Console data, articles, and
keywords. It never calls Google live and never returns stored CMS secrets. See the
[Pushrank privacy policy](https://pushrank.io/privacy-policy).

## Support

support@pushrank.io
