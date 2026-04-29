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
> Add instructions to the README about how to run the program. Include the URL (https://peter.beens.ca/Wordle-Aid/) and the option for downloading just the index.html file for offline use. Also, add an MIT License section to the README.

**Technical Context:** Updated README.md with an Online/Offline usage guide (pointing to the custom domain) and a standard MIT License notice.
