# Untap MCP server

Connect [Untap](https://untap.money) to your AI assistant. Untap is a UK
consumer fintech that detects refunds you are already owed: train Delay
Repay, UK261/EU261 flight compensation, TfL contactless overcharges,
and parking-ticket appeal grounds.

This repo holds the directory metadata for the Untap MCP server. The
server itself is hosted at:

```
https://untap.money/api/mcp
```

## Install

See [untap.money/connect](https://untap.money/connect) for one-click
install instructions for Claude (web and desktop), ChatGPT, and other
MCP-compatible clients.

In short:

- **Claude:** open
  [the add-connector dialog](https://claude.ai/settings/connectors?modal=add-custom-connector),
  paste the URL above, complete the Google sign-in.
- **ChatGPT:** Settings → Connectors → enable Developer Mode → add a
  custom MCP connector with the URL above.

## Authentication

OAuth 2.1 with Dynamic Client Registration. End-users sign in with the
Google account they use on Untap. No API keys to copy or manage.

## Tools

Six tools, scoped to the four recurring UK refund categories:

| Tool | What it does |
|---|---|
| `add_train_journey` | Add a UK train booking. Untap auto-checks National Rail HSP records and returns the Delay Repay verdict. |
| `add_flight` | Add a flight. Untap auto-checks AeroDataBox and returns the UK261/EU261 verdict. |
| `add_tfl_journeys` | Add a batch of TfL contactless journeys. Untap detects max-fare overcharges, incomplete journeys, and missed Hopper fares. |
| `add_parking_fine` | Add a UK PCN. Untap runs the appeal-grounds engine and suggests the strongest grounds. |
| `list_savings` | Read claimable / pending / historic refund opportunities. |
| `delete_my_data` | Two-step destructive tool to wipe every booking and statement from the user's account. |

Untap never files claims itself. Every claimable verdict carries a
`claim_url` deeplink to the operator's site for the user to confirm and
submit.

## Privacy

The MCP server cannot see passwords, payment details, or bank
information. Per-tool rate limits, per-user audit log, and
per-(user, client) revoke from
[untap.money/settings/connections](https://untap.money/settings/connections).

## Source

The MCP server source is in the main Untap repository (private). This
repo is the public directory metadata only.

## Licence

MIT — see [`LICENSE`](./LICENSE).
