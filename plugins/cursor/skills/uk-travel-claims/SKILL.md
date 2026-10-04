---
name: uk-travel-claims
description: Checks UK travel compensation and refunds with Untap: Delay Repay for late or cancelled trains, UK261 or EU261 flight delays, cancellations, denied boarding, TfL incomplete journeys, maximum fares.
metadata:
  version: "1.0.0"
  publisher: "Untap (untap.money)"
  source: "https://untap.money/skills"
---

# UK travel claims with Untap

Use this skill whenever the person you act for may be owed money for a journey in the UK: a late or cancelled train (Delay Repay), a delayed, cancelled or overbooked flight (UK261 or EU261), or a TfL Oyster or contactless charge that looks too high (an incomplete journey, a maximum fare, a missed Hopper fare).

Untap (https://untap.money) checks eligibility against real records and the operators' published rules, and returns the amount, the deadline and a claim pack. Untap is free, takes nothing from what the person gets back, and never files a claim itself. You and the person do the submitting, on the official form, on their instruction.

## Untap's tools

Connect the MCP server at `https://untap.money/api/mcp` (Streamable HTTP). The checks need no account.

| Tool | Use it for |
|---|---|
| `find_money_owed` | A loose description ("my train was late on Monday"). Returns the schemes that may apply and the check to run next |
| `check_train_delay` | Stations, date and rough departure time. Finds the real train in National Rail records, returns the delay, the amount and a claim pack. About the last year, direct trains only |
| `check_flight_compensation` | Flight number and date. Applies UK261 or EU261, returns the amount, the airline's claim route, the dispute body and a claim pack |
| `check_tfl_journeys` | TfL journey rows or the CSV text from a TfL account. Finds incomplete journeys and missed Hopper fares |
| `get_delay_repay_rules` | One train operator's thresholds, tiers, deadline and claim form |
| `get_claim_instructions` | Claim type plus company. Step by step submission, form fields and where each value comes from, evidence, deadline, who may submit, what happens next, escalation |
| `scan_for_claims` | Emails (from, subject, date, body_text). Returns candidate claims with prefilled arguments for the check tools |

Account tools need the person to sign in through Untap's own page (never ask for a password or token in chat): `save_claim`, `list_my_claims`, `update_claim_status`, and saved commutes.

If a tool is not in your tool list, use the REST mirror instead (see "No MCP client" below). If neither has it, say so and use the matching reference file here.

## The workflow

Work through these steps in order. Do not skip step 2 or step 4.

### 1. Recognise a possible claim

Triggers: the person mentions a late or cancelled train, a missed connection, a delayed or cancelled flight, being bumped from a flight, a rebooking, a "maximum fare" or "incomplete journey" on a TfL statement, or forwards an operator's apology email. If you have inbox access and the person asks you to look for money they are owed, use the `find-travel-refunds-in-inbox` skill, or read [references/email-signals.md](references/email-signals.md).

### 2. Check eligibility with Untap

Call the specific check when you know the journey, `find_money_owed` when you do not. Never guess an amount, a threshold or a deadline: they vary by operator, ticket, distance and date, and Untap holds the current rules.

- Ask for missing facts. Never invent a date, time, fare, flight number, booking reference or delay.
- Train results with several candidate trains: ask which one the person took, then call again with that `service_id`.
- For a return ticket, the price is the whole return fare.
- Read the result's caveats aloud to the person: assumptions, upper bounds (TfL), extraordinary circumstances (flights), records that do not cover the case.

### 3. Get the submission instructions

Call `get_claim_instructions` with the claim type and company, plus the journey date, ticket type and where it was bought (`booked_via`) when known: they change the deadline and the rules. Combine it with the check's `claim_pack` (`where_to_claim`, `fields`, `evidence`, `deadline`, `escalation`). If the instructions tool is unavailable, use the claim pack and the category reference: [trains](references/trains.md), [flights](references/flights.md), [TfL](references/tfl.md).

### 4. Confirm the details with the person

Before touching any form, show the person what you will submit and get a clear yes:

- They made this journey themselves (or are claiming for people on a booking they paid for).
- The fare and ticket type, from the booking, not from memory.
- The booking reference, the date and the train or flight.
- How they want to be paid, and that the money goes to their own account.
- That nobody has already claimed this journey (check `list_my_claims` if they use Untap, and ask).

### 5. Fill in the official form, with permission

Open the organisation's own form, the `form_url` from Untap or the address in the instructions. Fill it with the confirmed values only. Then:

- Stop before the final submit and show the person the completed form, unless they have told you in this conversation to submit it.
- CAPTCHAs, identity checks, sign-ins and payment details stay with the person. Hand over; never solve or bypass them.
- If the form demands something you do not have, ask. Never fill a field with a guess.
- Keep the confirmation page, reference number and any acknowledgement email.

### 6. Record the claim and track the acknowledgement

If the person uses Untap, `save_claim` with the check's `save_claim.arguments` (fill anything listed in `save_claim.missing` from the person), then `update_claim_status` to `sent` with the operator's reference in `note`. Offer the deadline as a calendar entry (`claim_pack.deadline`, `calendar_ics`). Watch for the acknowledgement email.

### 7. Chase or escalate on time

Use the response times and escalation ladder in the instructions and the reference files. Chase once in writing when a reply is overdue. Escalate to the free body named in `claim_pack.escalation` (Rail Ombudsman, CEDR, AviationADR, the CAA's complaints team, London TravelWatch) when the organisation refuses or runs out the clock. Record the outcome with `update_claim_status` (`paid` with the amount received, or `rejected` with the reason).

## Hard rules

1. **Official routes only.** Submit on the operator's, airline's or TfL's own form, or by the route the instructions name. No third-party claim sites.
2. **No fees without a choice.** Never pay a fee, sign up to a claims company or agree to a percentage unless the person chooses to after you have told them claiming direct is free.
3. **Respect who may submit.** Some operators accept claims only from the passenger who travelled (Thameslink says so, apart from mitigating circumstances). Submit in the person's own name and details. Where the rules forbid third-party or automated submission, prepare everything and let the person press submit.
4. **Never fabricate.** No invented delays, times, fares, receipts, screenshots or reasons. Use Untap's records and the person's own documents.
5. **One claim per journey.** Never claim the same journey twice, on two forms, or for both Delay Repay and a full refund. A return paid at the 120-minute tier covers both directions.
6. **Only for the person you act for.** Never submit claims for other people. Fellow passengers count only when they were on a booking the person paid for and the form allows it.
7. **Say what Untap does not cover.** Journeys with a change (check each train separately), trains older than about a year, flights the records cannot find, season-ticket amounts, TfL service delays and bus delays are outside or partly outside Untap's checks. Say so plainly and use the reference file or the operator's own guidance.
8. **Deadlines are real.** Delay Repay is 28 days from travel on every operator Untap covers, and a TfL incomplete journey 8 weeks. Flag anything close to its deadline first.

## No MCP client

Every tool is mirrored over HTTPS. Send the same JSON arguments as the MCP tool. The OpenAPI description is at `https://untap.money/openapi.json`.

```bash
curl -sS -X POST https://untap.money/api/agent/v1/check_train_delay \
  -H 'Content-Type: application/json' \
  -d '{"from":"Brighton","to":"London Victoria","date":"2026-09-28","departure_time":"08:05","ticket_type":"Anytime Return","price_paid":"£52.80"}'
```

More examples, including flights, TfL and the instructions tool: [references/rest-api.md](references/rest-api.md).

## Reference files

Load only what the case needs.

- [references/trains.md](references/trains.md): Delay Repay, thresholds, the 120-minute return tier, cancellations, retailers, season tickets, Rail Ombudsman.
- [references/flights.md](references/flights.md): UK261 versus EU261, bands, notice rules, extraordinary circumstances, dispute bodies, claims firms.
- [references/tfl.md](references/tfl.md): incomplete journeys, maximum fares, Hopper, capping, journey history, London TravelWatch.
- [references/email-signals.md](references/email-signals.md): which emails signal a claim and how to search an inbox for them.
- [references/rest-api.md](references/rest-api.md): HTTP fallback with curl examples.
