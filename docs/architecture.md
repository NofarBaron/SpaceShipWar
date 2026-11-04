# SpaceShipGame Architecture

This project is a browser-based arcade shooter built with plain HTML, CSS, and JavaScript. It does not use a backend server or database; the game state and user data are stored in memory inside the browser.

## High-level architecture

```mermaid
flowchart TD
    A[User] --> B[Browser]
    B --> C[index.html]
    C --> D[UI sections]
    D --> D1[Welcome screen]
    D --> D2[Register form]
    D --> D3[Login form]
    D --> D4[Preferences screen]
    D --> D5[Game canvas]
    D --> D6[Player history table]

    C --> E[CSS files]
    C --> F[jQuery + Validation]
    C --> G[js_files/game.js]

    G --> G1[Authentication logic]
    G1 --> G1A[Register user]
    G1 --> G1B[Login validation]
    G1 --> G1C[Logout flow]

    G --> G2[Preferences logic]
    G2 --> G2A[Shot key selection]
    G2 --> G2B[Time setting]
    G2 --> G2C[Player color selection]

    G --> G3[Game engine]
    G3 --> G3A[Canvas initialization]
    G3 --> G3B[Keyboard input]
    G3 --> G3C[Player movement]
    G3 --> G3D[Enemy movement]
    G3 --> G3E[Rocket shooting]
    G3 --> G3F[Collision detection]
    G3 --> G3G[Score and timer]
    G3 --> G3H[Game over / restart]

    G --> H[Player history]
    H --> I[Displayed score table]

    G --> J[Assets]
    J --> J1[Audio: space.mp3]
    J --> J2[Images: ships, enemies, rockets]
```

## Game flow

```mermaid
flowchart LR
    Start[Open app] --> Welcome[Welcome screen]
    Welcome --> Register{Register?}
    Register -->|Yes| Form1[Complete registration form]
    Form1 --> Validate[Validate fields]
    Validate --> Save[Add user to in-memory list]
    Save --> Login[Login screen]

    Welcome --> Login2{Login?}
    Login2 -->|Yes| Check[Check username and password]
    Check --> Pref[Preferences screen]
    Pref --> Play[Start game]

    Play --> Loop[gameLoop]
    Loop --> Input[Read keyboard input]
    Loop --> Move[Move player]
    Loop --> Enemies[Move enemies]
    Loop --> Shoot[Fire rocket]
    Loop --> Collision[Check collisions]
    Collision --> Score[Update points]
    Score --> End{Time over or dead?}
    End -->|No| Loop
    End -->|Yes| History[Save score to history]
    History --> Restart[Restart or play again]
```

## Main project structure

- `index.html` — main browser page and UI sections
- `js_files/game.js` — all game behavior, registration, login, preferences, and gameplay logic
- `css_files/` — styling for the screens and game interface
- `audio/` — background music and sound assets
- `media/` — images used by the game

## Runtime behavior

1. The user loads the website in the browser.
2. The browser renders the page using HTML and CSS.
3. `game.js` attaches events for login, registration, menu navigation, and gameplay.
4. User input is handled via keyboard and form events.
5. The canvas-based game loop updates objects and checks collisions every frame.
6. The score history is shown in a table in the browser and is stored temporarily in JavaScript variables.

## Notes for future improvement

This project is a strong candidate for a future Git repository refactor because the visual structure is already organized, and the next steps could be:

- separate logic into modules,
- add real backend persistence,
- create a cleaner landing page and game dashboard,
- improve game UI/UX with modern styling.

## Suggested next Git step

When you create the new repository, keep the project as a front-end game and add documentation like this file to make it easier to present and maintain.
