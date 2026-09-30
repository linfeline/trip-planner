# Weather, clothing, and packing rules

Use this reference when weather, outdoor conditions, clothing, or packing can affect the trip.

## 1. Weather must be activity-specific

Do not attach one city forecast to the whole day. **Verify venue exposure before classifying it**; do not assume a waterfront district, "water city", mall-adjacent attraction, or named complex is sheltered/indoor merely from its name. Classify each important activity:
- high visibility sensitivity: viewpoint, mountain panorama, skyline, sunrise/sunset;
- exposed outdoor: beach, ferry deck, island, ridge, waterfront;
- ordinary outdoor: city walk, market, park;
- mixed indoor/outdoor;
- indoor;
- unsafe/closed under specified warnings or official restrictions.

Check the dimensions that matter: temperature, apparent temperature when available, rain, wind/gusts, visibility/cloud, warnings, sunrise/sunset and road/sea conditions when relevant.

For forecasts outside the reliable forecast horizon, use historical/climatological guidance and label it as such. Never present a far-future daily forecast as current fact.

## 2. Clothing recommendation model

Recommend clothing from **weather × exposure × activity × time of day**, not temperature alone.

Consider:
- minimum/maximum and apparent temperature;
- wind exposure (coast, ferry deck, mountain, bridge, open observation deck);
- rain probability/intensity;
- sun/UV when available;
- walking intensity and indoor/outdoor transitions;
- early morning/night exposure;
- user-supplied cold/heat tolerance.

Output each day as a compact set:
- base layer/top;
- outer layer;
- bottoms;
- footwear;
- rain/sun/wind accessory;
- one short reason tied to the day's activities.

Use conditional wording when forecast confidence is low.

## 3. Packing aggregation

After daily clothing decisions, deduplicate into a trip-level packing list.

Calculate quantities conservatively from:
- trip length;
- laundry availability;
- repeat-wear suitability;
- activity changes;
- wet-weather contingency;
- baggage limits already confirmed by the user.

Separate:
- wear on departure;
- pack in main bag;
- day bag;
- documents/tickets;
- weather gear;
- medication/personal items only when the user has supplied them.

Do not invent personal medical needs.

## 4. Weather-triggered plan changes

When conditions materially change:
1. protect hard bookings/deadlines;
2. move the most weather-sensitive activity to the best available window;
3. swap with indoor or low-sensitivity alternatives;
4. show what changed and why;
5. update clothing advice for the revised day.

For ferry, island, mountain, coastal cliff, water activities, or other condition-sensitive transport/venues, official closure/suspension notices outrank generic forecast data.

## 5. Example

Instead of: "12–22°C，带外套"

Prefer: "Day 2 afternoon is mostly exposed coast + hilltop; if the current forecast confirms strong wind, use a long-sleeve base + wind-resistant shell + long trousers. Keep the shell accessible rather than buried in luggage. If rain increases, replace the exposed sunset segment with the designated indoor Plan B."

Only include specific weather values when they were actually verified for the relevant date/location.
