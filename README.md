# Sudoku (HTML + JS, no build)

A lightweight, single-file Sudoku you can host on GitHub Pages.  
Includes timer, three difficulty levels, pause/stop controls, mistake limit, and clue support.

## Features
- **UI**: Black page with centered heading; **white game area** with 9×9 grid and thick 3×3 borders.
- **Controls**: Start / Pause / Stop; **Beginner / Intermediate / Expert** levels.
- **Timer**: Pausable; shows **best time per level** (stored in `localStorage`).
- **Mistakes**: You get **3 chances**. Each wrong entry (digit not matching the solution) costs one life. At 0 → **game over**.
- **Clues**: Up to **3 clues** per game. Fills one correct cell (corrects a wrong-filled cell first, otherwise an empty cell).
- **Keyboard & Mobile**
  - Arrow keys to move, `1–9` to fill, `Backspace` to clear.
  - Inputs use `inputmode="numeric"` for better mobile keyboards.
- **Accessibility**: ARIA roles/labels; live region for status; high-contrast focus ring.
- **No Dependencies**: All logic is client-side; no tracking, analytics, or external libraries.

## Live Demo (GitHub Pages)
1. Create a new GitHub repository and add `index.html` (this file) and `README.md`.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose:
   - **Source:** Deploy from a branch
   - **Branch:** `main` (or `master`) / root
4. Save. Your site will be available at `https://<your-username>.github.io/<repo-name>/`.

## Local Usage
Just open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari).

## How It Works
- Generates a **full valid Sudoku solution** via a base pattern + random row/column/band/stack shuffles.
- **Digs** cells (removes numbers) to reach target **givens** per level:
  - Beginner: ~40–45 givens
  - Intermediate: ~32–36 givens
  - Expert: ~24–28 givens
- Each removal is tested with a fast backtracking solver to **preserve uniqueness** (early exits once 2 solutions are found).

## Best Practices Included
- **Uniqueness check** for puzzles (prevents multi-solution boards).
- **Early-exit solver** for performance.
- **Pause overlay** hides inputs to avoid “peek” cheating.
- **Row / Col / Box highlight** and **same-number** highlight on focus to reduce errors.
- **Strict input sanitization** (accepts only digits `1–9`, clears on invalid).
- **Responsive**: grid scales up to ~540px and down to narrow phones.
- **LocalStorage** best-time per level for replay value.

## Shortcuts & Tips
- **Start** a new game, then:
  - Use **arrow keys** to navigate.
  - Type **1–9** to fill a cell.
  - Use **Backspace** to clear a cell.
- **Clues** (`Get Clue`) are limited to **3** per game.
- If you make **3 mistakes**, the game ends. Wrong entries are rejected and cleared.

## Customization
- Tweak difficulty in `LEVELS` in the `<script>`:
  ```js
  const LEVELS = {
    beginner: {givensRange:[40,45]},
    intermediate: {givensRange:[32,36]},
    expert: {givensRange:[24,28]}
  };
