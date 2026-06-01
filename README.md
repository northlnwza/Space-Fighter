# Space Fighter

Space Fighter is a Java Swing arcade shooting game created as a Programming Paradigm final project. The player controls a rocket at the bottom of the screen, automatically fires bullets, destroys falling asteroids, earns score, and buys upgrades to survive harder waves.

The project demonstrates object-oriented design, event-driven GUI programming, multithreading, resource management, and basic game-state control in Java.

## Features

- Main menu with Play, Settings, How to Play, and Credits screens.
- Player setup screen with name input and difficulty selection.
- Five difficulty levels: Recruit, Soldier, Veteran, Ace, and Impossible.
- Real-time gameplay using keyboard movement and automatic shooting.
- Falling asteroids with different sizes and speeds.
- Score, HP, mission progress, and event log display.
- Upgrade system using score as currency:
  - Buy HP
  - Increase ship speed
  - Increase bullet speed
  - Enable double shot
  - Increase fire rate
  - Activate shield
- Victory and game-over states.
- Background music, sound effects, mute/unmute, volume control, and theme selection.

## Gameplay

The mission is to destroy enough asteroids before the player's HP reaches zero. Asteroids spawn from the top of the screen and move downward. If an asteroid hits the rocket or reaches the bottom of the game area, the player loses HP.

Bullets are fired automatically, so the player's main job is to move the rocket, avoid collisions, and choose upgrades at the right time.

## Controls

| Key | Action |
| --- | --- |
| `A` or `Left Arrow` | Move rocket left |
| `D` or `Right Arrow` | Move rocket right |
| `Esc` | Open settings during gameplay |

## Difficulty Levels

| Difficulty | Starting HP | Objective | Challenge |
| --- | ---: | ---: | --- |
| Recruit | 5 | 20 asteroids | Easier asteroid patterns |
| Soldier | 3 | 60 asteroids | Balanced default mode |
| Veteran | 3 | 60 asteroids | More fast asteroids |
| Ace | 2 | 80 asteroids | Faster and more dangerous waves |
| Impossible | 1 | 175 asteroids | Very high survival challenge |

As the player destroys asteroids, the spawn delay decreases until it reaches the minimum delay for the selected difficulty.

## Project Structure

```text
Space-Fighter/
├── pom.xml
├── README.md
└── src/main/java/Project3_6713118/
    ├── MainApplication.java      # Main menu and application entry point
    ├── GameMain.java             # Player setup and difficulty selection
    ├── GameFrame.java            # Core gameplay screen and game logic
    ├── GameEnitity.java          # PlayerRocket, Asteroid, and Bullet classes
    ├── SettingApplication.java   # Music, mute, and volume settings
    ├── HowtoPlay.java            # How-to-play screen
    ├── Credits.java              # Credits screen
    ├── Utilities.java            # Constants, image helper, sound helper, volume state
    ├── readme.txt                # Group member list
    └── resources/                # Images and audio assets
```

## Main Classes

| Class | Responsibility |
| --- | --- |
| `MainApplication` | Starts the program and displays the main menu. |
| `GameMain` | Collects player name and selected difficulty before starting the game. |
| `GameFrame` | Manages gameplay, score, HP, upgrades, collisions, victory, and game over. |
| `PlayerRocket` | Represents the player's controllable rocket. |
| `Asteroid` | Represents a falling obstacle. Each asteroid runs in its own thread. |
| `Bullet` | Represents a player bullet. Each bullet runs in its own thread. |
| `SettingApplication` | Lets the player change music theme, volume, and mute state. |
| `MySoundEffect` | Wraps Java sound playback using `Clip`. |
| `MyImageIcon` | Resizes image assets for Swing components. |

## Programming Paradigms Demonstrated

### Object-Oriented Programming

The project separates responsibilities into classes such as `GameFrame`, `PlayerRocket`, `Asteroid`, `Bullet`, and `SettingApplication`. Game objects keep their own state and expose behavior through methods.

### Event-Driven Programming

Swing listeners handle menu clicks, hover effects, radio button changes, keyboard input, sliders, and upgrade purchases.

### Concurrent Programming

Gameplay uses multiple threads:

- A spawner thread creates asteroids over time.
- A shooter thread fires bullets automatically.
- Each asteroid updates its own falling movement.
- Each bullet updates its own upward movement.

Swing UI updates are coordinated with `SwingUtilities.invokeLater(...)` where needed.

### State-Based Programming

The game tracks score, HP, difficulty, upgrade state, win condition, shield state, and whether gameplay is currently running.

## Requirements

- Java JDK 26 or newer, based on the current `pom.xml`.
- Apache Maven.
- A desktop environment that can display Java Swing windows and play audio.

If your machine uses an older JDK, update the `maven.compiler.source` and `maven.compiler.target` values in `pom.xml` to match your installed Java version.

## How to Run

Compile the project:

```bash
mvn compile
```

Run the main class:

```bash
java -cp target/classes Project3_6713118.MainApplication
```

You can also open the project in an IDE such as IntelliJ IDEA, then run:

```text
Project3_6713118.MainApplication
```

## Notes for Contributors

- Keep image and sound assets inside `src/main/java/Project3_6713118/resources/` unless the resource-loading strategy is changed.
- Gameplay constants such as speed, upgrade costs, panel sizes, and resource paths are stored in `Utilities.java` inside `MyConstants`.
- When changing Swing UI from background threads, use `SwingUtilities.invokeLater(...)`.
- Be careful with shared game lists such as asteroids and bullets because multiple threads can access them.
- Avoid committing generated build output from `target/`.

## Possible Future Improvements

- Package resources using Maven's standard `src/main/resources` folder.
- Add a Maven exec plugin or runnable JAR configuration.
- Add a pause screen instead of opening settings directly from `Esc`.
- Add high-score saving.
- Improve thread shutdown and use timers or an animation loop for smoother game control.
- Add unit tests for scoring, difficulty settings, and upgrade behavior.

## Team Members

- Thanakrit Jomhong 6713118
- Phurinut Wongwatcharapaiboon 6713245
- Jitchaya Hirunsri 6713222
- Tanop Udomkanaruck 6713233

## License

This project is licensed under the terms in [LICENSE](LICENSE).
