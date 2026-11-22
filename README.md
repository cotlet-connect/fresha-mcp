# Fresha API integration and MCP server: connect Fresha to ChatGPT, Claude and any AI agent

Fresha API integration and MCP server, unofficial, by Cotlet. Your AI works in your own signed-in Fresha account: the calendar, appointments, clients, client notes, sales, team pay reports and services, on the same screens your login opens. Cotlet has 17 ready Fresha tools for AI agents, and the Cloud Browser does the rest. No developer and no Fresha API key needed. Cotlet is independent and is not affiliated with Fresha.

**Does Fresha have an API or an MCP server?** Fresha has no public API, no developer portal and no webhooks for businesses (checked 22 Nov 2026). Its paid Data connector add-on copies data to analytics tools. Fresha's ChatGPT and Claude apps and its public MCP server, launched in August 2026, are for clients who search and book, not for running your business. Fresha has no Zapier app; it syncs with Xero and QuickBooks.

## What salon, barbershop and spa owners ask their AI to do in Fresha

| Job | Ask your AI | Make it repeat |
|---|---|---|
| Tomorrow's bookings | "Who is booked tomorrow, per team member, and where are the gaps?" | Every evening |
| Morning summary | "Summarize new bookings, cancellations and no-shows since yesterday." | Every morning |
| Lapsed clients | "Find clients who have not booked for 90 days and draft a win-back message for each. Send nothing yet." | Weekly |
| Fill a cancelled slot | "Tomorrow's 11:00 cancelled. List waitlist clients who could take it and draft a message to the first one." | When a slot opens |
| Client notes | "Add these notes from today's appointments to each client's profile. Show me before you save." | After each day |
| Marketplace fee check | "List this month's new clients charged the marketplace fee, with how they booked, so I can check the charges." | Monthly |
| Team pay | "Run the Pay Summary report for last week and total hours, services and tips per team member." | Every week |
| Accounting export | "Download this month's sales and payments summary for my accountant." | Monthly |
| Sales and clients to a spreadsheet | "Export this month's appointments, sales and new clients to a spreadsheet." | Daily or monthly |
| Bulk price change | "Raise all colour services by 5% and show me the new prices before you save." | When prices change |
| Import from an old system | "Import the clients in this CSV from my old booking system." | Once |
| Leaving Fresha | "Download my clients, appointments and sales before I move." | Once |

Your AI asks you before it sends, books, cancels or changes anything. Payments and refunds stay in your hands: Cotlet refuses payments.

## Your own Fresha API, built with Cotlet

Fresha gives businesses no public API. With Cotlet you build your own: your AI does the job once in your Cloud Browser, you save it as an endpoint, and you call it from Google Sheets, Power BI, GoHighLevel, Klaviyo, Mailchimp, n8n, Make, Zapier, your own code.

Examples you can build in a few minutes (none of them exists until you build it):

| Endpoint you build | What it returns or does |
|---|---|
| `bookings-for-day` | appointments for a date, with client, service, team member and time |
| `new-bookings` | bookings, cancellations and no-shows since a date |
| `lapsed-clients` | clients with no booking for a number of days |
| `open-slots` | free slots per team member for a date |
| `sales-summary` | sales, payments and tips for a period |
| `team-pay-summary` | hours, services and tips per team member for a period |
| `clients-export` | clients with contact details, first visit and last visit |
| `new-clients-source` | new clients in a period with how they booked |
| `add-client-note` | adds a note to a client's profile (writes only after you allow it) |
| `book-appointment` | books an appointment for a client and service (writes only after you allow it) |

Call it with your Cotlet API key, JSON in and JSON out:

```bash
curl -X POST https://cotlet.dev/api/v1/custom/bookings-for-day \
  -H "Authorization: Bearer $COTLET_API_KEY" -H "Content-Type: application/json" -d '{}'
```

Limits: one call runs up to 90 seconds, writes wait for your consent, payments are blocked. Start here: https://cotlet.dev/app/custom-api/new?app=fresha

## Connect in 2 minutes

