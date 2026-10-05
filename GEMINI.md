# Untap

Use Untap whenever the person may be owed money for a journey in the UK: a late or cancelled train (Delay Repay), a delayed, cancelled or overbooked flight (UK261 or EU261), or a TfL Oyster or contactless charge that looks too high (an incomplete journey, a maximum fare, a missed Hopper fare).

Untap checks eligibility against real records and the operators' published rules, and returns the amount, the deadline and a claim pack. It is free and takes nothing from what the person gets back.

## Tools

The `untap` MCP server (`https://untap.money/api/mcp`) has 20 tools. These 7 need no sign-in:

- `find_money_owed`: Find money you may be owed
- `check_train_delay`: Check a delayed train for Delay Repay
- `check_flight_compensation`: Check a flight for UK261 or EU261 compensation
- `check_tfl_journeys`: Check TfL journeys for overcharges
- `get_delay_repay_rules`: Delay Repay rules for a train operator
- `get_claim_instructions`: How to submit a train, flight or TfL claim
- `scan_for_claims`: Scan emails for train, flight and TfL claims

The account tools (`save_commute`, `list_commutes`, `check_commute`, `stop_commute`, `save_claim`, `list_my_claims`, `update_claim_status`, `add_train_journey`, `add_flight`, `add_tfl_journeys`, `add_parking_fine`, `list_savings`, `delete_my_data`) work with the person's Untap account: saved claims, commutes and bookings. They need the person to sign in through Untap's own page: run `/mcp auth untap`. Never ask for a password or token in chat.

## Rules

- Never guess an amount, a threshold or a deadline: they vary by operator, ticket, distance and date, and Untap holds the current rules. Ask for missing facts and never invent a date, time, fare, flight number, booking reference or delay.
- Untap never files a claim. The person submits it on the operator's, airline's or TfL's own form, so the money goes straight to them. Show them what will be submitted and get a clear yes first. CAPTCHAs, sign-ins and payment details stay with the person.
- Untap covers trains in Great Britain, TfL, and flights under UK261 and EU261. Journeys with a change (check each train separately), trains older than about a year, season-ticket amounts and bus delays are outside or partly outside its checks. Say so plainly.
- Use British English and pounds sterling.

## More

- Step-by-step skills for the whole claim workflow: https://untap.money/skills
- Documentation: https://untap.money/connect/docs
