# SerialHunt for Claude and other MCP clients

![SerialHunt](assets/icon.svg)

Ask an AI assistant whether a US bill is worth keeping and get an answer from government production figures instead of memory: the star note print run a serial came from and how many notes shared it, every fancy pattern in the digits with its exact odds, and the rarest star runs to watch for.

This repository holds:

- the connection details for the **SerialHunt remote MCP server** at `https://bigballi.com/SerialHunt/mcp`,
- a **Claude plugin** that adds that server plus a `paper-money-serials` skill, which teaches Claude how to read the numbers.

The server is run by [SerialHunt](https://bigballi.com/SerialHunt/lookup). Its star note figures come from the Bureau of Engraving and Printing's production reports, through the [uspapermoney.info](https://www.uspapermoney.info/) archive for Series 1963 to 2017A, and it updates weekly. The same answers are on the [web lookup](https://bigballi.com/SerialHunt/lookup).

## What you can ask

- "I got a $1 bill with serial A 032 12345 ★, Series 2017A. Is it rare?"
- "Is MB 123 45678 C on a $20 a fancy serial number?"
- "Which $2 star notes had the smallest print runs?"
- "What is a radar serial number, and how rare is it?"

## Tools

All tools are read-only (`readOnlyHint: true`) and need no account.

| Tool | What it answers |
|---|---|
| `check_serial` | One note from its serial: the Federal Reserve Bank, the series (worked out from the serial when it can be), every collector pattern in the digits with its odds, and for a star note the print run it came from, the notes printed and the rarity band. |
| `find_star_runs` | The 10 smallest star runs on record, optionally for one denomination, series or Federal Reserve Bank. |
| `list_serial_patterns` | The 17 fancy serial patterns, each strictly defined, with how many of the 100,000,000 possible serials match. |
| `get_coverage` | Which denominations and series the figures cover, the last update and any known gap. |

SerialHunt gives no prices and makes no authenticity claims, on purpose.

## Setup

### Claude (claude.ai, Desktop, mobile)

Settings → Connectors → Add custom connector, then paste `https://bigballi.com/SerialHunt/mcp`. No sign-in is needed.

### Claude Code

Install the plugin, which adds the server and the `paper-money-serials` skill:

```
/plugin marketplace add BigBalli/serialhunt-mcp
/plugin install serialhunt@serialhunt
```

Or add only the server:

```
claude mcp add --transport http serialhunt https://bigballi.com/SerialHunt/mcp
```

### Other MCP clients

Any client that supports remote MCP servers over Streamable HTTP can use `https://bigballi.com/SerialHunt/mcp` with no credentials. The server speaks protocol versions 2026-07-28, 2025-11-25, 2025-06-18 and 2025-03-26 and answers with JSON (no SSE, no sessions).

## Privacy

The server receives the tool name and its arguments (for example a serial number and a denomination), uses them to answer, and does not store them. It never sees your conversation or your account. Full policy: [bigballi.com/SerialHunt/privacy](https://bigballi.com/SerialHunt/privacy).

## Support

Email g@bigballi.com, or see [bigballi.com/SerialHunt/connect](https://bigballi.com/SerialHunt/connect).

## License

The contents of this repository are released under the MIT License. The production figures served by the SerialHunt MCP server are not part of this repository.
