# Flights: UK261 and EU261

Read this when a flight was delayed, cancelled or overbooked. Always run `check_flight_compensation` before quoting an amount: the scheme, distance band, arrival delay, notice given and any rerouting all change the answer.

## Contents

- UK261 or EU261: which applies
- The amounts and bands
- The 1,500 km EU rule
- The 3 hour threshold
- Cancellations and notice
- Rerouting and the half rate
- Denied boarding
- Extraordinary circumstances
- Care and refunds are separate
- Deadlines
- Claiming, chasing and dispute bodies (ADR and PACT)
- Claims firms compared with claiming direct
- What Untap does not cover
- Sources

## UK261 or EU261: which applies

UK261 is Regulation 261/2004 as kept in UK law after Brexit. EU261 is the EU original. The substance is the same; the currency and one distance rule differ.

| Flight | Scheme Untap applies |
|---|---|
| Departs a UK airport, any airline | UK261, in pounds |
| Departs an EU airport (or Iceland, Liechtenstein, Norway, Switzerland), any airline | EU261, in euros |
| Arrives in the UK from outside the UK and EU, on a UK or EU airline | UK261 |
| Arrives in the UK from outside the UK and EU, on any other airline | Not covered |

Codeshares follow the airline that operates the flight, not the one that sold the ticket. Let Untap decide; it reports the scheme it used.

## The amounts and bands

Per passenger, fixed in law, whatever the ticket cost. Distance is the great-circle distance between the airports.

| Distance | UK261 | EU261 | Half rate |
|---|---|---|---|
| Up to 1,500 km | £220 | €250 | £110 / €125 |
| 1,500 to 3,500 km | £350 | €400 | £175 / €200 |
| Over 3,500 km | £520 | €600 | £260 / €300 |

The half rate applies to a long-haul delay of 3 to 4 hours on arrival, and to the rerouting cases below. Quote Untap's amount and band; it applies the edge cases.

## The 1,500 km EU rule

Under EU261 only, a flight between two EU airports of more than 1,500 km is paid at the middle band even above 3,500 km (Dublin to Larnaca pays €400, not €600). The UK text dropped this wording, so a UK flight over 3,500 km to an EU airport pays £520.

## The 3 hour threshold

Compensation for a delay starts at 3 hours late on arrival, when the aircraft doors open at the destination. A flight that left 3 hours late but made up time in the air and arrived under 3 hours late does not qualify. Use the arrival delay, not the departure delay, in `arrival_delay_minutes`.

## Cancellations and notice

| Notice before departure | Compensation |
|---|---|
| 14 days or more | None |
| 7 to 13 days | Owed, unless the rerouting left no more than 2 hours earlier and arrived less than 4 hours later than planned |
| Under 7 days | Owed, unless the rerouting left no more than 1 hour earlier and arrived less than 2 hours later than planned |

Untap requires 15 or more calendar days before it treats a cancellation as exempt, because notice is captured as a date, not an exact time. Pass `cancellation_notice_days` from the airline's cancellation email. Keep that email: it is the evidence if the airline disputes the notice date.

## Rerouting and the half rate

When a cancelled flight is still compensable and the replacement arrived less than 2 hours (short band), 3 hours (middle band, and EU intra-community flights over 1,500 km) or 4 hours (long band) after the original arrival time, the airline may pay half. Untap follows the CAA and halves only strictly below those figures.

## Denied boarding

If the airline bumps the person because the flight was overbooked, UK261 and EU261 pay compensation. Pass `what_happened: "denied_boarding"`.

## Extraordinary circumstances

The airline owes nothing if it proves a specific event outside its control that it could not have avoided with all reasonable measures. The bar is high, and the airline must prove it.

- Usually extraordinary: severe weather, air traffic control restrictions, security alerts, strikes by third parties such as air traffic controllers.
- Usually not: technical faults (Huzar v Jet2, Court of Appeal, 2014), crew or staff illness (Lipton v BA Cityflyer, UK Supreme Court, 2024).
- Weather at a prior airport or an air traffic control slot may or may not count. Ask the airline in writing for the specific reason and evidence.
- A voucher accepted at the airport does not replace the compensation right unless the person clearly signed it away.

Untap returns an `extraordinary_circumstances` caveat. Pass it on; do not promise payment.

## Care and refunds are separate

