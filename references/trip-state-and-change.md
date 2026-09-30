# Trip state and controlled itinerary changes

Use this reference for importing, auditing, evaluating, revising, or adapting an existing trip.

## 1. Build trip state before editing

Extract the current plan into six layers:

| Layer | Examples | Default edit policy |
|---|---|---|
| Hard booking | flights, trains, ferry, prepaid hotel nights, timed tickets | locked |
| Hard deadline | latest hotel departure, check-in cutoff, boarding cutoff, airport arrival target | locked |
| Derived availability | city-presence window implied by arrival/departure, hotel stay window, post-ferry city change | derived from hard facts; exclude impossible candidate days |
| Soft anchor | preferred restaurant, sunset viewpoint, market in the morning | movable with reason |
| Optional item | backup museum, snack stop, casual shopping | freely replaceable |
| Assumption | estimated traffic, historical climate, unverified opening hours | re-verify if decision-critical |

For each day record: start/end lodging, fixed times, ordered stops, transport legs, meals, outdoor exposure, known buffers, and optional alternatives.

Do not silently turn a user-provided fact into a researched fact. Preserve provenance: **user-confirmed / source-verified / estimated / unknown**.

**Imported known facts are authoritative for planning state.** If the itinerary already says the traveler arrives at 23:55, do not later treat that day as a daytime candidate or ask the arrival time again. Ask only when sources conflict or a material field is genuinely absent.

Before ranking candidate days, pre-filter them:
1. remove days outside the destination/city-presence window;
2. remove time windows already consumed by hard bookings/deadlines and protected transfer buffers;
3. remove impossible opening-day/time combinations once verified;
4. only then compare geography, detour, weather fit, cost, and experience value.

## 2. Candidate suggestion workflow

When the user gives a suggested place, first resolve the exact POI. If ambiguous, present the likely matches rather than choosing silently.

Research, when relevant:
- exact address/coordinates and whether it is the intended branch;
- hotel → candidate route;
- candidate's route relative to the previous and next scheduled stops;
- opening days/hours and reservation/ticket requirements;
- visit duration only if supported by a source or clearly labeled as a planning allowance;
- weather sensitivity: exposed coast, mountain, island, viewpoint, indoor, mixed;
- transport/parking/last-mile friction;
- current reviews or temporary closure information if material.

### Geography evidence priority

For mainland-China route/distance questions:
1. if the host exposes a connected **高德/AMap MCP** with POI and route/matrix capabilities, use it first;
2. otherwise use `scripts/tencent_lbs.py`;
3. otherwise use a map browser/search;
4. if no source succeeds, report `unknown` and name the missing check.

Use a distance matrix for coarse day/cluster screening when available, then route planning for the final candidate leg. Do not convert straight-line distance into driving time.

Distance from lodging alone is insufficient. The real insertion cost is normally:
**previous stop → candidate → next stop minus previous stop → next stop**.

## 3. Decision card before mutation

Return a compact comparison containing:

- candidate;
- exact location/branch confidence;
- distance/time from lodging;
- incremental detour for the best day;
- best insertion day(s);
- what must move or be dropped;
- hard constraint impact;
- weather fit, only after the venue exposure type (outdoor/indoor/mixed/covered) is verified rather than guessed from its name;
- cost/booking impact;
- physical load;
- evidence gaps;
- recommended edit shape: add / replace / move / defer.

Do not modify the source itinerary in this step.

## 4. Hard-constraint safety

A revision is invalid if it:
- crosses a locked booking or boarding/check-in deadline;
- consumes the protected transfer buffer without explicit user approval;
- schedules a place outside verified opening windows;
- creates a route whose transport duration has not been re-checked;
- depends on a weather-sensitive activity when current warnings/conditions make it unsafe or unavailable.

For airport/rail/ferry/timed-entry days, show the remaining buffer after the proposed change.

## 5. Minimal-diff revision

After explicit approval:
1. edit only the affected day(s);
2. keep unrelated reservations, restaurants, and sightseeing unchanged unless required;
3. re-run route timing for all changed legs;
4. re-check opening/booking/weather dependencies;
5. update per-day clothing advice if outdoor exposure or timing changed;
6. update packing only if the change introduces a new requirement;
7. emit a change log.

Change log template:

| Item | Before | After | Why | New risk |
|---|---|---|---|---|

Also state **unchanged hard anchors** so the user can verify that important bookings were preserved.

## 6. Same-day adaptation

Establish current state first:
- local date/time;
- actual starting point;
- completed/skipped activities;
- active reservations;
- luggage status;
- fatigue/physical condition supplied by the user;
- current weather/warnings;
- earliest realistic departure;
- latest return/transfer deadline.

Past itinerary text is context, not truth about the current state.

## 7. Version behavior

Treat an accepted revision as a new plan version. Keep a human-readable change log. Do not require a database or complex version-control model unless the host supports one.

If the user rejects a candidate, leave the itinerary unchanged.
