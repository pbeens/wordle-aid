# Wordle Aid – Prompts

---

### User Prompt 1 – 2026-04-29 07:34 – Initial Concept

> I want a web-based program that's going to be like a wordle aid. All it is, I think, is: give me blocks at the top of the page for three five-letter words, and then the alphabet below it. What I want to be able to do is drag and drop letters to the three words so that I can visualize words.
>
> Also, I would like to be able to perhaps color code words. Maybe once a letter is placed on one of the words, I can click on it to toggle between the wordle colors. Green means I know where it goes; yellow means I don't know where it goes, but it is a valid letter. That way I can just position letters and try to imagine the different words.
>
> Ask me any questions to clarify the requirements, because I'm sure that there are situations I'm not imagining.

---

### User Prompt 2 – 2026-04-29 07:37 – Clarifications

> Okay, dragging a letter from the alphabet, it has to stay because I could be positioning that letter in one of the three different words, just to let me visualize things differently. Yes, reordering within a word, I would like to be able to do that. Yeah, why not? Moving between words, yeah, why not? And then removing a letter. Let's just drag it back to the alphabet, because I think just clicking on the letter once it's been placed, I just want it to toggle between the colors, the Wordle colors for correct position or correct letter but wrong position. I also don't want to worry about the gray or dark letters when they're not in there, because if I discover that a letter is not in the word, I will drag them off of the word. And the toggle order: it will initially go on uncolored, and then green or yellow. I won't be toggling it to gray because if I discover that a letter is not used, I will actually drag it off. I'm not worried about word validation at all. Let's start with that.

**Decisions captured:**

- Letters stay in alphabet (reusable palette)
- Drag within / between words = swap
- Drag back to keyboard = remove
- Click placed tile cycles: uncolored → green → yellow → uncolored
- No gray state, no word validation

---

### User Prompt 3 – 2026-04-29 07:46 – Cross Out Alphabet Letters

> Let me also be able to click on letters of the alphabet. If I click on them, it toggles between x-ing them out and resetting them.

**Implemented:** Click a keyboard letter to cross it out (red strikethrough, dimmed). Click again to restore.

---

### User Prompt 4 – 2026-04-29 07:49 – Ctrl+Drag to Copy

> Is control drag on a PC the standard way of copying something? If it is, then I would like to be able to control drag a letter to duplicate it to another location or word.

**Implemented:** Ctrl+drag from a placed word-tile copies it (source stays). Normal drag = swap. Browser shows "+" cursor when Ctrl is held.

---

### User Prompt 5 – 2026-04-29 07:52 – 3-State Keyboard Click Cycle

> I think I would like to also be able to click on the letter in the alphabet to indicate that it's part of the word. Let's change up the order:
>
> - If I click on it the first time, it changes color to say that it's part of the word.
> - If I click on it a second time, it will cross it off.
> - Then I guess a third time would reset it.

**Implemented:** Keyboard letter click cycle: normal → in-word (yellow) → eliminated (strikethrough) → normal.

---

### User Prompt 6 – 2026-04-29 08:02 – Invalid Letters Row

> I want to add an extra word where I can drag and drop letters, letters that are in the word but in the incorrect position. I still want to have five letters, but for instance I want to be able to drag more than one letter to it, just to indicate letters where they can't go. We could do that.
>
> Right now we've got word one, two, three. Let's add a fourth word. We won't call it word four; we'll call it "invalid letters" or something like that. We can drag and drop letters to locations, so again the locations have to be able to accept more than one letter, theoretically up to four, I guess.

**Implemented:** Added "Invalid" row with 5 multi-letter columns. Drop any letter to add a chip; click × to remove. Drag from word tile = move (source clears); Ctrl+drag = copy (source stays). Duplicate letters per slot are prevented.
