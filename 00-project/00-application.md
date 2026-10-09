---
name: Karpov Artemii
neptun: B3D5N4
id: 2026-NP-04
---
# Deterministic Replay and State Synchronization for Games

## My interpretation of the brief
The project is a system capable of recording and reproducing replays of a simulated system, capable of detecting divergence and recovering via snapshots in case of a state mismatch. This must be done while keeping storage and performance overhead at minimum, minimalizing amount of data stored per replay.

## Why I am a good fit for this project
I am interested in furthering my knowledge in game development, and replays in particular are of high interest to me as such a project has been previously unsuccessfully attempted by other maintainers at a project I work on (see below), but failed due to performance, storage size and determinism issues with the implementation.

## Relevant experience and background
I have over seven years of open-source multiplayer game development background and creating modifications for closed-source games, as can be seen on my [main GitHub Account](https://github.com/SmArtKar). I am one of the primary maintainers for one of the main forks of one of the oldest open-source videogames, and have vast experience with designing the architecture and optimizing performance of complex internal systems.

## Proposed approach
I would create a simple simulation influenced both by pseudo-random number generation and external user input in the Unity engine using the C# language. Then I would create the recording/snapshotting system, followed by a replay player capable of reproducing the saved data. After this I will profile the system performance and run experiments, evaluating and comparing system performance overhead, replay file size and divergence recovery capabilities to existing systems.

## Initial plan
1. Define the rules and interactions of the simulation system, process utilized to store replays and snapshot states, and means of recovery in case of divergence.
2. Write the specification and initial technical proposal.
3. Create the simulation used as testing grounds for the replay system.
4. Create the recording and snapshotting system, followed by replay and recovery systems.
5. Profile and optimize performance and recovery capabilities of the system.
6. Compare the final project with existing competitor systems.

## Additional information
I plan to maintain a Git repository from the start and use issues to track work. I will utilize the Unity engine and C# language for both the simulation and the replay systems, and a custom format for the replay data.
I prefer to avoid utilizing AI/LLM tools when possible as I believe the long-term cost of system maintainability and knowledge is not worth the short-term speed tradeoff, only utilizing simplified versions as autocomplete to speed up the process of writing boilerplate code.
