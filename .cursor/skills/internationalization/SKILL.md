---
name: internationalization
description: Prepare UI and content for multiple locales—string externalization, plurals, dates, and RTL. Use when adding translations or fixing i18n bugs.
---

# Internationalization (i18n)

## When to Use

- Adding or changing user-visible strings in apps
- Formatting dates, numbers, or currencies for users
- Supporting RTL languages or locale-aware sorting

## Instructions

1. **Externalize strings.** No user-facing literals embedded in logic without a message catalog; include context for translators (`button.save`, `error.network_timeout`).
2. **Plurals and gender.** Use ICU message format or framework equivalents; avoid concatenating translated fragments that break grammar in other languages.
3. **Dates and numbers.** Use locale-aware formatting APIs; store UTC in backends; display in user timezone when appropriate.
4. **Layout.** Avoid fixed widths for translated text; support RTL with logical CSS properties (`margin-inline`, `text-align: start`).
5. **Testing.** Pseudo-locale or longest-language smoke tests to catch truncation and layout breaks.

## Checklist

- [ ] Strings are complete sentences or phrases, not arbitrary splits
- [ ] Sorting and collation use locale rules when product requires it
