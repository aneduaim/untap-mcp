# REST fallback for agents without MCP

Every Untap check is also available over plain HTTPS. Use this when your platform cannot connect an MCP server.

- Endpoint: `POST https://untap.money/api/agent/v1/{tool}`
- Body: JSON, the same arguments the MCP tool takes.
- Response: JSON `{ "tool", "text", "result" }`. `result` is the structured result the MCP tool returns (amount, deadline, `claim_pack`, `save_claim` and so on); `text` is the readable summary.
- Description: `https://untap.money/openapi.json`. Read it first: it is the authority on which tools are exposed, their exact fields, rate limits and errors.
- No account and no API key. Only the open tools (checks, rules, instructions, email scan) are mirrored. Saving and tracking claims needs the MCP server and the person's own sign-in.
- Never put personal details in the URL. Send them in the body.

## Describe the situation

```bash
curl -sS -X POST https://untap.money/api/agent/v1/find_money_owed \
  -H 'Content-Type: application/json' \
  -d '{"situation":"My Southern train from Brighton to Victoria on Monday was about 40 minutes late"}'
```

## Check a train

```bash
curl -sS -X POST https://untap.money/api/agent/v1/check_train_delay \
  -H 'Content-Type: application/json' \
  -d '{"from":"Brighton","to":"London Victoria","date":"2026-09-28","departure_time":"08:05","operator":"Southern","ticket_type":"Off-Peak Return","price_paid":"£27.40"}'
```

If the result lists several candidate trains, ask the person which one they took and repeat the call with `"service_id"` set to that train's id.

## Operator rules only

```bash
curl -sS -X POST https://untap.money/api/agent/v1/get_delay_repay_rules \
  -H 'Content-Type: application/json' \
  -d '{"operator":"Avanti"}'
```

## Check a flight

```bash
curl -sS -X POST https://untap.money/api/agent/v1/check_flight_compensation \
  -H 'Content-Type: application/json' \
  -d '{"flight_number":"BA2551","date":"2026-08-14","from_airport":"LGW","to_airport":"BCN","what_happened":"cancelled","cancellation_notice_days":3}'
```

Leave out `what_happened` and `arrival_delay_minutes` when the person does not know; Untap looks the flight up.

## Check TfL journeys

From the CSV downloaded from the person's TfL account:

```bash
curl -sS -X POST https://untap.money/api/agent/v1/check_tfl_journeys \
  -H 'Content-Type: application/json' \
  -d @journeys.json
```

where `journeys.json` holds `{"csv_text":"<the CSV file's text>"}`, or `{"journeys":[...]}` with one object per row (date, start_time, end_time, mode, from_location, to_location, bus_route, fare_pence, is_max_fare, is_incomplete).

## Get the submission instructions

```bash
curl -sS -X POST https://untap.money/api/agent/v1/get_claim_instructions \
  -H 'Content-Type: application/json' \
  -d '{"claim_type":"train_delay","company":"Avanti","journey_date":"2026-09-28","ticket_type":"Anytime Return","booked_via":"third_party_retailer"}'
```

`claim_type` is one of `train_delay`, `train_cancellation`, `flight_delay`, `flight_cancellation`, `denied_boarding`, `tfl_incomplete_journey`, `tfl_overcharge`. `booked_via` is one of `operator_direct`, `third_party_retailer`, `travel_agent`, `package_holiday`. For flights, add `departure_airport` and `arrival_airport`. If these differ from the OpenAPI description, the description wins.

## Scan emails for candidates

```bash
curl -sS -X POST https://untap.money/api/agent/v1/scan_for_claims \
  -H 'Content-Type: application/json' \
  -d '{"emails":[{"from":"noreply@email.example.co.uk","subject":"Your journey on 28 September","date":"2026-09-28","body_text":"We are sorry your train was delayed..."}]}'
```

Up to 25 emails per call. Send only travel emails, trimmed to what matters.

## When a call fails

- `400` (`invalid_input`, with `issues`): a missing or malformed field. Ask the person for the fact; never fill it with a guess.
- `404` (`unknown_tool`): the response lists the tools that exist.
- `429` (`limit_reached`): wait for the `Retry-After` time; do not loop.
- `500`: Untap could not complete the check. Tell the person, and use the reference files for the rules. Do not quote an amount Untap did not return.
