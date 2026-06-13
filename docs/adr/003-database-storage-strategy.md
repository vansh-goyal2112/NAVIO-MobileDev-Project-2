# ADR-003: Database / Storage Strategy
## Status
Accepted

## Date
May 2026

## Decided By
Dhruv, Vansh, Vasu, Ethan – decided together during our Phase 2 planning session

## Context
One of NAVIO's core promises is that it works without Wi-Fi once the map is loaded. SAIT buildings have patchy connectivity and students can't be waiting for a network request every time they need to find a room. So we need map data, room names, coordinates, floor layouts, pathfinding nodes, to live on the device. We also need somewhere to save small user preferences like saved rooms or last known location.

## Options We Looked At
Option 1 – No local storage, fetch from API every time: requires internet every single use. Not viable for us.
Option 2 – Remote database with offline caching (Firebase/Supabase): cloud storage that caches locally. This adds backend complexity we don't need right now and goes beyond the scope of this course.
Option 3 – Local unencrypted storage (SQLite + AsyncStorage): map data on device, fast reads, no backend needed, works fully offline.
Option 4 – Local encrypted storage: same as Option 3 but with encryption. Adds complexity without much benefit since the map data isn't sensitive.

## Decision
Local unencrypted storage: SQLite (via expo-sqlite) for the campus map data and AsyncStorage for user preferences like saved rooms and last location. No remote database will be implemented in Phase 2; however, cloud synchronization can be considered in future phases if the application requirements expand.

## Why We Chose This
This is the most straightforward path to the offline-first experience NAVIO needs. SQLite gives us a proper structured store for the map data so we can run real queries (find room by name, look up nearby nodes, etc.) without internet. AsyncStorage handles the lightweight stuff like preferences. We decided against encryption because the campus map data is publicly accessible information, there's nothing sensitive about it and adding encryption in Phase 2 would just add complexity without a real security benefit. If we ever add user accounts or personal data down the line, that's when encryption becomes worth it.

## Trade-offs
Map data updates will require a new app build or a manual sync mechanism, we'll need to bundle the initial campus map data with the app. That's manageable for Phase 2. Remote sync can be scoped into a later phase if the project grows to need it.