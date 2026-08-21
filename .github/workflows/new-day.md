---
description: Adds today's UTC date to the Daily Updates navigation in index.html, with a matching dialog confirming the daily update ran.
engine: copilot
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
safe-outputs:
  create-pull-request:
    title-prefix: "[new-day] "
    allowed-files:
      - "index.html"
---

# New Day

## Task

Add today's UTC date as a new Daily Update entry in `index.html`, following the existing structure exactly.

## Steps

1. Compute today's date in UTC from the workflow run (do not use local time). Format it exactly like the existing entries, e.g. "1st of August" (ordinal day + "of" + full month name, no year, no leading zero).
2. Open `index.html` and inspect the existing `daily-updates-nav` list and the existing `<dialog class="daily-update-dialog">` elements to learn the exact structure, ID conventions, wording, and styling patterns already in use (e.g. `id="august-1-dialog"`, `aria-controls`, `data-dialog-trigger`, `aria-labelledby`/`aria-describedby` pairing with `<h2>`/`<p>` ids).
3. **Check for an existing entry for today's UTC date first.** If a navigation item, dialog, or date text matching today's UTC date already exists anywhere in `index.html`, make **no changes** to the file at all — do not create a pull request.
4. If today's date is not yet present:
   - Add exactly one new `<li>` item to the `daily-updates-list` `<ul>` containing a `daily-update-trigger` button, following the same markup, attributes, and ID naming convention as the existing entries (derive the id from the month and day, e.g. a date of August 5th would use ids following the `august-5-...` pattern seen in the existing markup).
   - Add exactly one new matching `<dialog class="daily-update-dialog">` element (placed alongside the existing dialogs, before the closing `</body>`/script), with an `id`, `aria-labelledby`, and `aria-describedby` that follow the same naming convention, and with the same header/close-button structure as existing dialogs.
   - The dialog heading and body must confirm that the daily update automation ran successfully for today's UTC date — keep the tone and structure consistent with the existing dialog(s), but do not copy their specific wording verbatim; write new content confirming this specific day's automated update completed.
   - Do not remove, rename, renumber, or otherwise modify any existing Daily Update navigation entries or dialogs — every prior daily update must remain exactly as it was.
   - Do not create duplicate ids, duplicate navigation entries, or duplicate dialogs.
5. Do not modify `styles.css` or any file other than `index.html`.
6. Only create a pull request if you actually added a new Daily Update entry. If today's date was already present, exit without creating a pull request (no-op).

## Output

Use the `create-pull-request` safe output to propose the change to `index.html` only, if and only if a new entry was added.
