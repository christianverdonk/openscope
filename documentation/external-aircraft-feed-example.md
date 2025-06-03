# External Aircraft Feed Example

The JSON snippet below illustrates the minimum set of data fields required to create aircraft from an external source. Each object represents one aircraft to be spawned or handed off to OpenScope.

```json
[
  {
    "callsign": "DLH401",
    "airline": "dlh",
    "type": "A320",
    "category": "departure",
    "origin": "EDDH",
    "destination": "EDDF",
    "route": "EDDH.AMLUH8G.AMLUH",
    "altitude": 16000,
    "speed": 250,
    "heading": 330,
    "spawnTime": "2025-06-03T18:00:00Z"
  },
  {
    "callsign": "DLH902",
    "airline": "dlh",
    "type": "A319",
    "category": "arrival",
    "origin": "EDDF",
    "destination": "EDDH",
    "route": "BOGMU.BOGMU05.EDDH",
    "altitude": 30000,
    "speed": 320,
    "waypoints": ["BOGMU", "DH255"],
    "spawnTime": "2025-06-03T18:05:00Z"
  }
]
```

### Field descriptions

- `callsign` – IFR callsign or flight number.
- `airline` – ICAO identifier used to pick the fleet.
- `type` – aircraft model (ICAO code). Optional if the airline fleet provides one.
- `category` – `arrival`, `departure`, or `overflight`.
- `origin` / `destination` – airports relevant to the category.
- `route` – route string or list of fixes.
- `altitude` – spawn altitude or requested altitude in feet MSL.
- `speed` – spawn speed in knots.
- `heading` or `waypoints` – initial heading or array of fixes to fly immediately.
- `spawnTime` – when the aircraft should be created. External logic controls the timing.

This example uses standard JSON so that feeds can be produced by any tooling capable of generating JSON. Each object can be validated against a matching JSON Schema to ensure the required properties are present before injecting traffic into the simulator.
