# Runway Rush

*Get them there on time.*

Runway Rush is a Frogger-inspired arcade game set in a busy airport. The player guides five unique passengers through a crowded terminal concourse and across an active runway to reach their assigned departure gates before time runs out.

---

## Gameplay

The screen is divided into distinct horizontal zones:

- **Start Area** (bottom): The passenger's starting position. A safe zone with a custom background image.
- **Terminal Concourse** (lower half): Six lanes of moving obstacles including crowds of travelers, security carts, and luggage carriers. All move at varying speeds and directions. Contact with any obstacle resets the passenger.
- **Security Checkpoint** (middle): A safe zone where the player can pause. Features flashing siren lights and a custom background image.
- **Active Runway** (upper half): Five lanes of fast-moving vehicles. Service trucks and airplanes are lethal on contact. Baggage trains (marked with yellow and black hazard stripes) are rideable platforms — the player can jump on, ride across, and jump off. Stepping onto a runway lane without landing on a baggage train results in failure.
- **Departure Gates** (top): Five gates labeled 1 through 5. Each passenger must reach their specific assigned gate. The target gate is shown in the "NOW DEPARTING" banner and is randomized each round.

## Passengers

There are five unique passenger types, each with a distinct visual appearance. The order in which passengers appear is randomized each level. Each passenger is assigned a random gate. Deliver all five to complete a level.

## Controls

- **Desktop**: Arrow keys (Up, Down, Left, Right) for lane-based movement. R to restart. Q to quit to title screen.
- **Mobile**: Swipe in any direction on the game canvas or the dedicated swipe pad below the game. Tap to start, restart, or advance levels.

## Scoring

- Points are awarded for each successful gate delivery, with bonus points for remaining time.
- Collectible bonus items (stars) appear on the field and award 50 points when collected. They do not appear on the Security Checkpoint or Active Runway lanes.
- After all five passengers board, a Net Promoter Score (NPS) is calculated based on movement efficiency. Fewer total moves yields a higher NPS percentage.

## Difficulty Progression

- Completing all five deliveries advances to the next level.
- Each level increases obstacle speeds by 15%.
- The timer per passenger decreases slightly with each level.
- The player has 5 lives. Each collision costs one life. The game ends when lives or time run out.

## NPS Screen

After all five passengers board, the game pauses and displays a custom graphic, the player's Net Promoter Score as a percentage, and encouragement text. Music stops during this screen and resumes when the next level begins. Tap, click, or press SPACE to advance.

---

## Technical Details

### Architecture

Runway Rush is a single-file HTML5 Canvas game. The only external dependency is the QR code library used for the tip jar. All game logic, rendering, audio management, and input handling are contained in one `index.html` file. It runs in any modern browser on desktop or mobile.

### Social Sharing

The page includes Open Graph and Twitter Card meta tags for rich link previews when shared on social media. The `box-art.png` asset is used as the preview image.

### Key Technical Features

- **High-DPI rendering**: Canvas is scaled by `devicePixelRatio` for sharp text on Retina displays
- **Automatic image flipping**: Obstacle images only need one direction; the code mirrors them based on lane direction
- **Lane-based movement**: Classic Frogger grid movement with one-lane-per-input
- **Rideable platforms**: Baggage trains carry the player horizontally with a grace period for jumping between trains
- **Responsive layout**: Canvas scales to fit mobile screens with proportional height
- **Touch controls**: Swipe detection on both the canvas and a dedicated swipe pad below the game
- **Customizable assets**: Every visual and audio element can be replaced via the config object
- **Tip jar**: PayPal donation button with QR code on the page footer and game over screen, consistent with other Dosswerks Arcade games

### Asset System

All custom assets are defined in the `CUSTOM_ASSETS` object at the top of the script:

```javascript
const CUSTOM_ASSETS = {
    boxArtImage: 'assets/box-art.png',
    playerImages: ['assets/passenger1.png', ...],
    terminalObs1–3,                    // terminal obstacle images
    runwayObs1–3,                      // runway obstacle images
    collectibleImage, gateFilledImage,
    startAreaImage, checkpointImage,
    sirenImage, npsImage,
    backgroundMusic, moveSound, crashSound,
    gateSound, collectSound, levelUpSound, gameOverSound
};
```

Set any value to `null` to use the default fallback.

### File Structure

```
runway-rush/
  index.html          — game + all logic
  story.html          — backstory and instructions
  README.md
  assets/
    box-art.png       (splash + OG share image)
    passenger1–5.png
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

Concept, design, art direction, and audio: [Andrew Doss](https://www.andrewdoss.com/)

Game engine and code: Built with Kiro AI-assisted development

© 2026 Andrew Doss. All Rights Reserved.
