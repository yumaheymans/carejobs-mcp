# CareJobs.Now MCP server

A free, hosted, read-only [Model Context Protocol](https://modelcontextprotocol.io) server for **US healthcare jobs**. It lets Claude, ChatGPT, Cursor, VS Code and other MCP clients search the open jobs that [CareJobs.Now](https://carejobs.now) reads every day from the career sites of 258 hospitals, health systems, clinic groups and care companies (170,000+ openings), with the pay each employer posts. Every answer links to the job's page on CareJobs.Now, where the user applies on the employer's own site.

- **Endpoint:** `https://carejobs.now/api/mcp`
- **Transport:** Streamable HTTP (legacy clients that open with `initialize` are served too)
- **Auth:** none. Public, read-only, no API key, free.
- **Official MCP Registry:** `now.carejobs/healthcare-jobs`
- **Docs and data:** https://carejobs.now/data

## Tools

| Tool | What it does |
| --- | --- |
| `search_healthcare_jobs` | Search open US healthcare jobs by words (a unit, a shift, a town), kind of job, state, shift and pay. Returns title, employer, kind of job, posted pay, shift, place and a link to the job. |
| `get_healthcare_pay` | Posted hourly pay by kind of healthcare job (median and typical range, with the number of rates and employers behind it). |
| `get_healthcare_job_market` | How many healthcare jobs are open, how many were first listed in the last 7 days, and who is hiring. |
| `get_healthcare_jobs_by_state` | Open jobs and employers per US state, or for one state by kind of job. |
| `list_healthcare_employers` | The hospitals, health systems, clinic groups and care companies whose jobs CareJobs.Now reads. |
| `get_healthcare_employer` | One employer: what it is, where it hires, its open jobs and the pay it posts. |

## Connect

**Claude (claude.ai, Claude Desktop) and ChatGPT:** add a custom connector with the URL `https://carejobs.now/api/mcp` (no authentication).

**Claude Code:**

```bash
claude mcp add --transport http carejobs https://carejobs.now/api/mcp
```

**Cursor, VS Code and other clients that take a URL** (`mcp.json`):

```json
{
  "mcpServers": {
    "carejobs": { "url": "https://carejobs.now/api/mcp" }
  }
}
```

**Clients that only run local (stdio) servers** can bridge to it with [mcp-remote](https://www.npmjs.com/package/mcp-remote):

```json
{
  "mcpServers": {
    "carejobs": { "command": "npx", "args": ["-y", "mcp-remote", "https://carejobs.now/api/mcp"] }
  }
}
```

## Example prompts

- "Find night-shift ICU nurse jobs in Boston with posted pay."
- "What do CNA jobs pay in Texas?"
- "Which hospitals are hiring respiratory therapists in Ohio?"

## Data

The same figures are free as JSON and CSV, no key needed: [`/roles.json`](https://carejobs.now/roles.json) (open jobs by kind of job and employer), [`/pay.json`](https://carejobs.now/pay.json) (posted hourly pay by kind of job) and [`/pay.csv`](https://carejobs.now/pay.csv). A dated open dataset is on Zenodo: [10.5281/zenodo.23395728](https://doi.org/10.5281/zenodo.23395728) (CC BY 4.0). An [llms.txt](https://carejobs.now/llms.txt) describes the site for AI assistants.

## About

CareJobs.Now is a free job board for everyone who works in US healthcare. The server is hosted by CareJobs.Now; this repository holds its documentation and its [`server.json`](server.json) for the MCP Registry. Questions: hello@carejobs.now.
