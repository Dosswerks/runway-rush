# Runway Rush

*Get them there on time.*

Runway Rush is a Frogger-inspired arcade game set in a busy airport. The player guides five unique passengers through a crowded terminal concourse and across an active runway to reach their assigned departure gates before time runs out.

---

## Gameplay

The screen is divided into distinct horizontal zones:

- **Start Area** (bottom): The passenger's starting position. A safe zone with a custom background image.
- **Terminal Concourse** (lower half): Six lanes of moving obstacles including crowds of travelers, security carts, and luggage carriers. All move at varying speeds and directions. Contact with any obstacle resets the passenger.
- **Security Checkpoint** (middle): A safe zone where the player can pause. Features flashing siren lights and a custom background image.
- **Active Runway** (upper half): Five lanes of fast-moving vehicles. Service trucks and airplanes are lethal on contact. Baggage trains (marked with yellow and black hazard stripes) are rideable platforms -- the player can jump on, ride across, and jump off. Stepping onto a runway lane without landing on a baggage train results in failure.
- **Departure Gates** (top): Five gates labeled 1 through 5. Each passenger must reach their specific assigned gate. The target gate is shown in the "NOW DEPARTING" banner and is randomized each round.

## Passengers

There are five unique passenger types, each with a distinct visual appearance. The order in which passengers appear is randomized each level. Each passenger is assigned a random gate. Deliver all five to complete a level.

## Controls

- **Desktop**: Arrow keys (Up, Down, Left, Right) for lane-based movement. R to restart. Q to quit to title screen.
- **Mobile**: Swipe in any direction on the game canvas or the dedicated swipe pad below the game. Tap to start, restart, or advance levels.

## Scoring

- Points are awarded for each successful gate delivery, with bonus points for remaining time.
- Collectible bonus items (stars) appear on the field and award 50 points when collected. They do not appear on the Security Checkpoint or Active Runway lanes.
- After all five passengers board, a Net Promoter Score (NPS) is calculated based on movement efficiency. Fewer total moves yields a higher NPS percentage. A perfect direct route for all five passengers scores 100%.

## Difficulty Progression

- Completing all five deliveries advances to the next level.
- Each level increases obstacle speeds by 15%.
- The timer per passenger decreases slightly with each level.
- The player has 5 lives. Each collision costs one life. The game ends when lives or time run out.

## NPS Screen

After all five passengers board, the game pauses and displays:
- A custom 200x200 graphic
- The player's Net Promoter Score as a percentage
- Encouragement text based on the score
- Music stops during this screen and resumes when the next level begins

The player taps, clicks, or presses SPACE to advance to the next level.

---

## Technical Details

### Architecture

Runway Rush is a single-file HTML5 Canvas game with no external dependencies. All game logic, rendering, audio management, and input handling are contained in one `index.html` file. It runs in any modern browser on desktop or mobile.

### Development Process

The game was developed iteratively through conversational AI-assisted coding using Kiro. The process followed this pattern:

1. **Specification**: The game concept was described in natural language, referencing Frogger as the core mechanic and defining the airport theme, lane structure, obstacle types, passenger system, and scoring.

2. **Scaffolding**: The initial HTML/CSS/JS structure was generated with a customizable asset system, splash screen, and game loop -- following the same pattern established in two prior games (Barrel Bears and Can't Drive 55).

3. **Iterative refinement**: Each feature was added, tested, and adjusted through conversation:
   - Lane types and obstacle behaviors were defined and tuned
   - Rideable baggage train mechanics were implemented with a grace period system to prevent instant death on lane entry
   - Collision detection was refined for each zone type
   - The start area was constrained to a single row with skip logic to jump directly to the terminal
   - Mobile swipe controls were added with a dedicated swipe pad
   - High-DPI canvas scaling was added for crisp text rendering
   - The NPS scoring system was designed and implemented
   - Visual polish was applied incrementally: hazard stripes, siren lights, gate highlighting, terminal floor patterns

4. **Asset integration**: All graphics and sounds are loaded through a centralized `CUSTOM_ASSETS` configuration object. Each asset has a fallback -- if the file is missing, a default drawn graphic or no sound is used. Images facing right are automatically flipped horizontally when the lane moves left.

5. **Deployment**: The game is hosted on GitHub Pages as a static site. Assets are stored in an `/assets/` subfolder. Updates are made by uploading files through the GitHub web interface.

### Key Technical Features

- **High-DPI rendering**: Canvas is scaled by `devicePixelRatio` for sharp text on Retina displays
- **Automatic image flipping**: Obstacle images only need one direction; the code mirrors them based on lane direction
- **Lane-based movement**: Classic Frogger grid movement with one-lane-per-input
- **Rideable platforms**: Baggage trains carry the player horizontally with a grace period for jumping between trains
- **Responsive layout**: Canvas scales to fit mobile screens with proportional height
- **Touch controls**: Swipe detection on both the canvas and a dedicated swipe pad below the game
- **Customizable assets**: Every visual and audio element can be replaced via the config object

### Asset System

All custom assets are defined in the `CUSTOM_ASSETS` object at the top of the script:

```javascript
const CUSTOM_ASSETS = {
    boxArtImage: 'assets/box-art.png',
    playerImages: ['assets/passenger1.png', ...],
    terminalObs1: 'assets/crowd.png',
    terminalObs2: 'assets/security.png',
    terminalObs3: 'assets/luggage.png',
    runwayObs1: 'assets/truck.png',
    runwayObs2: 'assets/baggage-train.png',
    runwayObs3: 'assets/airplane.png',
    collectibleImage: 'assets/collectible.png',
    gateFilledImage: 'assets/gate-filled.png',
    startAreaImage: 'assets/start-area.png',
    checkpointImage: 'assets/checkpoint.png',
    sirenImage: 'assets/siren.png',
    npsImage: 'assets/nps.png',
    backgroundMusic: 'assets/music.mp3',
    moveSound: 'assets/move.mp3',
    crashSound: 'assets/crash.mp3',
    gateSound: 'assets/gate.mp3',
    collectSound: 'assets/collect.mp3',
    levelUpSound: 'assets/levelup.mp3',
    gameOverSound: 'assets/gameover.mp3',
};
```

Set any value to `null` to use the default fallback.

### File Structure

```
runway-rush/
  index.html
  story.html
  README.md
  assets/
    box-art.png
    passenger1.png - passenger5.png
    crowd.png
    security.png
    luggage.png
    truck.png
    baggage-train.png
    airplane.png
    collectible.png
    gate-filled.png
    start-area.png
    checkpoint.png
    siren.png
    nps.png
    music.mp3
    move.mp3
    crash.mp3
    gate.mp3
    collect.mp3
    levelup.mp3
    gameover.mp3
```

---

## Credits

Concept, design, art direction, and audio: Andrew Doss

Game engine and code: Built with Kiro AI-assisted development

Hosted on GitHub Pages
