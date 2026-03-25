---
name: frontend-accessibility
description: Improve web accessibility—semantics, keyboard use, focus, ARIA, color, and motion. Use when building or reviewing UI components and pages.
---

# Frontend accessibility (a11y)

## When to Use

- Building forms, dialogs, navigation, or data tables
- Reviewing UI for WCAG-oriented issues
- Fixing keyboard traps or screen reader problems

## Instructions

1. **Semantic HTML first.** Use native elements (`button`, `a`, `label`, `input`) before ARIA. ARIA supplements, not replaces, semantics.
2. **Keyboard.** All interactive controls reachable via Tab; visible focus styles; Escape closes modals/menus when expected; no keyboard traps.
3. **Forms.** Associate labels with controls; describe errors in text near the field and link with `aria-describedby` when using ARIA.
4. **Images and icons.** Meaningful `alt` text; decorative images use empty alt. Icon-only buttons need accessible names.
5. **Color and contrast.** Do not rely on color alone for state; meet contrast for text and interactive elements (aim for WCAG AA unless specified).
6. **Motion.** Respect `prefers-reduced-motion` for non-essential animation.

## Quick checks

- [ ] Can complete primary flows with keyboard only
- [ ] Focus order matches visual order
- [ ] Dynamic regions announce important updates without overwhelming chatter