Whatever the cause, the airline must look after delayed passengers: meals and drinks in reasonable relation to the wait, two phone calls or emails, and a hotel and transfers if the delay runs overnight. For a cancellation the person may choose a refund or rerouting at the earliest opportunity. If the airline did not provide care and the person paid for it, keep the receipts and ask the airline to reimburse reasonable costs, separately from the compensation claim.

## Deadlines

Six years from the flight date in England, Wales and Northern Ireland, and five years in Scotland, for bringing a court claim. The CAA's complaints team will not take a complaint when less than a year of that time is left. Untap's claim pack gives the date it calculates.

## Claiming, chasing and dispute bodies (ADR and PACT)

1. **Claim direct with the airline**, on its own claim form (Untap returns the link). One claim can include everyone on the booking the person paid for; the amount is per passenger. Give the booking reference, flight number, date, scheduled and actual arrival, the names of the passengers and the amount.
2. **Wait, then chase.** There is no single statutory reply time. Chase once in writing after about two weeks.
3. **Escalate for free** when the airline refuses or has not replied within 8 weeks of the written complaint. Untap's `claim_pack.escalation` names the right body:
   - **CEDR** or **AviationADR**: the two ADR bodies the CAA approves. Free. Apply within 12 months of the airline's final response. The decision binds the airline if the passenger accepts it.
   - **The CAA's Passenger Advice and Complaints Team (PACT)**: for airlines in no ADR scheme. UK261 only, free, and its view does not bind the airline.
   - **Schlichtung Reise & Verkehr**: the German scheme some airlines (Lufthansa, Swiss, Austrian, Brussels Airlines) have joined.
   - **EU261 claims**: the national enforcement body of the country flown from.
4. **Last resort:** the small claims court (Money Claim Online in England and Wales), within the six or five year limit. It carries a fee.

Which airline is in which scheme changes; trust Untap's result, which follows the CAA's list (checked 30 September 2026).

## Claims firms compared with claiming direct

Claiming direct is free and the airline pays the same fixed amount whoever asks. Claims firms keep a share. Published fees, as Untap's guides record them (checked July and August 2026):

| Firm | Published fee |
|---|---|
| AirHelp | 35% including VAT, plus 15% if legal action is needed |
| Bott and Co | 42% plus VAT, about 50.4% |
| Flightright | 20 to 30% plus VAT, plus 14% if lawyers are involved |

On £520 at 35% the person keeps £338. Only mention a firm if the person asks, or if the airline has already refused and the person will not escalate themselves. Never sign the person up without their explicit choice.

## What Untap does not cover

- Flights older than about a year are not in the flight-status records. Untap can still apply the rules to facts the person gives (`what_happened`, `arrival_delay_minutes`), and the result says the verdict rests on what they said.
- Airports not in Untap's database: the check cannot work out the distance. Say so.
- Flights outside UK261 and EU261 (for example, into the UK on a non-UK, non-EU airline). Other rules may apply; Untap does not check them.
- Baggage, missed connections on separate bookings, package holiday claims and insurance.

## Sources

- Untap's rules, open data: https://untap.money/open-data/rules/flight-compensation-bands.json
- Untap guide, UK261: https://untap.money/guides/flight-compensation-uk261
- Untap guide, claims companies: https://untap.money/guides/claims-companies
- Regulation 261/2004 as it applies in the UK, Article 7: https://www.legislation.gov.uk/eur/2004/261/article/7
- Regulation 261/2004 as adopted by the EU, Article 7: https://www.legislation.gov.uk/eur/2004/261/article/7/adopted
- CAA, delays: https://www.caa.co.uk/air-passengers/travel-problems-and-rights/flight-delays-and-cancellations/delays/
- CAA, cancellations: https://www.caa.co.uk/air-passengers/travel-problems-and-rights/flight-delays-and-cancellations/cancellations/
- CAA, alternative dispute resolution: https://www.caa.co.uk/air-passengers/travel-problems-and-rights/travel-complaints/alternative-dispute-resolution/
- CAA, how PACT can help: https://www.caa.co.uk/air-passengers/travel-problems-and-rights/travel-complaints/how-the-caa-can-help/
- EU national enforcement bodies: https://transport.ec.europa.eu/transport-themes/passenger-rights/air_en
- UK Supreme Court, Lipton v BA Cityflyer [2024] UKSC 24: https://caselaw.nationalarchives.gov.uk/uksc/2024/24/press-summary
