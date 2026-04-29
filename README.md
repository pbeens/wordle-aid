# Wordle Aid

A browser-based drag-and-drop tool to help you visualize and strategize your [Wordle](https://www.nytimes.com/games/wordle/index.html) guesses.

## Features

- **Three 5-letter word slots** — drag letters into position to build candidate words
- **QWERTY keyboard palette** — drag any letter from the keyboard; it stays available for reuse
- **Color coding** — click a placed letter to cycle through:
  - *(uncolored)* — not yet evaluated
  - 🟩 **Green** — correct letter, correct position
  - 🟨 **Yellow** — correct letter, wrong position
- **Reorder & move** — drag letters between positions within a word, or across words (swap)
- **Ctrl+drag to copy** — hold Ctrl while dragging a placed letter to duplicate it (source stays). Implemented: Ctrl+drag from a placed word-tile copies it (source stays). Normal drag = swap. Browser shows "+" cursor when Ctrl is held.
- **Remove a letter** — drag it back to the keyboard area
- **Invalid Letters row** — 5 columns matching the word positions; drop letters here to mark which letters *can't* go in each position. Each column holds multiple letters. Click **×** on a chip to remove it.
- **Placement validation** — if you try to drag a letter into a column where it's already marked invalid, the tile flashes red, a toast notification explains why, and the drag ghost snaps back (rejected drop)
- **Rejection feature** — drops are rejected if they conflict with established "Invalid Letters" or other grid state rules.
- **Keyboard letter states** — click a keyboard letter to cycle through:
  - *(normal)* — untracked
  - 🟨 **In word** — letter is in the word (turns yellow)
  - ~~**Eliminated**~~ — letter is not in the word (crossed out in red)
- **Reset All** — clears everything back to a blank slate

## Running Locally

```bash
python -m http.server 8765
```

Then open [http://localhost:8765](http://localhost:8765) in your browser.

No build step, no dependencies — it's a single `index.html` file.

## Tech Stack

- Pure HTML, CSS, and JavaScript (no frameworks)
- Google Fonts: [Inter](https://fonts.google.com/specimen/Inter)

## Author

**Peter Beens** — [github.com/pbeens](https://github.com/pbeens)
