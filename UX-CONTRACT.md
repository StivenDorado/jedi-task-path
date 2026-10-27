# UX Contract

## Product context

- Audience: Spanish-speaking solo makers and students.
- Primary jobs: capture a mission, move it through a simple board, track focused time, and complete suggested steps.
- Target market(s): General web; desktop and mobile.
- Active locales: `es-CO`.
- Language/content register: clear, conversational Spanish; action labels describe the result.
- Timezone/calendar policy: browser-local date and 24-hour elapsed timer.
- Accessibility target: WCAG 2.2 AA.

## Visual contract

- Project `DESIGN.md`: `DESIGN.md`.
- Token ownership model: `DESIGN.md` owns the tokens; `styles.css` is the runtime adapter.
- Runtime design-system/token source: `:root` custom properties in `styles.css`.
- Supported themes: light paper canvas with ink shell.

## Canonical UI Map

| Capability | Canonical owner | Source of truth | Allowed variants | Verification |
|---|---|---|---|---|
| Form | Native labeled form + `validateMissionForm` | This contract | create / edit | submit + inline errors |
| Scrollbar | Global application stylesheet | DESIGN.md | default | computed style |
| Dialog | Native `<dialog>` | This contract | detail / create | Escape + focus |
| CRUD | `MissionStore` | localStorage | create / update / delete | full-flow browser check |
| Select/Listbox | Native select | This contract | native | keyboard + native popup |
| Date | Native date input | This contract | native | locale + keyboard |

## Component behavior

| Component | Default | Hover | Focus | Active | Disabled | Busy | Error |
|---|---|---|---|---|---|---|---|
| Button | clear label | tonal lift | visible outline | pressed | reduced contrast | stable width | inline error nearby |
| Input | labeled, bordered | lavender border | visible outline | n/a | muted | n/a | message + `aria-invalid` |
| Dialog | centered, modal | n/a | first action | n/a | n/a | n/a | persistent inline message |

## Dataset navigation

- Exploratory list: mission board with search and status filters.
- URL state: not persisted; local state is sufficient for this single-screen MVP.
- Empty/no-results: explain the next action and offer “Nueva misión”.
- Back/scroll restoration: close restores the trigger button focus.

## Flow ledger

| Operation | Trigger | Pending | Success destination | Success feedback | Failure recovery | Focus outcome |
|---|---|---|---|---|---|---|
| Create | Nueva misión / form submit | button stable | board + new card | toast + saved status | inline validation | new card action |
| Edit | modal save | button stable | same modal | toast | inline message | save button |
| Delete | modal delete | button stable | board | toast | item remains if storage fails | board heading |
| Search | input | immediate local filter | filtered board | result count | clear search | search input |
| Timer | start/pause | active readout | same modal/card | status text | recover from stored start time | timer button |

## Navigation and responsive behavior

- Route document title: `Mission Control — Tus misiones`.
- Sidebar transforms into a compact top bar on narrow screens.
- Board columns stack vertically under 800px.
- Modal fits the visual viewport and its body scrolls internally.
- Sticky header never covers focused content.

## Overlays and feedback

- Dialog primitive: native modal `<dialog>`.
- Toast placement: bottom-right desktop, bottom-center mobile; polite live region; 3.2s duration.
- Layer order: dialog > toast > app content.

## Async and resilience

- Mutation default: local synchronous update with storage write.
- Duplicate submit: disabled while saving, with stable button geometry.
- Offline: local data remains usable; storage failure produces a visible error toast.
- Timer state: elapsed seconds are derived from stored `startedAt` so reload does not reset an active timer.

## Validation

- Native fields are labeled; `novalidate` is used so errors stay in the product UI.
- Required title shows inline guidance and first-invalid focus.

## Verification

- Static audit: `python .../audit_project.py . --mode strict`.
- Browser matrix: desktop 1440px, mobile 390px, keyboard modal flow, reload persistence, reduced motion.
