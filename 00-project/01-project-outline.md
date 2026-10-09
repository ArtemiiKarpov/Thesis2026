---
name: Karpov Artemii
neptun: B3D5N4
id: 2026-NP-04
github: https://github.com/ArtemiiKarpov/Thesis2026
---
# Deterministic Replay and State Synchronization for Games

The project implements a system that allows game states to be recorded and replayed at a later date utilizing Unity and C# language. By the end of the project, the user can perform a simple set of actions, and later replay the recording of the previous session. The system should be able to detect divergence and correct itself in such a case, and utilize minimal CPU time and disk space.

## Objectives
- **Primary objective:** Create a complete deterministic replay recorder and player.
- **Target users / stakeholders:** Game developers looking to review player gameplay for data collection or manual cheating investigation.
- **Measurable success criteria:** The system can record and replay any set of player and world actions, including ones affected by randomization with full parity to the original session.
- **Constraints:** Unity, C#.

## Scope
### In scope
- Basic set of player interactions, such as movement, shooting and pressing buttons to demonstrate possible behaviors.
- Set of player-agnostic world behaviors, including ones affected by random number generation.
- Ability to record arbitrary timespans of gameplay and fixed world-states.
- Ability to replay previously recorded gameplay and world-states.
- Automatic divergence detection and correction.
- Profiling of the system, investigation of correlation between system parameters and CPU/disk overhead, and comparasion to similar existing systems.

### Out of scope
- Multiplayer support
- Network synchronization

## Notes
The included set of player interactions and world behaviors serves as a prototype/showcase of the system, and is not part of the core product.
