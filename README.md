# Colour Clash (tvOS)

A colour-memory game for Apple TV. Memorise a colour, find it again among nine lookalike shades, and beat your best score.

> SE4041 Mobile Application Design and Development, Assignment 02, Part B (tvOS prototype)

**Author:** _Your Name_ (_Your Student ID_)
**Platform:** tvOS (SwiftUI)
**Repository:** https://github.com/LakinduCh/ColorClash_MADD_tvOS

---

## Concept

Colour Clash is a quick, family-friendly living-room game designed for the TV and the Siri Remote. Each game has 5 rounds. A target colour is shown for 3 seconds, then disappears. The player must pick it from a 3x3 grid of very similar shades. The closer the pick, the more points (up to 100 per round).

**Target audience:** families, casual gamers and friends sharing a living-room TV.

**Planned multiplayer:** the start menu already includes a "Multiplayer (Coming soon)" option for turn-based play on one TV.

### Similar existing apps
_Add 2 to 3 similar apps here with a short description and how Colour Clash differs (for example, colour-matching and colour-memory games on the App Store)._

---

## Features

- **Start menu** with Single Player and a disabled Multiplayer button.
- **Three-phase rounds:** Memorise (3-second countdown), Choose (3x3 grid), Reveal (target vs. your pick with hex codes).
- **Scoring:** 0 to 100 points per round based on colour distance, with feedback text ("Perfect match!", "So close!", "Not bad!", "Way off!").
- **Final results:** total score out of 500, a rating (Colour Master, Sharp Eye, Getting There, Keep Practising) and a saved **high score**.
- **Siri Remote support:** focus-based navigation with `.buttonStyle(.card)` and the **Menu** button (`onExitCommand`) returns to the start menu.
- **Smooth animations:** phase transitions and screen changes.

---

## Tech stack

- **Language:** Swift 5+
- **UI:** SwiftUI for tvOS
- **State and architecture:** MVVM with the Observation framework (`@Observable`, `@MainActor`)
- **Persistence:** `UserDefaults` (high score)
- **Concurrency:** Swift concurrency (`Task.sleep`, `.task(id:)`) for the countdown

---

## Project structure

```
Color Clash/
├── ColourClashApp.swift      App entry point
├── Views/
│   ├── RootView.swift        Switches between menu and game, background gradient
│   ├── StartMenuView.swift   Title and Single Player / Multiplayer buttons
│   ├── RoundView.swift       Memorise, choose and reveal phases
│   └── FinalResultView.swift Final score, rating and high score
└── Model/
    ├── GameViewModel.swift   Game rules, state, scoring, high score
    └── GameColor.swift       RGB colour, lookalike generation, distance
```

---

## How to build and run

### Requirements
- A Mac with **Xcode 16 or later**
- tvOS Simulator (for example **Apple TV 4K**) or a real Apple TV

### Steps
1. Clone the repository:
   ```
   git clone https://github.com/LakinduCh/ColorClash_MADD_tvOS.git
   ```
2. Open `Color Clash.xcodeproj` in Xcode.
3. Select the **Color Clash** target, open the **General** tab and check:
   - **Supported Destinations** lists **Apple TV** (remove **Mac** if present)
   - **Minimum Deployments** for tvOS is not higher than your simulator version
4. Choose **Apple TV 4K** from the device menu at the top.
5. Press **⌘R** to build and run.

### Controls in the simulator
| Action | Key / button |
|---|---|
| Move focus | Arrow keys |
| Select | Return |
| Back / Menu | Esc |

### Troubleshooting
| Problem | Fix |
|---|---|
| `'card' is unavailable in macOS` | The run destination is My Mac. Choose an Apple TV simulator |
| "Simulator platform doesn't match supported platforms" | Add **Apple TV** under **Supported Destinations** |
| "OS version lower than deployment target" | Lower the tvOS **Minimum Deployment** or install a newer runtime |

---

## How to play

1. From the start menu choose **Single Player**.
2. **Memorise** the colour shown on screen for 3 seconds.
3. **Choose** the matching colour from the 3x3 grid.
4. See the **reveal**: your points and how close you were.
5. After 5 rounds, view your final score, rating and high score. Choose **Play Again** or **Main Menu**.

---

## Architecture notes

- `GameViewModel` owns all rules and state (round, phase, score, high score). Views only read state and call actions such as `choose(_:)` and `nextRound()`.
- `GameColor` is a simple value type that creates random colours and lookalike shades and measures colour distance.
- A `roundToken` value restarts the memorise countdown each round through `.task(id:)`.

---

## Pitch summary

_Add value proposition, target market, revenue model and go-to-market strategy here, or link to your pitch deck._

---

## Third-party resources and AI use

- No third-party libraries are used; only Apple frameworks.
- AI assistance (Claude) was used during development. Prompts, responses and how they helped are documented in the report.

---

## Screenshots

_Add screenshots here (menu, memorise, choose, reveal, final result)._

---

## License

Created for academic purposes (SLIIT, SE4041).
