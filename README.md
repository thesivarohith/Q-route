# Q Route

> A privacy-aware ride-safety system that detects suspicious route deviations and starts a passenger safety verification workflow.

[![Status: Independent Open-Source Project](https://img.shields.io/badge/status-independent%20open--source%20project-blue.svg)](#project-status)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)](CONTRIBUTING.md)

## Overview

Q Route is an independent open-source project exploring a practical safety layer for ride-hailing and campus-transport systems.

The system compares a ride's movement with its expected route. If it detects a sustained or otherwise suspicious deviation, it starts a safety verification workflow that lets the passenger confirm that they are safe or request help.

Q Route is an early-stage project. Its implementation and technical design may evolve through open-source discussion, experimentation, testing, and community contribution.

## Problem

Ride-hailing passengers may face situations in which:

- A vehicle takes an unexpected route.
- A vehicle stops for an unusual period.
- The passenger cannot manually open the safety feature.
- Trusted contacts may receive information too late.
- A route change is noticed only after the situation has become serious.
- Existing safety features depend mainly on the passenger identifying danger and taking action.

A route deviation does not automatically mean that a passenger is in danger. Traffic, road closures, navigation errors, and one-way roads can all cause legitimate route changes.

The challenge is to detect unusual ride behavior early without creating excessive false alarms.

## Proposed solution

Q Route explores a safety workflow that:

1. Stores the pickup point, destination, and expected route.
2. Tracks a ride only after the passenger gives consent.
3. Compares movement with a configurable route corridor.
4. Detects sustained or suspicious deviations.
5. Asks the passenger to confirm whether they are safe.
6. Notifies a trusted contact when help is requested or the passenger does not respond.
7. Shows the passenger how to contact emergency services manually.
8. Records an incident timeline for testing and review.

The system is intended to assist passengers and trusted contacts. It is not intended to replace emergency services, professional dispatch systems, or official police infrastructure.

## Example workflow

```text
Ride begins
    |
    v
Expected route is created
    |
    v
Location updates are received
    |
    v
Movement leaves the route corridor
    |
    v
Grace period and route re-evaluation
    |
    +--> Valid alternative route? ---> Continue monitoring
    |
    v
Safety verification request
    |
    +--> Passenger confirms safe ---> Close event
    |
    +--> Passenger requests help ---> Notify trusted contact
    |
    +--> No response -----------> Retry and escalate according to policy
```

## Initial scope

Q Route focuses on:

- Ride and route representation.
- Expected-route storage.
- Route-corridor monitoring.
- Configurable route-deviation detection.
- Passenger safety verification.
- Trusted-contact notification workflows.
- Incident-status tracking.
- Emergency-workflow simulation.
- Security, privacy, and threat-model documentation.
- Reproducible testing of safe and suspicious ride scenarios.

Implementation details may vary between deployments and contributors.

## Out of scope

The following are not promised by this project:

- Direct automatic police-station notification.
- Guaranteed emergency response.
- Integration with Rapido, Uber, Ola, or another ride-hailing platform.
- Automatic audio or video recording.
- Facial recognition.
- Driver emotion or voice analysis.
- Continuous location tracking outside an active ride.
- Silent monitoring without user consent.
- Production deployment for real emergencies.

## Design principles

Q Route is developed around these principles:

- **Consent first:** Location monitoring should begin only after clear user consent.
- **Privacy by default:** Collect the minimum information required for the active ride.
- **Human verification:** A route deviation should trigger verification, not an automatic assumption of danger.
- **Low false-alarm rate:** Multiple signals should be considered before escalation.
- **Transparent limitations:** The project must clearly explain what it can and cannot do.
- **Provider independence:** The design should avoid unnecessary dependence on a single map or communication provider.
- **Open collaboration:** Students, developers, security researchers, and domain experts are welcome to contribute.

## Known bottlenecks

### Route-deviation accuracy

GPS data can be inaccurate near buildings, bridges, tunnels, or areas with poor signal. A different route may also be legitimate because of traffic, road closures, or road restrictions.

Q Route should use a configurable route corridor, a grace period, and route re-evaluation instead of treating every GPS difference as a suspicious deviation.

### False alarms

False alarms can cause users to ignore safety notifications. The system should evaluate multiple signals, including:

- Distance from the expected route.
- Duration of the deviation.
- Vehicle stopping time.
- Direction of movement.
- Network and GPS quality.
- Passenger response.

### Connectivity

Location updates may be delayed or unavailable when the device has a weak internet connection. Implementations should support last-known-location handling and delayed synchronization where appropriate.

### Battery usage

Continuous GPS tracking can consume significant battery power. Implementations should use balanced location updates and increase tracking frequency only when a ride becomes suspicious.

### Passenger response

A passenger may be unable to respond because of injury, fear, a dead battery, or lack of network access. The system should use a staged escalation workflow instead of treating a single missed response as proof of danger.

### Emergency integration

Official emergency-service integration requires authorization, technical coordination, privacy safeguards, and operational responsibility. Implementations must not claim direct police integration without appropriate approval.

### Privacy and security

Live location is sensitive information. Q Route implementations should restrict tracking to active rides, protect stored data, control access, and define a suitable retention period.

### Communication channels

Automated calls, SMS, push notifications, and in-app alerts have different technical and regulatory limitations. Each communication channel must be evaluated for reliability, accessibility, and legal compliance.

## Project status

Q Route is an independent open-source project in its initial design and development stage.

The project is open to:

- Technical implementations.
- Alternative architecture proposals.
- Route-deviation algorithms.
- Privacy-preserving approaches.
- Threat modelling.
- Usability research.
- Accessibility improvements.
- Testing tools and simulated ride data.
- Documentation and review.

No feature should be considered production-ready unless it has been implemented, tested, documented, and reviewed for safety and privacy.

## Repository structure

```text
.
├── README.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── LICENSE
├── PRIVACY.md
└── docs/
    ├── problem-statement.md
    ├── system-design.md
    ├── threat-model.md
    ├── route-deviation.md
    ├── emergency-workflow.md
    └── testing-strategy.md
```

## Getting started

Because the project is still in the design and development stage, setup instructions will be added alongside the relevant implementation.

When contributing code, document:

- Required software.
- Environment variables.
- Local development steps.
- Test commands.
- Demo instructions.
- Known limitations.

Never commit API keys, private credentials, personal phone numbers, live location data, or emergency-service credentials to this repository.

## Contributing

Contributions are welcome from students, developers, designers, security researchers, testers, and domain experts.

Before contributing, please read:

- [Contributing guidelines](CONTRIBUTING.md)
- [Code of conduct](CODE_OF_CONDUCT.md)
- [Security policy](SECURITY.md)
- [Privacy principles](PRIVACY.md)

For large changes, open an issue first so that the proposed direction can be discussed before implementation begins.

## Safety disclaimer

Q Route is an independent open-source project for research, education, and experimentation.

It is not an emergency service, a police dispatch system, a substitute for official safety applications, or a guarantee of rescue. During a real emergency, contact the appropriate local emergency service directly.

Do not rely on an untested Q Route implementation for personal safety.

## License

Q Route is released under the [MIT License](LICENSE).

## Acknowledgements

Q Route is being developed as an independent open-source initiative to explore practical, privacy-aware safety technology for ride-hailing and campus transportation.
