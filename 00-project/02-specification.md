---
project_outline: "[[01-project-outline]]"
---
# Deterministic Replay and State Synchronization for Games

## 1. Actors and permissions
| Role                  | Needs                                     | Responsibility / access                                |
| --------------------- | ----------------------------------------- | ------------------------------------------------------ |
| Player | Ability to interact with the game world, record replays | Controls the player character, interacts with the world in arbitrary fashion, starts/stops the replay system |
| Reviewer | Review recorded data | Can load and play recorded replay data |

## 2. Use cases / user stories
### Create a recording
- **Actor:** Player
- **Precondition:** The player has started a recording.
- **Main flow:**
  1. The actor moves the player with the keyboard, uses mouse to shoot and press buttons.
  2. The system records player inputs and interactions.
  3. The system records any changes in world-state due to player interactions or player-agnostic events.
  4. The system stores the recording in a replay file.
- **Alternative / error flows:** If the session is aborted early, the replay file must still contain valid data up to the moment the session ended.
- **Postcondition:** The session is recorded in a replay file.
### Replaying a recording
- **Actor:** Reviewer
- **Precondition:** The reviewer has opened a recording file
- **Main flow:**
  1. The system loads the selected recording file.
  2. The actor starts or pauses the replay of the recording.
  3. The actor can jump to any arbitrary point in the recording.
- **Alternative / error flows:** In case of divergence, the system must be capable of detecting and correcting it, or informing the user if state correction fails.
- **Postcondition:** The reviewer finishes the replay.


## 3. Functional requirements
| Requirement                                                               | Acceptance criteria                                                                                                                                 | Priority |
| ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| The player must be able to start or stop a recording | The player should be able to start and stop the recording system at arbitrary times | Must |
| The player must be able to record their actions | Whenever a player performs an action while a recording is active, it must be recorded | Must |
| Player-agnostic events must be recorded | Any event not directly caused by the player must also be recorded whenever it occurs, even if it does not persistently alter the world-state after occuring | Must |
| The reviewer must be able to view the recording | A recording file must be able to be opened by the reviewer in order to view the replay | Must |
| The replay system must be able to verify the validity of a replay | The world-state must be regularly checked for validity in order to detect divergence | Must |
| The replay system must be able to attempt course correction | In case divergence is detected, the system must be able to attempt to correct the replay or issue a warning to the user | Must |
| The player can move around | The player needs to be able to move their avatar with keyboard keys in the game world as part of the demo | Should |
| The player can shoot with their mouse | The player needs to be able to fire projectiles with mouse clicks in order to demonstrate/verify/profile more advanced player interaction recording | Should |
| The player can interact with world objects | Player's projectiles and movement needs to alter the world-state in order to demonstrate/verify/profile recording of not just player actions but the world-state. | Should |
| The demo world can have a random, world-state altering event occur | The world needs to have a random player-agnostic event, such as a light changing color on a random timing, in order to demonstrate/verify/profile deterministic nature of replays and player-agnostic world-state alteration | Should |

Priority: **Must** = required for the final product; **Should** = important; **Could** = optional if time permits.

## 4. Business rules and constraints
| Rule or constraint                                                           | Rationale                                               |
| ---------------------------------------------------------------------------- | ------------------------------------------------------- |
| The recording must be consistently written to the disk in a way that does not overwrite existing data. | Ensures data preservation in case of a crash. |
| The replay must use a local timescale rather than using the system clock. | Prevents non-determinism based on when the replay is ran. |
| The replay must use a system-agnostic RNG. | Prevents non-determinism from the replay being ran on different OSs/system architectures |
| The system must have acceptable CPU/disk overhead | High CPU overhead or disk space consumption make the system undesirable to use compared to other existing systems. |

## 5. User interface and workflow
The main product only consists of a simple app capable of selecting the replay to be ran, and a widget to be embedded in the game/simulation which allows the player to start/stop the recording, and the reviewer to play/pause/jump to a time point in a review.
The demo is a primitive game with a player avatar moved by keyboard, capable of launching projectiles with the mouse and some world objects that can be interacted with in order to test/demonstrate the capabilities of the system.

## 6. Non-functional requirements
| Requirement                                                                                      | How it will be verified                                    |
| ------------------------------------------------------------------------------------------------ | ---------------------------------------------------------- |
| The system must not have a noticeable performance overhead. | System performance measurement when running a replay with large amounts of interactions. |
| The disk space usage must be within acceptable levels. | File size verification after running a long replay/replay with large amounts of interactions. |
| The system can gracefully handle crashes without data loss. | Integration test with a forced process abortion. |

## 7. Open questions and risks
| Question / risk | Impact | Owner | Resolution / decision |
| --- | --- | --- | --- |
| Frequency of snapshots | CPU overhead, replay size | Student | Profile the system and determine the required frequency of full world-state snapshots utilized for divergence detection that is within acceptable performance overhead bounds. |
| Frequency of state verification | CPU overhead, replay size | Student | Profile the system and determine the required frequency of hashes/checksums for divergence detection that is still within acceptable performance overhead bounds. |
| Event ordering | Affects replay validity | Student | Verify that multiple inputs/events within the same frame/tick are deterministic and are always handled in the same order. |
