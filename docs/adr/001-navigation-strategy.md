# ADR-001: Navigation Strategy
 
## Status
Accepted
 
## Date
June 2026
 
## Decided By
Dhruv, Vansh, Vasu, Ethan – decided together during our Phase 2 planning session
 
 
## Context
 
We needed to figure out how users are going to move around inside NAVIO. The app has a few pretty distinct sections, there's a search screen where you look up a room, the actual AR camera view where you follow the directions, and a settings screen. These don't really belong stacked on top of each other, but some of them do have sub-screens (like a room detail page before you start navigating). So we had to pick a structure that handles both of those patterns without overcomplicating things for a team that's still learning React Native.
 
 
## Options We Looked At
 
Option 1 – Stack Navigator only: every screen stacks on top of the last one. Simple to set up but makes it annoying to jump between main sections.
 
Option 2 – Tab Navigator only: persistent tabs at the bottom. Great for flat navigation but doesn't handle drill-down screens well.
 
Option 3 – Drawer Navigator: a slide-out side menu. We felt this was better suited to apps with lots of settings or sections, which NAVIO doesn't have.
 
Option 4 – Hybrid (Tabs + Stacks): bottom tabs for the main sections, stack navigation inside each tab for deeper screens.
 
 
## Decision
 
We went with a Hybrid Stack + Tab Navigator using React Navigation. Bottom tabs for Home/Search, AR View, and Settings. Stack navigation within each tab handles deeper screens like room detail and route preview.
 
 
## Why We Chose This
 
This approach best aligns with NAVIO’s user flow and navigation requirements. Users need the main sections to remain easily accessible through bottom tabs while still being able to navigate to detailed screens, such as room details and route previews, without losing their current navigation context. The hybrid pattern handles that cleanly. React Navigation is also the most widely used navigation library for React Native, the documentation is solid and there's a lot of community support if we get stuck, which matters a lot since none of us have built a full React Native app before.
 
 
## Trade-offs
 
It's a bit more setup upfront than using a single navigator, but it pays off quickly once we start adding screens. The React Navigation docs are thorough enough that we don't expect this to slow us down. Easy to extend with new screens in later phases too.
