# Untap for AI assistants

Check whether you are owed money for a delayed train, a disrupted flight, a TfL overcharge or a UK parking ticket, and get the operator's own claim link.

Untap checks UK refunds and compensation from delayed trains, disrupted flights, TfL journey charges and parking notices. Public checks return the applicable rules, amount, deadline and claim guidance. Sign in to save claims, track progress and check saved train commutes for dates you request. You submit claims directly to the operator or airline. Untap never files a claim for you.

Every package here is a thin wrapper around the same hosted MCP server, plus Untap's skills:

```
https://untap.money/api/mcp
```

Tools live on the server, so they update in every assistant without a new package. Version 1.3.0.

## Install

**Claude Code**

```
/plugin marketplace add aneduaim/untap-mcp
/plugin install untap@untap
```

**Claude (web, desktop and Cowork):** go to Customize, Plugins, Add, Add marketplace and paste `https://github.com/aneduaim/untap-mcp`. Install Untap, then connect it from the plugin's **Connectors** tab. You can also add `https://untap.money/api/mcp` as a custom connector.

**ChatGPT and Codex:** `plugins/agent-plugins` is an Agent Plugins 1.0.0 package, and `.agents/plugins/marketplace.json` lists it as a repo marketplace. In ChatGPT developer mode you can also add `https://untap.money/api/mcp` as a connector.

**Cursor and Grok Bot:** `plugins/cursor` is the Cursor plugin package, listed in `.cursor-plugin/marketplace.json`. You can also add `https://untap.money/api/mcp` in Cursor's MCP settings.

**Gemini CLI:** this repository is a Gemini CLI extension (`gemini-extension.json` and `GEMINI.md` at the root).

```
gemini extensions install https://github.com/aneduaim/untap-mcp
```

Account tools sign in with `/mcp auth untap`.

**Any other MCP client:** connect to `https://untap.money/api/mcp` over Streamable HTTP. Account tools sign you in through OAuth 2.1 with dynamic client registration; there are no API keys.

Setup guides for each assistant: [untap.money/connect](https://untap.money/connect).

## What is in this repository

| Path | Format | Read by |
|---|---|---|
| `plugins/claude/` | Claude plugin (`.claude-plugin/plugin.json`, `.mcp.json`) | claude.ai, Claude Desktop, Cowork, Claude Code |
| `plugins/cursor/` | Cursor plugin (`.cursor-plugin/plugin.json`, `mcp.json`) | Cursor, Grok Bot |
| `plugins/agent-plugins/` | Agent Plugins 1.0.0 (`plugin.json`, `mcp.json`) | ChatGPT, Codex and other Agent Plugins hosts |
| `.claude-plugin/marketplace.json` | Claude Code marketplace | Claude Code, claude.ai |
| `.cursor-plugin/marketplace.json` | Cursor marketplace | Cursor |
| `.agents/plugins/marketplace.json` | Agent Plugins repo marketplace | Codex, ChatGPT desktop |
| `gemini-extension.json`, `GEMINI.md` | Gemini CLI extension manifest and context file | Gemini CLI, geminicli.com/extensions |
| `server.json` | Official MCP Registry entry | registry.modelcontextprotocol.io |
| `smithery.yaml` | Smithery listing | smithery.ai |

These files are generated from one source in Untap's main repository. Please open an issue rather than a pull request against a package.

## Tools

| Tool | What it does | Sign-in |
|---|---|---|
| `find_money_owed` | Find money you may be owed | No |
| `check_train_delay` | Check a delayed train for Delay Repay | No |
| `check_flight_compensation` | Check a flight for UK261 or EU261 compensation | No |
| `check_tfl_journeys` | Check TfL journeys for overcharges | No |
| `get_delay_repay_rules` | Delay Repay rules for a train operator | No |
| `get_claim_instructions` | How to submit a train, flight or TfL claim | No |
| `scan_for_claims` | Scan emails for train, flight and TfL claims | No |
| `save_commute` | Save a usual train journey | Yes |
| `list_commutes` | List saved commutes | Yes |
| `check_commute` | Check a saved commute for a travel date | Yes |
| `stop_commute` | Stop a saved commute | Yes |
| `save_claim` | Save a checked claim to your Untap account | Yes |
| `list_my_claims` | List my claims | Yes |
| `update_claim_status` | Update a claim’s status | Yes |
| `add_train_journey` | Add a train booking | Yes |
| `add_flight` | Add a flight | Yes |
| `add_tfl_journeys` | Add TfL journeys from a contactless statement | Yes |
| `add_parking_fine` | Add a parking ticket (PCN) | Yes |
| `list_savings` | List the person’s refund opportunities | Yes |
| `delete_my_data` | Delete all my Untap data | Yes |

This table was generated from the server's source for version 1.3.0. The live list is always the server's own `tools/list` at `https://untap.money/api/mcp`. 7 of 20 tools work without signing in.

## Skills

- **uk-travel-claims**: Checks UK travel compensation and refunds with Untap: Delay Repay for late or cancelled trains, UK261 or EU261 flight delays, cancellations, denied boarding, TfL incomplete journeys, maximum fares.
- **find-travel-refunds-in-inbox**: Searches an inbox for UK train, flight and TfL refunds the person may be owed, then checks them with Untap. Use for find refunds, money I'm owed, check my emails for compensation, travel refunds.

The same skills can be downloaded on their own at [untap.money/skills](https://untap.money/skills).

## Privacy

When your assistant calls an Untap tool, Untap receives the inputs the assistant sends to that tool. It does not receive your conversation or other chats.

- Check tools work without signing in. They do not save your booking or result to an account. To verify a journey, Untap sends the stations, airports, flight number and date to National Rail or its flight-data provider. Technical usage records (tool name, outcome, duration) are kept; anonymous records contain no tool inputs.
- If you sign in and ask your assistant to save a claim, journey or commute, Untap stores those details in your account until you delete them. A saved commute is checked only when you ask.
- Revoke an assistant at [untap.money/settings/connections](https://untap.money/settings/connections). Delete your data at [untap.money/data](https://untap.money/data) or with the two-step delete tool.

Full details: [privacy policy](https://untap.money/privacy).

## Licence

The MIT licence covers the files in this repository: the manifests, the MCP configuration and the skills, which you are welcome to copy and share. It does not cover the Untap service at untap.money, which is used under its [terms](https://untap.money/terms).
