# Trains: Delay Repay

Read this when a train in Great Britain was late or cancelled. Always run `check_train_delay` (or `get_delay_repay_rules` for the rules alone) before quoting an amount: the operator, ticket type, fare and the minute the train arrived all change the answer.

## Contents

- How Delay Repay works
- The 15 and 30 minute schemes, by operator
- What each delay pays
- The 120 minute return tier and its exceptions
- Cancellations, abandoned trips and missed connections
- The 28 day deadline
- Tickets from Trainline and other retailers
- Who may submit (GTR's passenger rule)
- Season tickets
- Evidence and the form
- Response, chasing and the Rail Ombudsman
- What Untap does not cover
- Sources

## How Delay Repay works

Delay Repay is each train operator's compensation scheme for late arrival. It pays whatever caused the delay. Only two things go into the amount: how late the person arrived at their destination, and the single fare for the delayed journey. Not how late the train left, and not what the whole booking cost.

There is no central portal. Each operator takes claims on its own site. Untap's check identifies the train that actually ran from National Rail records and names the operator and form to use.

## The 15 and 30 minute schemes, by operator

Untap's table, from the same code that runs the checks (operators' own pages, checked 30 September 2026). "Automatic scheme" describes only specific ticket types bought direct; call `get_delay_repay_rules` for the scope. Anything not listed here is outside Untap's table: say so and use the operator's own page.

| Operator | Pays from | 120 min return tier | Automatic scheme | Claim form |
|---|---|---|---|---|
| Avanti West Coast | 15 min | Yes | Detected, you confirm | https://avantiwestcoast.co.uk/help-and-support/delay-repay |
| c2c | 15 min | Yes | Paid automatically | https://c2c-online.co.uk/help-feedback/delay-repay/ |
| Caledonian Sleeper | 30 min | Yes | Detected, you confirm | https://sleeper.scot/delay-repay-form/ |
| Chiltern Railways | 15 min | Yes | Check when you claim | https://chilternrailways.delayrepaycompensation.com/ |
| CrossCountry | 30 min | Yes | Manual claim only | https://crosscountrytrains.co.uk/help-support/delay-repay |
| East Midlands Railway | 15 min | Yes | Manual claim only | https://www.eastmidlandsrailway.co.uk/delay-repay |
| Gatwick Express | 15 min | Yes | Detected, you confirm | https://www.gatwickexpress.com/help-and-support/delay-repay-compensation |
| Great Northern | 15 min | Yes | Detected, you confirm | https://www.greatnorthernrail.com/help-and-support/delay-repay-compensation |
| Great Western Railway | 15 min | Yes | Detected, you confirm | https://gwr.com/help-and-support/refunds-and-compensation/delay-repay |
| Greater Anglia | 15 min | Yes | Manual claim only | https://greateranglia.co.uk/about-us/our-performance/delay-repay |
| Hull Trains | 30 min | No | Manual claim only | https://delayrepay.hulltrains.co.uk/ |
| LNER | 30 min | Yes | Detected, you confirm | https://lner.co.uk/support/delay-repay/ |
| London Northwestern Railway | 15 min | Yes (unverified) | Detected, you confirm | https://londonnorthwesternrailway.co.uk/about-us/delay-repay |
| Lumo | 30 min | No | Detected, you confirm | https://lumo.co.uk/help/delay-repay |
| Northern Trains | 15 min | Yes | Detected, you confirm | https://delayrepay.northernrailway.co.uk/ |
| ScotRail | 30 min | Yes | Manual claim only | https://scotrail.co.uk/plan-your-journey/our-delay-repay-guarantee |
| South Western Railway | 15 min | Yes | Detected, you confirm | https://southwesternrailway.com/contact-and-help/delay-repay |
| Southeastern | 15 min | Yes | Detected, you confirm | https://delayrepay.southeasternrailway.co.uk/ |
| Southern | 15 min | Yes | Detected, you confirm | https://www.southernrailway.com/help-and-support/delay-repay-compensation |
| Thameslink | 15 min | Yes | Detected, you confirm | https://www.thameslinkrailway.com/help-and-support/delay-repay |
| TransPennine Express | 15 min | Yes | Detected, you confirm | https://delayrepay.tpexpress.co.uk/ |
| Transport for Wales | 15 min | Yes | Detected, you confirm | https://tfw.wales/help-and-contact/rail/delay-repay |
| West Midlands Railway | 15 min | Yes (unverified) | Detected, you confirm | https://westmidlandsrailway.co.uk/about-us/delay-repay |

"Detected, you confirm" means the operator raises a claim for some tickets and emails the person to accept it. Nothing is paid if that email is ignored, so treat it as a claim to finish, not money already on its way. A pre-filled claim and a manual claim for the same journey count as two claims: use one.

"Unverified" means Untap could not read the operator's page and applies the national scheme. Tell the person to check the operator's page when claiming.

## What each delay pays

As a share of the single fare for the delayed journey. On a return ticket the single fare is half the return price.

| Late at destination | 15 minute operators | 30 minute operators |
|---|---|---|
| 15 to 29 minutes | 25% of the single | Nothing |
| 30 to 59 minutes | 50% of the single | 50% of the single |
| 60 to 119 minutes | 100% of the single | 100% of the single |
| 120 minutes or more | The whole fare paid, single or return (see below) | The same, except Lumo and Hull Trains |

Do the arithmetic only to sanity check Untap's figure. Quote Untap's amount and basis (`single_fare` or `return_fare`).

