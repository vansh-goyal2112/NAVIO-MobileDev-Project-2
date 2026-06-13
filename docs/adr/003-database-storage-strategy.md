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