# Jet Cab AMS MCP server

Book Amsterdam chauffeur rides with an AI assistant: fixed-price Schiphol transfers, custom rides and private tours (Mercedes E-Class, S-Class, V-Class).

Official remote [Model Context Protocol](https://modelcontextprotocol.io) server of **Jet Cab AMS** (https://www.jetcabams.nl/).

| | |
|---|---|
| Endpoint | `https://www.jetcabams.nl/mcp` |
| Transport | Streamable HTTP (MCP 2026-07-28 and 2025-03-26 to 2025-11-25) |
| Authentication | none |
| Official MCP Registry | `nl.jetcabams.www/booking` |

## Tools

- **list_services** (read-only): fixed-price Schiphol routes, private tours and cars with passenger and luggage limits and prices.
- **get_quote** (read-only): exact price and rule check for one ride; returns a signed `quoteToken` valid for 15 minutes. No booking, no email, no payment.
- **request_booking**: sends the quoted ride as a booking request with the customer's name, email and phone, only after the customer approved the price and accepted the Terms. The customer confirms the request through a link emailed to them before the business sees it. Nothing is charged through MCP.

## Connect

- **Claude**: add a custom connector with the endpoint URL (no authentication).
- **ChatGPT** (Developer mode): add a connector with the endpoint URL, authentication none.
- **Cursor / VS Code / any MCP client**:

```json
{ "mcpServers": { "jetcabams": { "url": "https://www.jetcabams.nl/mcp" } } }
```

## Links

- Website and booking form: https://www.jetcabams.nl/
- Agent docs: https://www.jetcabams.nl/llms.txt
- API (OpenAPI): https://www.jetcabams.nl/openapi.json
- Terms: https://www.jetcabams.nl/terms.html · Privacy: https://www.jetcabams.nl/privacy.html
- Demo: https://www.jetcabams.nl/media/mcp-demo.mp4

The server itself runs on the business's website; this repository holds its public documentation and listing metadata.
