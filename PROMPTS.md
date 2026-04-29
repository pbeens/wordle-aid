# Wordle-Aid Development Prompts

This file documents the development history of **Wordle-Aid**. It serves as a transparent transcript of the collaborative process between the human developer (**Peter Beens** — [github.com/pbeens](https://github.com/pbeens)) and the AI coding assistant (**Antigravity**). It tracks the evolution of requirements, technical implementation decisions, and the creative direction of the project.

---

### Support & Feedback

- **Report a Bug**: [GitHub Issues](https://github.com/pbeens/Wordle-Aid/issues)
- **Enjoying the tool?**: [Buy Me a Coffee](https://buymeacoffee.com/pbeens)

---

### User Prompt 1 – 2026-04-29 07:34 – Initial Concept

**Goal:** Create a visual Wordle scratchpad with three 5-letter rows and a reusable alphabet palette.

**Prompt:**
> I'd like a web-based Wordle aid. The layout should have blocks at the top for three five-letter words and the alphabet below it. I want to be able to drag and drop letters from the alphabet to the words to visualize different possibilities.
>
> I also want to color-code the letters. Once a letter is placed, I should be able to click it to toggle between Wordle colors: Green for the correct position and Yellow for a valid letter in the wrong position. This is purely a visual tool to help me imagine different word combinations.

---

### User Prompt 2 – 2026-04-29 07:37 – Refining Drag-and-Drop Mechanics

**Goal:** Establish rules for letter reusability, reordering, and removal.

**Prompt:**
> Let's refine the mechanics:
>
> - Letters dragged from the alphabet should stay there (reusable palette) so I can use them in multiple words.
> - I want to be able to reorder letters within a word and move them between words.
> - To remove a letter, I should be able to drag it back to the alphabet area.
> - Clicking a placed letter should cycle through the colors (Green, Yellow, and Uncolored).
> - We don't need to worry about "gray" (excluded) letters in the word slots; if a letter isn't used, I'll just drag it off.
> - No word validation is necessary; it's a free-form scratchpad.

---

### User Prompt 3 – 2026-04-29 07:46 – Alphabet Elimination

**Goal:** Add a way to mark letters as "eliminated" directly on the keyboard palette.

**Prompt:**
> I also want to be able to click letters in the alphabet palette. Clicking a letter should toggle a "crossed-out" state so I can keep track of eliminated letters visually while I work.

**Technical Context:** Implemented a `crossed` CSS state with a red strikethrough and dimmed background for the keyboard keys.

---

### User Prompt 4 – 2026-04-29 07:49 – Duplicate via Ctrl+Drag

**Goal:** Implement a standard "copy" shortcut for faster visualization.

**Prompt:**
> Can we use the standard "Ctrl+drag" convention to duplicate letters? I’d like to be able to hold Ctrl and drag a letter from one slot to another to copy it instead of moving it.

**Technical Context:** Updated the drag-and-drop logic to check for `e.ctrlKey`. Normal drag performs a swap; Ctrl+drag performs a copy of the letter and its color state.

---

### User Prompt 5 – 2026-04-29 07:52 – 3-State Keyboard Cycle

**Goal:** Expand the keyboard palette to track "Known" vs "Eliminated" letters.

**Prompt:**
> Let's upgrade the alphabet click behavior to a 3-state cycle:
>
> 1. First click: Mark as "in the word" (Yellow).
> 2. Second click: Mark as "eliminated" (Crossed out).
> 3. Third click: Reset to normal.

---

### User Prompt 6 – 2026-04-29 08:02 – Position-Specific Invalid Letters

**Goal:** Add a way to track letters that are known to be in the word but are "invalid" for specific positions.

**Prompt:**
> I want to add an "Invalid Letters" row below the three words. This row should also have five slots, but each slot must be able to hold multiple letters.
>
> If I know a letter belongs in the word but *cannot* go in a specific position, I'll drag it there. This helps me track those "Yellow" letter rules more effectively.

**Technical Context:** Implemented an `invalidLetters` array-of-arrays. Used a chip-style layout within the slots to allow multiple letters per position, including a small "x" on each chip for easy removal.

---

### User Prompt 7 – 2026-04-29 08:14 – Placement Validation

**Goal:** Prevent accidental placement of letters into positions already marked as invalid.

**Prompt:**
> Let's add a validation rule: If I attempt to drag a letter into a position where it has already been marked as "invalid," the app should reject the placement.
>
> Maybe the letter could "fly back" to where it came from and show a quick message explaining why it was rejected.

**Technical Context:** Leveraged the native HTML5 drag-and-drop "reject" behavior (skipping `preventDefault` on invalid targets). Added a red-flash CSS animation and a temporary toast notification for user feedback.

---

### User Prompt 8 – 2026-04-29 11:11 – Support Features & Deployment

**Goal:** Add bug reporting and support links to both the README and the web page, and a styled "Buy Me A Coffee" modal to the app.

**Prompt:**
> I want to add a link at the very bottom of the README and on the web page itself that says "Report an Issue" (linking to the repo's issues).
>
> Also, add a "Buy Me A Coffee" button to the web app. When clicked, it should show a pop-up saying "If you are enjoying this, please consider buying me a coffee" with a link to the site.
>
> Finally, help me configure the site for GitHub Pages.

**Technical Context:** Added a fixed-position support container to the UI with a "Report an Issue" link and a "Buy Me a Coffee" button. Implemented a modal overlay for the coffee message.

---

### User Prompt 9 – 2026-04-29 11:21 – Final README Polish
**Goal:** Add usage instructions and licensing to the README.

**Prompt:**
> Add instructions to the README about how to run the program. Include the URL (https://peter.beens.ca/wordle-aid/) and the option for downloading just the index.html file for offline use. Also, add an MIT License section to the README.

**Technical Context:** Updated README.md with an Online/Offline usage guide (pointing to the custom domain) and a standard MIT License notice.

---

### User Prompt 10 – 2026-04-29 12:02 – Adjust Keyboard Cycle Order
**Goal:** Change the keyboard click order to prioritize elimination.

**Prompt:**
> I want to change the order of clicking on the letters of the alphabet. The first time that I click on a letter, I would like it to be struck out. The second time I click on it, I would like it to be highlighted like it's a valid letter.

**Technical Context:** Updated the `KEY_STATE_CYCLE` object in `index.html` to `normal → crossed → in-word → normal`.

---

### User Prompt 11 – 2026-04-29 12:17 – Add Official Wordle Link
**Goal:** Add a direct link to the NYT Wordle game for convenience.

**Prompt:**
> Let's add an open Wordle link. We can put that right above "Report an issue" and make sure it opens in a new tab.

**Technical Context:** Added a link to `https://www.nytimes.com/games/wordle/index.html` in the support container on the web page.

---

### User Prompt 12 – 2026-04-29 12:20 – Auto-update Keyboard State
**Goal:** Automatically mark letters as "in the word" when added to the invalid list.

**Prompt:**
> If I drag a letter to the invalid list, automatically change its color state on the keyboard.

**Technical Context:** Updated the `drop` handler in `makeInvalidSlot` to set the letter's state in `keyStates` to `'in-word'` whenever a letter is dropped into an invalid position slot.

---

### User Prompt 13 – 2026-04-29 12:21 – Auto-update Keyboard on Green Tile
**Goal:** Automatically mark letters as "in the word" when a tile is marked as correct (green).

**Prompt:**
> Let's do the same thing. If I drop a letter and then I mark it as the correct location... [automatically change its color state on the keyboard].

**Technical Context:** Updated the `click` handler in `makeTile` to set the letter's state in `keyStates` to `'in-word'` whenever a tile is cycled to the `'green'` state.

---

### User Prompt 14 – 2026-04-29 13:00 – Mobile Interaction Experiment
**Goal:** Create a touch-friendly version of the app for mobile devices.

**Prompt:**
> How difficult would it be to make it mobile friendly as well? ... Let's create an index_mobile that we can start experimenting on. Instead of drag, it would be to touch a button, then touch the location, something like that.

**Technical Context:** Created `index_mobile.html` using a "Select then Place" interaction model. Removed all native Drag and Drop logic in favor of `click` events that manage a `selection` state. Implemented responsive CSS using `clamp()` and flexbox to optimize for portrait mobile screens.
