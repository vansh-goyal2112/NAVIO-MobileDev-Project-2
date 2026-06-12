# ADR-002: Hardware Requirements

## Status
Accepted

## Date
May 2026


## Decided By

Dhruv, Vansh, Vasu, Ethan – decided together during our Phase 2 planning session


## Context

NAVIO is an AR app, so the hardware question is actually pretty important. We need to know exactly what device features the app depends on so we can handle permissions properly and make sure the app doesn't just crash on a device that's missing something. The tricky part is that GPS sounds like the obvious choice for navigation, but GPS stops working the moment you're inside a building, which is literally the whole problem NAVIO is trying to solve.


## Options We Looked At

Option 1 – Camera only: overlay directions on the camera feed without real AR tracking. Simple but not accurate, the directions wouldn't actually anchor to the real world.

Option 2 – Camera + GPS: combine camera with GPS for positioning. GPS drift indoors makes this unreliable for our use case.

Option 3 – Camera + Accelerometer/Gyroscope: use motion sensors for orientation. Better indoors but still limited without proper AR surface detection.

Option 4 – Camera + ARCore (camera, accelerometer, gyroscope working together): full AR motion tracking and surface detection designed for exactly this kind of use case.


## Decision

We're using Camera + ARCore for all indoor navigation. ARCore combines the camera, accelerometer, and gyroscope together for motion tracking and surface detection. GPS will only be used at the outdoor campus entry point, once you're inside, ARCore takes over completely. But we also understand the scope of this course so we may stick to a simplified AR implementation that will be developed using the AR capabilities available within the React Native ecosystem and only the minimum AR features required for the project will be implemented during this course.


## Why We Chose This

ARCore is designed specifically for this type of indoor AR tracking and spatial interaction. It addresses the limitations of GPS in indoor environments by providing more accurate motion tracking and spatial awareness, and it gives us the surface detection we need to anchor AR waypoints to the real world. Keeping GPS only for the outdoor entry point is the right call, GPS drift indoors makes it unsuitable for precise indoor navigation. Inside a building, ARCore provides a more suitable approach for this environment. Speaker and fingerprint scanner aren't needed for anything NAVIO does, so we kept the hardware requirements lean.


## Trade-offs

The app requires an ARCore-compatible device, so we'll need to add a clear error message for unsupported hardware. Testing also has to happen on a real physical device since ARCore support on emulators is pretty limited. That's a real constraint but it's not unexpected for an AR app.