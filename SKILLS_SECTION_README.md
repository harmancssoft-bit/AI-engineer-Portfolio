# Skills Section Revert Notes

This file records the portfolio changes around the hero skill burst and the Skills section so they can be reverted or adjusted quickly later.

## Files changed

- `dist/index.html`

## Skill burst components

The hero skill animation lives in these places:

- CSS: `.character-wrap`, `.character-wrap:after`, `.character-wrap.skill-burst`, `.orbit-chip`, `.orbit-chip:nth-of-type(...)`
- HTML: the `<span class="orbit-chip">...</span>` labels inside `#characterWrap`
- JavaScript: `triggerSkillBurst()`, `moveCharacter(e)`, and `resetCharacter()`

Current behavior:

- Skills are hidden at the Pokeball/hand area by default.
- The idle Pokeball glow is hidden so it does not leave a red mark near the hand.
- When the faster preloader reaches 100%, the character appears and the pills burst from the Pokeball once, then fade back quickly.
- On hover, the pills burst outward around the lower body/side area and reverse into the Pokeball on mouse leave.
- The face area is intentionally avoided.

## Project layout and page transition

- Production projects are stacked in the left column: Astravi first, SENSE AI below it.
- Personal projects are stacked in the right column: LinkedIn Optimization Agent first, Agentic Job Applier below it.
- The About Harman section uses `#about.section-visible` with IntersectionObserver to create the overlapping page transition over the hero.

## Skills section components

The main Skills section lives in:

- CSS: `.skills-grid`, `.skill-group`
- HTML: `<section class="dark" id="skills">...`

Current layout:

- 3-column desktop grid.
- Wider cards with more spacing.
- Skill groups: GenAI Systems, AI Agents, Backend AI, Data / Retrieval, Automation / QA, Client / Team.

## Fast revert approach

Use git diff/history for `dist/index.html`, or ask Codex:

> Revert only the hero skill burst and Skills section to the version before `SKILLS_SECTION_README.md` was created. Keep project and experience content unchanged.
