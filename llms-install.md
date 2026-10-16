# Installing the CareJobs.Now Healthcare Jobs MCP server

This is a hosted (remote) MCP server. There is nothing to download, build or run locally, and it needs no API key.

- Endpoint: `https://carejobs.now/api/mcp`
- Transport: Streamable HTTP
- Authentication: none (public, read-only, free)

## Cline

Add this to `cline_mcp_settings.json` and save:

```json
{
  "mcpServers": {
    "carejobs": {
      "type": "streamableHttp",
      "url": "https://carejobs.now/api/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

## Check it works

Ask: "Find night shift ICU nurse jobs in Texas with posted pay." Cline should call `search_healthcare_jobs` and return jobs with links to each employer's application.

The six tools are listed in [README.md](README.md#tools).
