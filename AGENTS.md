# AGENTS.md

## Project Overview

This repository contains a keynote talk deck and its speaker notes.

- Main deck: `index.html`
- Speaker notes: `speaker-notes.md`
- Presentation framework: Reveal.js assets in `reveal/`

The deck is a single-file HTML presentation with inline styles and slide content. There is no separate build step.

## Talk Context

- This is a keynote, not a paper talk.
- The audience is broad ICSE-style software engineering audience, with many researchers in the room and some industry practitioners.
- The talk should be intellectually sharp, but still generous, accessible, and inviting.
- The talk is based on industry lessons from large-scale systems and long-lived software.

## Core Message

The central thesis of the talk is:

- At scale, the hardest problems are often in architecture, infrastructure, data, time, migration, and coordination, not only in local code structure.
- Design decisions age.
- Refactoring and migration are inevitable.
- Good design is less about timeless elegance and more about reversibility, survivability, and safe change.

## Audience / Tone Guidance

When editing the deck or notes, keep these constraints in mind:

- It is a keynote: aim for strong, memorable ideas rather than dense technical detail.
- The audience includes researchers: avoid sounding anti-academia.
- Provocation is fine, but it should feel constructive, not dismissive.
- Prefer nuance over absolutist claims.
- Avoid turning the research close into a niche tooling wishlist; keep it high-level and relevant to many kinds of researchers.
- The talk should feel confident and opinionated, but not combative.

## Content Priorities

The current narrative emphasizes:

- "Scale" is multi-dimensional: traffic, uptime, data, teams, services, coordination, regulation, and time.
- The cost of change is a more important lens than static code beauty.
- Migration paths, rollout strategies, compatibility periods, and organizational boundaries are part of design.
- Code quality still matters, but the talk is not primarily about local code cleanliness.
- Socio-technical concerns matter: ownership, team boundaries, decision-making, and Conway's Law affect changeability.
- The research close should invite broader engagement with real change in real systems.

## Editing Rules

If you change `index.html`, you must also review and update `speaker-notes.md` in the same session.

Required synchronization rules:

- The speaker notes must follow the exact current slide order.
- Slide additions, removals, or moves must be reflected in the notes immediately.
- Slide numbering in `speaker-notes.md` must stay accurate.
- If slide titles or core claims change, update the matching notes so they are not stale.
- Do not leave the deck and notes semantically out of sync.

## Slide Design Guidance

- Keep slides sparse: one strong idea per slide when possible.
- Prefer short headlines and minimal supporting text.
- Avoid repeating the same idea across too many consecutive slides unless the user explicitly wants more emphasis.
- Use bullets only when the audience needs a list to scan.
- Preserve the keynote rhythm: thesis -> concrete story -> lesson -> broader principle.
- When possible, move to stories and examples early rather than over-explaining the thesis abstractly.

## Speaker Notes Guidance

- Notes should help the speaker land the point of the slide, not restate the slide word-for-word.
- Notes can carry nuance that is too long for the slide, but they must still match the slide's current message.
- Notes should explain transitions between sections when the deck makes a conceptual jump.
- If a slide is provocative, the notes should usually contain the softening nuance.

## Current Structural Intent

Future edits should generally preserve these high-level beats unless the user asks for a larger rewrite:

1. Set context and define what "scale" means.
2. State the thesis that large-scale pain often lives beyond code.
3. Move into concrete migration/change stories early.
4. Treat time and socio-technical factors as part of design.
5. Bridge explicitly into the code-design section.
6. Use the code section to discuss changeability, not code aesthetics alone.
7. Close with practical principles and a broad, inclusive research invitation.

## Things To Watch Out For

- Do not accidentally make the talk say "code quality does not matter."
- Do not let the close become hostile toward researchers.
- Do not bloat the deck with too many near-duplicate principle slides.
- Do not make the slide text more absolute than the notes can defend.
- Do not add detailed technical mechanisms unless they clearly support the keynote story.

## Suggested Editing Checklist

Before finishing a session that changes the talk:

1. Check the slide order in `index.html`.
2. Check that `speaker-notes.md` reflects the same order.
3. Verify the note headings and slide numbers are still correct.
4. Confirm the talk still reads like a keynote, not a lecture or paper.
5. Look for repeated ideas that can be compressed.
6. Make sure provocative lines are balanced by nuance in the notes.
