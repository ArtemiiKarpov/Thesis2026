---
project_outline: "[[00-project/01-project-outline]]"
---

<!-- 5xl -->
# Deterministic Replay and State Synchronization for Games

A system to record full, deterministic replays of user gameplay or computer simulations and replay them afterwards.

<!-- @space -->

<!-- @set-align left -->
<!-- @set-width 65% -->

**Author**: Karpov Artemii 

**Neptun**: B3D5N4

**Supervisor**: Novak Peter

**Project ID**: 2026-NP-04

---
<!-- @slide Problem -->

## Problem

- Video game developers need to be able to review user gameplay for a variety of reasons, commonly either in order to gain better understanding of playtester experience, or to locate cheaters in multiplayer videogames.
- Continious recording of full world-state is extremely computationally intensive and would require vast volumes of disk space.
- There is a large variety of parameters that have trade-offs that alter on a per-user basis, such as snapshot and checksum frequency that affect replay size and recording overhead, but improve recovery time.

---
<!-- @slide Proposal -->

<!-- @set-scale 75% -->

## Proposal

<!-- @align left -->
A system which allows player inputs and world-events to be consistently recorded without capturing the full world state outside of periodic state snapshots to use for divergence recovery, and provides deterministic, system and time-agnostic RNG for developer use.

<!-- @gap 6 -->

## Target users
<!-- @set-align left -->
- Game developers seeking to have a more in-depth view into playtester experience.
- Game developers needing tools to manually verify if a player is cheating in cases where automated systems cannot detect unnatural behavior.
- Simulation developers that may need to manually review or re-run a portion of the simulation after it concluded to get a better understanding of the events that occured within.

---
<!-- @slide Plans -->

## Planned scope

<!-- @columns 2 4 -->

<!--@set-scale 70%-->
<!-- @set-align left -->

### In-scope
- User input recording system
- Replay reveiw system that runs replay files
- Deterministic RNG
- Minimal interface for opening replay files
- Divergence detection and correction from world-state snapshots
- Embedded widgets for starting/saving and running/pausing/jumping in the replay for players/reviewers respectively
- Small demo used to demonstrate, verify and profile the functionality of the system

<!-- @col-break -->

### Out-of-scope
- Full videogame as a demo
- Multiplayer recording
- Network synchronization of multiple players

<!-- @columns -->

---
<!-- @slide User journeys -->

## Initial user journeys

<!-- @set-align left -->
<!-- @set-scale 60% -->

### User journey 1: Installing the system into a project
- The developer adds the system files to an existing project.
- The developer marks fields such as object position, velocity, player health and ammo, etc for serialization.
- The developer replaces sources of RNG with deterministic versions provided by the system.
- The developer adds widgets for players to start/stop recording, or sets up automatic recording.


### User journey 2: Creating a replay
- The player opens the game.
- The player uses the widget to start a replay, or the replay is started automatically.
- Player's actions are recorded into a replay file.
- The player stops the replay, the replay is stopped automatically, or the game is closed/crashes.


### User journey 3: Reveiwing the replay
- The reviewer opens a file via the app.
- The game is opened in review mode.
- Reviewer uses the widget to pause or continue the replay, or to jump to a specific point in time during the replay.
- The reviewer closes the replay.

---
<!-- @slide Next steps -->

## Next steps

- Review existing systems on the market for functionality, profile if possible to use for comparasions with the finished product.
- Define exact means by which sources of non-determinism such as event odering, RNG, FPEs, mathematical operation inaccuracies need to be handled.
- Prototype the initial technical design of the replay system.