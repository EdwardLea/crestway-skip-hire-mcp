# Crestway Skip Hire MCP server

UK skip hire prices, sizes and local permit rules for AI assistants.

A free, read-only [MCP](https://modelcontextprotocol.io) server from
[Crestway Skip Hire](https://www.crestwayskiphire.co.uk). Connect it to Claude,
ChatGPT, Cursor, VS Code or any MCP client, and ask things like "How much is a
skip in Swindon?" or "Do I need a permit for a skip on the road in Chippenham?".

**Server URL:** `https://www.crestwayskiphire.co.uk/mcp`
(Streamable HTTP, no sign-up or API key)

## Tools

| Tool              | Input                                | Returns                                                                                                                                                         |
| ----------------- | ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `skip_prices`     | `postcode`, full or district (`SN1`) | Guide price for each skip size, 2 yard mini to 12 yard maxi, ex VAT, and the town page covering the postcode                                                     |
| `skip_sizes`      | none                                 | Each size's typical dimensions, bin bag count, typical jobs, placement and heavy waste rules                                                                     |
| `town_skip_facts` | `town`, name or slug                 | The council's skip permit (fee, lead time, how to apply), nearest recycling centres, council bulky and garden waste, fly-tipping fines and figures, common questions |
| `how_to_book`     | `postcode`, `size`, both optional    | The number to call and hours, the next-day cut-off, what to have ready for the call, and with a postcode and size the guide price and council road permit fee |
| `find_town`       | `query`, name or postcode district   | Up to 5 towns with a Crestway page, with county and page URL                                                                                                     |

Every answer includes the Crestway page it came from and the phone number.
Prices are guide prices, ex VAT, and match the website. Town facts come from
council websites and official datasets, each with its source and the month it
was checked. Coverage is England.

## Setup

### Claude

Settings › Connectors › Add custom connector, then paste the server URL.

### Claude Code

```sh
claude mcp add --transport http crestway https://www.crestwayskiphire.co.uk/mcp
```

### ChatGPT

Settings › Apps and Connectors › Advanced › turn on developer mode, then
create a connector with the server URL and no authentication.

### Cursor

`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "crestway": { "url": "https://www.crestwayskiphire.co.uk/mcp" }
  }
}
```

### VS Code

`.vscode/mcp.json`:

```json
{
  "servers": {
    "crestway": { "type": "http", "url": "https://www.crestwayskiphire.co.uk/mcp" }
  }
}
```

### stdio-only clients

```json
{
  "mcpServers": {
    "crestway": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://www.crestwayskiphire.co.uk/mcp"]
    }
  }
}
```

## Privacy

No bookings, accounts or personal details. We log which tool was called and
the postcode district asked about, never IP addresses.

## More

- About the server: https://www.crestwayskiphire.co.uk/mcp-server
- Questions or corrections: hello@crestwayskiphire.co.uk

This repository holds the listing and setup instructions. The server runs at
the URL above.
