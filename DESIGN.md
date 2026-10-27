---
version: alpha
name: "Mission Control"
description: "A compact Spanish-language mission board for turning small intentions into visible progress."
colors:
  ink: "#101827"
  paper: "#F6F3ED"
  lavender: "#C6B8FF"
  coral: "#FF8D70"
  mint: "#A8E6CF"
  yellow: "#F4D06F"
  muted: "#667085"
  line: "#DFDAD0"
typography:
  sans:
    fontFamily: "Inter, ui-sans-serif, system-ui, sans-serif"
  display:
    fontFamily: "Space Grotesk, Inter, ui-sans-serif, system-ui, sans-serif"
  mono:
    fontFamily: "ui-monospace, SFMono-Regular, Menlo, monospace"
rounded:
  DEFAULT: "1rem"
  sm: "0.75rem"
  md: "1.25rem"
  lg: "1.75rem"
spacing:
  section-gap: "2rem"
  page-max: "90rem"
components:
  button: { }
  card: { }
  dialog: { }
  board: { }
  progress-orbit: { }
---

# Mission Control Design System

## Overview

### Creative North Star

Mission Control feels like a beautifully marked-up field notebook connected to a small flight console: tactile paper surfaces sit inside an ink-dark workspace, while colored markers communicate momentum. The interface is made for a person who wants to start and finish small missions, not administer a project-management system.

### Product context and register

- **Audience and primary job:** Spanish-speaking solo makers and students who need to capture tasks, see what is moving, and resume work quickly.
- **Target market(s) and evidence:** General desktop and mobile web; the brief explicitly requires a small agile MVP and mobile behavior.
- **Locale(s) and language policy:** `es-CO` copy, 24-hour time, local browser date formatting. No English UI leakage.
- **Usage scene:** Short daily check-ins on a laptop or phone, with one mission in focus.
- **Register:** Product tool; warm, focused, quietly playful.
- **Memorable signature:** The circular “orbit” progress mark, used as a summary rather than decoration.
- **Restraint:** No gradients, no noisy illustrations, no dense enterprise tables.
- **Anti-references:** Generic kanban dashboards and gamified streak apps; this should feel intentional and calm, not corporate or addictive.
- **Token ownership/runtime mapping:** This file owns durable visual tokens; `styles.css` mirrors them in `:root` as the runtime adapter.

## Colors

Ink creates a reliable shell and strong contrast. Paper is the working surface. Lavender means progress and selected state, coral means the active “go” moment, mint means completion, and yellow means time-sensitive attention. Muted text is reserved for metadata; the line token keeps the board structured without heavy boxes.

## Typography

Space Grotesk handles display text and numeric readouts because its open forms feel technical without becoming cold. Inter/system fallbacks carry Spanish body copy and controls. Monospace is reserved for elapsed time. Sentence case is used throughout.

## Layout

The shell uses a 16-column desktop grid with a persistent left rail and a content canvas. The board is a three-column layout at wide widths and becomes a stacked, readable list under 800px. Cards keep a stable minimum height and the detail panel becomes a full-width modal on small screens.

## Elevation & Depth

Hierarchy comes from ink/paper contrast, a 1px line, and one restrained shadow on the dialog. Cards do not float excessively; the active card receives a lavender inset marker.

## Shapes

Controls are softly rounded at 12px, cards at 20px, and the main modal at 28px. The orbit is the only circular container. Focus uses a 3px lavender outline with a 2px offset.

## Components

- **Buttons:** Coral filled primary actions, ink outline secondary actions, and text icon buttons for compact controls. All have stable dimensions between states.
- **Cards:** A status eyebrow, title, one-line description, step count, and explicit action. Whole cards are not clickable; the “Abrir misión” button is the target.
- **Dialog:** Native `<dialog>` owns the modal, with explicit close, Escape support, focus restoration, and a scrollable body.
- **Progress orbit:** Accessible text label plus SVG ring. The ring never carries meaning alone.
- **Motion:** 180ms ease-out for surfaces and hover; stopwatch ticks are functional. Reduced motion disables transitions and pulse.

## Do's and Don'ts

- **Do:** Keep one clear next action visible in every mission state.
- **Do:** Preserve work in local storage and tell the user when it was saved.
- **Don't:** Hide mission actions behind hover-only affordances.
- **Don't:** Use confirmation dialogs for routine reversible interactions.
