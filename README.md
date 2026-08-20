# Miraqo MCP Server

Connect Claude, ChatGPT, Gemini, Claude Code or Cursor to your SEO data in
[Miraqo](https://miraqo.io) — rankings, technical audit, backlinks, competitors,
Search Console and AI visibility — and query it in plain language from the chat
you already use.

This is a **hosted, remote MCP server**. There is nothing to install and nothing
to run locally. This repository is documentation only.

```
https://app.miraqo.io/mcp
```

You need a Miraqo account. A 14-day free trial is available, no card required.

---

## Setup

### claude.ai, ChatGPT, Gemini — one click

Add a **custom connector** and paste the address above. A standard OAuth
authorization starts automatically: sign in to Miraqo, confirm, done. No token
to generate or paste.

Where you add a connector differs slightly between apps (and may depend on your
plan with that app), but the address is always the same.

You can revoke access at any time from **Account settings → AI Connector (MCP) →
Connected apps**.

### Claude Code

Generate a personal token in **Account settings → AI Connector (MCP)**, then:

```bash
claude mcp add --transport http miraqo https://app.miraqo.io/mcp \
  --header "Authorization: Bearer YOUR_TOKEN"
```

### Cursor and other token-based clients

```json
{
  "mcpServers": {
    "miraqo": {
      "url": "https://app.miraqo.io/mcp",
      "headers": { "Authorization": "Bearer YOUR_TOKEN" }
    }
  }
}
```

Tokens are shown **once** at creation. You can keep up to 5 active and revoke
them individually.

---

## Tools

26 tools. Start with `list_projects` to get the `project_id` the others take.

### Read — never consume plan quota

| Tool | What it returns |
| --- | --- |
| `list_projects` | Your projects, each with its latest audit (id, status, date, score) |
| `get_usage` | Month-to-date consumption against plan limits, including the MCP action cap |
| `get_keywords` | Tracked keywords with latest position, URL and AI Overview presence |
| `get_keyword_history` | Up to 365 days of position history for one keyword, with SERP features |
| `get_competitors` | Tracked competitors: average position and keyword-gap size |
| `get_keyword_gap` | Keywords a competitor ranks for, with volume, difficulty and CPC |
| `get_domain_analysis` | Cached competitive snapshot of any domain: authority, organic keywords, top pages |
| `get_backlinks` | Latest backlink snapshot: new, lost, referring domains, anchors, spam score |
| `get_audit_overview` | Score, pages crawled and what the latest audit produced |
| `get_audit_issues` | Non-zero issue counters: 404s, titles, duplicates, security, sitemap |
| `get_audit_pages` | Per-page status, title, word count, load/LCP/TTI and issue flags |
| `get_audit_redirects` | Redirect chains with `linked_from` — the pages where the fix belongs |
| `get_cwv_report` | Core Web Vitals: lab and field data, worst pages by LCP |
| `get_topical_architecture` | Topic clusters with their pillar pages, structural or AI-refined |
| `get_cluster_pages` | Pages in a cluster, ranked by inbound internal links |
| `find_pages` | Search crawled pages by URL or title substring |
| `get_ai_visibility` | Whether AI assistants mention your brand and cite your URLs, with share of voice |
| `get_gsc_performance` | Search Console by query or page, aggregated over 7/28/90-day windows |
| `get_gsc_daily` | Day-by-day Search Console site totals — the series to date a drop against |

### Actions — consume plan quota

Each also counts against a separate monthly cap on MCP-initiated actions. Check
`get_usage` before running them.

| Tool | What it does |
| --- | --- |
| `run_audit` | Starts a new technical crawl. Costs audit credits equal to the pages actually analysed |
| `run_keyword_research` | Volume, difficulty and CPC — by seed, list, domain, or gap against a competitor |
| `run_domain_analysis` | Refreshes a competitive snapshot. Reuses a snapshot newer than 7 days for free |
| `run_ai_visibility_check` | Re-runs the project's AI visibility prompts |
| `add_ai_prompt` | Creates an AI visibility prompt and runs the first check |
| `refine_topical_architecture` | AI pass over the audit's topic clusters. Once per audit |
| `generate_topical_bridge` | Writes a linking paragraph to connect two pages. Cached pairs are free |

Reads are unmetered, so exploring your data costs nothing.

---

## REST API

The same capabilities are available as a documented REST API under `/api/v1`,
for integrations that are not MCP clients. The link is in the AI Connector card
in your account settings.

## Notes

- Tool descriptions are currently served in Italian. The Miraqo interface is
  available in Italian, English, German, French and Spanish.
- Data scope follows your account: the server only ever exposes projects the
  authenticated token can already see, and respects per-user project permissions.

## Links

- [miraqo.io](https://miraqo.io)
- [AI Connector guide](https://miraqo.io/help/connettore-ai-mcp/)
- [Asking questions about your data](https://miraqo.io/help/chatta-con-i-tuoi-dati/)
- [Pricing](https://miraqo.io/prezzi/)

Issues and questions about the connector are welcome here. For account or
billing matters, write to supporto@miraqo.io.
