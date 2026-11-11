# Events and Ticketing

The common events vocabulary -- the events people attend, the venues that host them, the ticket types on sale, the tickets issued and the attendees who hold them -- distilled from the APIs that already exist. Calendar events belong to the scheduling context. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Event, Events, Ticketing, Event Ticketing, Event Management, Live Events, Conferences, Venues in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| event | 25 | 21 | name 90%, start_at 81%, end_at 76%, id 71%, category 57%, status 57% | events 23, event 5, attractions 1 |
| venue | 7 | 7 | name 100%, id 86%, address 71% | venues 7, venue 1 |
| ticket_type | 5 | 3 | description 100%, id 100%, name 100%, price 100% | ticket-types 2, products 1, ticket_classes 1, ticket_types 1 |
| ticket | 11 | 8 | id 50%, status 50% | tickets 9, ticket 2, passes 1, issued_tickets 1 |
| attendee | 15 | 11 | email 73%, first_name 64%, id 64%, last_name 64%, name 64% | attendees 8, attendee 3, registrations 3, registrants 2 |

Cohort: 123 providers with harvested OpenAPI, 26 crosswalks. Of the providers exposing a event: 44% create, 92% list, 88% fetch, 40% update, 40% delete. Generated 2026-11-10 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- An event agrees on name, start, end, category and id across Eventbrite, Ticketmaster's discovery API, webinar platforms and conference tools, once webhook feeds are set aside.
- An attendee agrees on name and email; whether they checked in and which event they hold sit just below core once Cvent's six listings count once.
- A venue agrees only on id, name and address across the providers that expose one.
- Ticket types are rarely a resource of their own (5 providers); most platforms put prices and tiers on the event.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The Ticketing tag lives here, not in help desk: in APIs.io it mixes support tickets with event and transit ticketing, and this is the event side.
- An event counts only at a provider that also lists venues, sells ticket types, issues tickets or registers attendees (`requires_any`); a bare `/events` is a webhook feed or a calendar entry elsewhere.
- Shows, performances and attractions are events; registrants, registrations and guests are attendees; passes and admissions are tickets.
- Duplicates merged: six Cvent listings, GoTo Webinar.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
