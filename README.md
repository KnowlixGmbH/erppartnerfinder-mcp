# ERP Partner Finder – MCP server & data schema

Open interface to [erppartnerfinder.com](https://erppartnerfinder.com), an independent, rule-based directory of the
Odoo implementation partners in Germany, Austria and Switzerland (≈190 partners, updated weekly).

- **Remote MCP server:** `https://erppartnerfinder.com/api/mcp` (Streamable HTTP, no API key; agents can look up and prepare requests, only the buyer can send them)
- **JSON feed:** `https://erppartnerfinder.com/api/partners` (`?country=DE|AT|CH`) — schema in [`schema/partner.schema.json`](schema/partner.schema.json)
- **Ranking and matching rules:** https://erppartnerfinder.com/en/how-we-rank

> Operated by Knowlix GmbH, itself an Odoo partner and listed under the same published rules. Not affiliated with or
> endorsed by Odoo S.A. Company data only — no personal data.

## Tools

| Tool | What it does |
|---|---|
| `search_partners` | Filter by country, city, tier (gold/silver/ready), app specialism, industry focus or text; ranked by the published formula |
| `get_partner` | Full profile: odoo.com figures (tier, references by industry, certified experts, project sizes, retention) and facts from the partner's own website (services, prices, AI-assisted delivery, hosting, languages) |
| `match_partners` | Rule-based shortlist (up to 5) for a project — country, industry, size, apps, languages — with the reasons for each match |
| `prepare_request` | Saves the project answers (no personal data) and returns a link where the buyer adds their own contact details, confirms by email and chooses the partners. Agents never send anything to partners |
| `directory_stats` | Partners per country and tier, medians per tier, pricing transparency, cities and app specialisms |

## Connect

**Claude Code**

```bash
claude mcp add --transport http erppartnerfinder https://erppartnerfinder.com/api/mcp
```

**Claude Desktop / Cursor / other clients** (`mcpServers` config)

```json
{
  "mcpServers": {
    "erppartnerfinder": { "url": "https://erppartnerfinder.com/api/mcp" }
  }
}
```

Clients that only speak stdio:

```json
{
  "mcpServers": {
    "erppartnerfinder": { "command": "npx", "args": ["-y", "mcp-remote", "https://erppartnerfinder.com/api/mcp"] }
  }
}
```

## Example prompts

- "Which Odoo Gold partners have an office in Vienna?"
- "Shortlist Odoo partners for a 40-user manufacturing company in Switzerland switching from SAP Business One."
- "What do Odoo partners in Germany charge for an implementation, according to their websites?"

## Data sources and rules

Tier, references, certified experts, project sizes and retention come from the public Odoo partner directory
(odoo.com/partners). Website facts are summarised from each partner's own website with the same rules for every
partner. Every partner is ranked by the same published formula; there are no paid placements. Partners can correct
their profile for free.

## Terms

This repository only documents the public interface — it contains no application code and no data.
© Knowlix GmbH. You may use the MCP server, the JSON feed and the schema to look up and cite partners, with a link to
the partner's profile on erppartnerfinder.com. Please don't bulk-copy or republish the data.