## The 120 minute return tier and its exceptions

On a return ticket, if one direction arrives 120 minutes or more late, the operators that publish this tier refund the whole return fare. It is one claim, and it covers the other direction too: never claim the other direction as well, even if it was also late.

Exceptions in Untap's table:

- **Lumo and Hull Trains** have no 120 minute tier. From 60 minutes they pay half the return, however long the delay.
- **West Midlands Railway and London Northwestern Railway** are unverified; the national tier is applied.
- **Govia Thameslink operators** (Thameslink, Southern, Great Northern, Gatwick Express) allow one 120 minute claim per day, and one per open return.
- **LNER:** two Advance Singles bought as a round trip do not count as a return.
- **Northern:** a season ticket at 120 minutes or more pays one journey, not two.

When Untap applies this tier, its claim pack tells the person to say it was a return and that they arrived two hours or more late. Follow that wording.

## Cancellations, abandoned trips and missed connections

- **Cancelled train:** counts as a delay. The amount follows how much later the person arrived on the next available service. Pass `was_cancelled` or let Untap look it up.
- **Decided not to travel** because the train was delayed or cancelled: the ticket is refundable in full, with no admin fee, from whoever sold it. That is a refund on a separate form, instead of compensation. Never use both forms for one journey.
- **A journey with a change:** Untap's records hold direct trains only. Check each train separately and claim on the arrival time at the final destination as the operator's form asks. Say plainly that Untap checked the trains one at a time.
- **Split tickets:** Untap's guidance is that each ticket is claimed separately from the operator named on it. Confirm with `get_claim_instructions`.

## The 28 day deadline

Every operator in Untap's table publishes 28 days from the date of travel. Untap's claim pack gives the last day as `deadline.date`. A few operators will look at a late claim with a reason, but do not rely on it: past 28 days the claim is a request for a favour.

Caledonian Sleeper's pre-filled claims must be confirmed within 28 days or the money is lost.

## Tickets from Trainline and other retailers

A retailer (Trainline, a split-ticket app, a travel agent) sells the ticket; the operator pays Delay Repay. Claim on the operator's form, not in the retailer's app, quoting the booking reference from the retailer's confirmation. Automatic and pre-filled schemes usually cover only tickets bought direct from the operator, so retailer bookings stay manual.

## Who may submit (GTR's passenger rule)

Thameslink's Delay Repay page says claims must be made by the person who experienced the delay, and that third-party claims are accepted only in mitigating circumstances, such as travelling with children. Thameslink, Southern, Great Northern and Gatwick Express share one claims system (Govia Thameslink Railway). It also warns that it may prosecute fraudulent claims, and that duplicate claims for one journey are declined.

So, for every operator:

- The claim goes in the passenger's own name, with their own contact and payment details.
- Act only on the person's instruction, in their session, and let them review before submitting.
- Do not claim for a friend or family member who travelled on their own ticket.
- A booking the person paid for with others on it: claim for the group only if the form asks for the number of passengers.

## Season tickets

Operators pay a pro-rated daily value of a season ticket, using their own published formula, not a share of a fare. Untap does not model season-ticket amounts and saved commutes support day tickets only. Use Untap to confirm the train and the delay, then take the amount from the operator's form. GTR caps season-ticket Delay Repay per day.

Giving a season ticket back is a separate refund process (the price paid, minus the weekly price for each week used, minus an admin fee), through whoever sold it. It is not Delay Repay.

## Evidence and the form

A claim usually needs: the date, the departure and arrival stations, the scheduled train, the booking reference or a photo of the ticket, the ticket type and price, and how to be paid. Untap's `claim_pack.fields` gives each value and where to find any it does not know.

- A booking confirmation email or app receipt is usually enough proof of purchase. A line on a bank statement helps when the ticket is lost.
- Advance tickets are covered. Delay Repay is not an ordinary refund.
- Operators can see their own running data. Do not attach made-up screenshots or timings.

## Response, chasing and the Rail Ombudsman

1. Untap's claim steps allow 20 working days for the operator to respond. Chase once in writing after that, quoting the claim reference.
2. If the claim is refused and the person thinks that is wrong, complain to the operator first.
3. **Rail Ombudsman** (free, https://www.railombudsman.org): once the operator has had 40 working days or has sent a final response (a "deadlock letter"), and within 12 months of that final response. Its decisions bind the operator, not the passenger.

Never suggest a claims company for Delay Repay: the amounts are small, the form is short and the escalation is free.

## What Untap does not cover

- Trains older than about a year (records run roughly the last year, and each day appears the next day).
- Journeys with a change, as one check. Check each train.
- Operators outside the table above, and Delay Repay on the Elizabeth line or London Overground (see the TfL reference).
- Season-ticket amounts, Room Supplement refunds on the Caledonian Sleeper, and c2c's automatic 2 to 14 minute payments.

## Sources

- Untap's rules, open data: https://untap.money/open-data/rules/delay-repay-operators.json
- Untap guide, Delay Repay by operator: https://untap.money/guides/train-delay-repay
- Office of Rail and Road, compensation and refund rights: https://www.orr.gov.uk/rail-passenger-compensation-and-refund-rights
- National Rail Conditions of Travel: https://www.nationalrail.co.uk/NRCOT/
- Thameslink, Delay Repay: https://www.thameslinkrailway.com/help-and-support/delay-repay
- Rail Ombudsman: https://www.railombudsman.org/
