# Untap

Untap checks UK refunds and compensation from delayed trains, disrupted flights, TfL journey charges and parking notices. Public checks return the applicable rules, amount, deadline and claim guidance. Sign in to save claims, track progress and check saved train commutes for dates you request. You submit claims directly to the operator or airline. Untap never files a claim for you.

This Cursor plugin connects your assistant to Untap's MCP server at `https://untap.money/api/mcp` and adds skills that tell it when and how to use Untap. Version 1.3.3.

## Use it

Install the plugin from the Cursor Marketplace in Cursor or Grok Bot, then sign in to Untap when a tool asks.

Then ask about a journey that went wrong. For example:

- "My train was over 30 minutes late last week. Am I owed Delay Repay?"
- "Did TfL overcharge me? Here is my contactless journey history."
- "My flight was cancelled. What compensation can I claim?"
- "What are Southern Delay Repay amounts and deadlines?"
- "What am I owed so far, and which claims are closest to their deadline?" (needs sign-in)

The check tools work straight away, without an account. Your assistant asks you to sign in to Untap only when you want to save claims, track their progress or check a saved commute.

## Skills

- **uk-travel-claims**: Checks UK travel compensation and refunds with Untap: Delay Repay for late or cancelled trains, UK261 or EU261 flight delays, cancellations, denied boarding, TfL incomplete journeys, maximum fares.
- **find-travel-refunds-in-inbox**: Searches an inbox for UK train, flight and TfL refunds the person may be owed, then checks them with Untap. Use for find refunds, money I'm owed, check my emails for compensation, travel refunds.

## Data

When your assistant calls an Untap tool, Untap receives the inputs the assistant sends to that tool. It does not receive your conversation or other chats.

- Check tools work without signing in. They do not save your booking or result to an account. To verify a journey, Untap sends the stations, airports, flight number and date to National Rail or its flight-data provider. Technical usage records (tool name, outcome, duration) are kept; anonymous records contain no tool inputs.
- If you sign in and ask your assistant to save a claim, journey or commute, Untap stores those details in your account until you delete them. A saved commute is checked only when you ask.
- Revoke an assistant at [untap.money/settings/connections](https://untap.money/settings/connections). Delete your data at [untap.money/data](https://untap.money/data) or with the two-step delete tool.

Full details: [privacy policy](https://untap.money/privacy).

## Support

Documentation: [untap.money/connect/docs](https://untap.money/connect/docs). Questions: contact@untap.money.

## Licence

The MIT licence covers the files in this package: the manifests, the MCP configuration and the skills, which you are welcome to copy and share. It does not cover the Untap service at untap.money, which is used under its [terms](https://untap.money/terms).
