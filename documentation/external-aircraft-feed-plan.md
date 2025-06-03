# External Aircraft Feed Requirements and Plan

This document outlines the required data for creating aircraft in OpenScope from an external source and proposes tasks to decouple external traffic from the internal Traffic Generator.

## Minimum Required Aircraft Data

Based on the spawn pattern documentation and the code that builds aircraft objects, each externally supplied aircraft must provide:

- **Airline and weight** – used to choose an aircraft type and callsign.
- **Category** – `arrival`, `departure`, or `overflight`.
- **Route** or list of waypoints – defines the path to follow.
- **Altitude** – spawn altitude or requested altitude.
- **Speed** – indicated airspeed at spawn.
- **Heading** or **initial fixes** – direction or fixes to fly immediately.
- **Spawn rate information** – if the external feed manages spawn timing.

These fields mirror the required spawn pattern keys described in `spawnPatternReadme.md` and `spawnPatternMethodReadme.md`.

Internally, aircraft are constructed with properties such as airline, callsign, type, altitude, position, route, and commands as seen in `_buildAircraftProps` within `AircraftController.js`.

## Proposed Tasks for Decoupling

1. **Expose a Public Creation Interface**
   - Create a method (or event) on `AircraftController` that accepts an initialization object similar to `_buildAircraftProps` and instantiates an `AircraftModel` without relying on `SpawnPatternModel`.
2. **Design External Feed Parser**
   - Build a module to parse external data into the initialization format. This parser should validate required fields and convert coordinates into the simulation's position model.
3. **Separate Spawn Scheduling**
   - Allow the external feed to determine when aircraft are added. The Traffic Generator would continue to handle internal spawn patterns independently.
4. **Synchronization and Updates**
   - If real‑time updates are required, provide a mechanism to update aircraft state (position, altitude, speed) from the external feed while respecting game physics.
5. **Configuration and Controls**
   - Add user controls to enable/disable external traffic and to select the data source. Ensure that existing traffic settings remain functional.
6. **Documentation and Examples**
   - Document the expected external feed format and provide example scripts demonstrating how to push aircraft data into OpenScope via the new interface.

This sequence isolates the new external feeding mechanism from the existing Traffic Generator while preserving the ability to spawn aircraft internally.