Sign up at https://cotlet.dev, sign in to Fresha once in your Cloud Browser, then add Cotlet to your AI.

### Claude

Settings → Connectors → Add custom connector, paste `https://cotlet.dev/mcp/v1` and sign in with Cotlet.dev.

### ChatGPT

Open Plugins in ChatGPT, choose Create as a plugin, paste `https://cotlet.dev/mcp/v1` and sign in with Cotlet.dev. No API key needed.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Fresha tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"fresha":{"command":"uvx","args":["fresha-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t fresha-mcp .
docker run -i --rm -e COTLET_API_KEY fresha-mcp
```

Tools: `fresha_guide`, `fresha_status`, `fresha_open`, `fresha_read`, `fresha_click`, `fresha_type`, `fresha_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install fresha-mcp        # or run it once: uvx fresha-mcp connect
fresha-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 fresha_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 fresha_agent.py status    # is Fresha ready in your Cotlet.dev account
python3 fresha_agent.py guide     # Fresha screens and sign-in link
python3 fresha_agent.py read      # open Fresha, read the page, close the browser
python3 fresha_agent.py tools     # list Cotlet.dev tools
python3 fresha_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Fresha business owners
**Can ChatGPT or Claude read my Fresha calendar?**

Fresha's own ChatGPT and Claude apps are for clients who book. With Cotlet, ChatGPT and Claude work in your own business account: they read your calendar, clients and sales, and tell you who is booked tomorrow.

**Does Fresha work with Zapier or Make?**

Fresha has no Zapier app and no public API. With Cotlet you build your own Fresha endpoints, such as `new-bookings` or `clients-export`, and call them from Zapier, Make or n8n.

**How do I connect Fresha to GoHighLevel?**

Call your `new-bookings` endpoint from a GoHighLevel or n8n workflow on a schedule, so new bookings, cancellations and completed appointments update your contacts.

**How do I get Fresha sales and client data into Google Sheets or Power BI every day?**

Build `sales-summary` and `clients-export` endpoints once, then load them into Google Sheets or Power BI on a schedule.

**How do I connect Fresha to Klaviyo or Mailchimp?**

A `clients-export` or `new-bookings` endpoint feeds Klaviyo or Mailchimp, so clients who booked get your emails without a manual export.

**Can AI fill a cancelled slot from my waitlist?**

Your AI lists who could take the slot and drafts the message. It books only after you say yes.

**Can AI check which clients I paid the marketplace fee for?**

It lists the new clients charged the fee in a period, with how they booked, so you can check each charge with Fresha.

**How do I export all my Fresha data every month as a backup?**

Your AI downloads every report and list your login can export: clients, appointments and sales. A `clients-export` endpoint can run it on a schedule.

**I'm leaving Fresha. How do I take my clients with me?**

Your AI exports your client list, appointments and sales your login can see, as spreadsheets for your new system.

**Is Cotlet affiliated with Fresha?**

No. Cotlet is independent and not affiliated with Fresha.

## Find it on

- [Fresha MCP server on Cotlet.dev](https://cotlet.dev/integrations/fresha-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=fresha&utm_content=find)
- [Fresha API with Cotlet](https://cotlet.dev/integrations/api/fresha?utm_source=github&utm_medium=readme&utm_campaign=fresha&utm_content=find)
- [Does Fresha have an API or MCP server?](https://cotlet.dev/api-status/fresha?utm_source=github&utm_medium=readme&utm_campaign=fresha&utm_content=find)
- [PyPI package fresha-mcp](https://pypi.org/project/fresha-mcp/)

## More salon, spa and booking apps on Cotlet

- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [Zenoti MCP](https://github.com/cotlet-connect/zenoti-mcp)
- [DaySmart MCP](https://github.com/cotlet-connect/daysmart-mcp)
- [Acuity Scheduling MCP](https://github.com/cotlet-connect/acuity-scheduling-mcp)
- [StyleSeat MCP](https://github.com/cotlet-connect/styleseat-mcp)
- [Salonized MCP](https://github.com/cotlet-connect/salonized-mcp)
