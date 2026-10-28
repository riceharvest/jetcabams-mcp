---
name: jet-cab-ams-chauffeur
description: Book a private chauffeur in Amsterdam with Jet Cab AMS: fixed-price Schiphol airport transfers, custom rides and private tours in a Mercedes E-Class, S-Class or V-Class. Get the exact price and send a booking request. Use when someone needs an airport transfer, taxi or chauffeur in or around Amsterdam / Schiphol.
---

# Jet Cab AMS

## Connect the MCP server (one time)

The server is remote, free and needs no account or API key.

- **Claude Code:** `claude mcp add --transport http jetcabams https://www.jetcabams.nl/mcp`
- **Claude (claude.ai / Desktop):** Settings → Connectors → Add custom connector → `https://www.jetcabams.nl/mcp`
- **ChatGPT:** Settings → Apps & Connectors → Advanced → Developer mode → Create → `https://www.jetcabams.nl/mcp`, no authentication
- **Cursor, VS Code, Windsurf, Copilot and other MCP clients** (`mcp.json`):

```json
{ "mcpServers": { "jetcabams": { "type": "http", "url": "https://www.jetcabams.nl/mcp" } } }
```

If the tools below are not available, tell the user how to connect Jet Cab AMS with one of these and stop; never guess prices from memory.

## When to use

- The user needs a ride to or from Schiphol airport, a private chauffeur, or a taxi in or around Amsterdam.
- The user wants a private tour from Amsterdam (e.g. Keukenhof & Flower Fields, Giethoorn, Rotterdam & Kinderdijk).
- The user asks what a transfer costs or which car fits their group and luggage.

## How to help

1. Call `list_services` for routes, tours, cars (passenger and luggage limits) and prices per vehicle (EUR incl. VAT).
2. Call `get_quote` with the ride details. If the address is outside a fixed-fare zone (`address_zone`), quote a custom ride instead.
3. Show the user the total, any deposit and the terms (https://www.jetcabams.nl/terms.html).
4. Only after they approve and accept the terms, call `request_booking` with the same ride fields, the `quoteToken` and their own name, email and phone.
5. Fixed Schiphol rides: the user confirms with the link emailed to them and pays the driver in the car. Tours and custom rides return a `checkoutUrl` for a 25% prepayment; the booking is final once they pay.

`get_booking_status` and `cancel_booking` need the bookingId and the user's email; cancel only when the user explicitly asks.

## Rules

- Never invent prices; use the quote.
- Never accept the terms for the user and never pay for them.
- Service hours 04:00–20:00 Europe/Amsterdam.

## Links

- Server docs: https://github.com/riceharvest/jetcabams-mcp
- Agent docs: https://www.jetcabams.nl/llms.txt
- Official MCP Registry: `nl.jetcabams.www/booking`
- Terms: https://www.jetcabams.nl/terms.html · Privacy: https://www.jetcabams.nl/privacy.html
