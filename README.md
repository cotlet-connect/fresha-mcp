# How to connect Fresha to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Fresha account.** Fresha's official ChatGPT and Claude apps help customers find and book appointments, not run your business. Cotlet.dev connects your own signed-in Fresha account to any AI agent, so the AI books, reschedules and looks up clients for you.

## What you can ask

> Book Maria Lopez for a gel manicure with Chloe on Thursday at 11 am.

> Move all of Tom's Monday appointments to Wednesday at the same times.

> How busy are we next week? Show which team member has the most free slots.

> Which clients haven't visited in 60 days? List them with their last service and phone number.

> Add a note to Priya Shah's client profile: allergic to latex, prefers afternoon slots.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

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

## Questions from Fresha users

**Does Fresha have an API or data connector?**

You don't need one. Cotlet.dev works in your own signed-in Fresha account, so your AI agent can read and change appointments and client records without a Fresha API key.

**How do I connect Fresha to ChatGPT?**

Fresha's own ChatGPT app is for customers finding appointments. To manage your business, add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Fresha once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Fresha API key.

**Is there a way to use Claude with Fresha?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Fresha account, not just the customer booking connector.

**Is there a Fresha MCP server?**

Fresha's official ChatGPT and Claude integrations are customer-facing: they show availability, prices and venues, then send people to Fresha to book. Cotlet.dev is a hosted MCP server that works in your Fresha business account for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Fresha on Cotlet.dev](https://cotlet.dev/integrations/fresha-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=fresha&utm_content=find)
- [PyPI package fresha-mcp](https://pypi.org/project/fresha-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-fresha-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/fresha-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=fresha

Start free: https://cotlet.dev/signup?app=fresha&utm_source=github&utm_medium=readme&utm_campaign=fresha
