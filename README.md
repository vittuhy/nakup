# Nákup

A grocery list that sorts what you dictate into your store's aisles, in your own fixed order.

Static single page — no backend, no build step. The list lives in the browser's
`localStorage` on the device you use it from.

## Use

Open the page, tap **⚙** and paste an OpenAI API key. It is stored in that browser
only and is never committed here. Without a key the app still works; items just
land in *Ostatní*.

Type or dictate into the box at the bottom. Items are split, de-duplicated against
what is already on the list, and filed into a section.

## Adding from an iPhone Action button

A Shortcut, four actions:

1. `Dictate Text` — Czech, stop listening after a pause
2. `URL Encode`
3. `Text` — `https://vittuhy.github.io/nakup/?add=` + the encoded output
4. `Open URLs`

Then **Settings → Action Button → Shortcut**. The page reads `?add=` on load and
sorts straight away.

## Changing the aisles

`SECTIONS` at the top of the script in `index.html` — names and emoji, in
store-walking order. Section matching ignores case, spacing and `&` vs `a`, so
renaming one does not strand existing items.

`MODEL` on the next line sets the OpenAI model.

## Sync (optional)

Paste a GitHub token with **Gists: read and write** into the ⚙ panel. The list is
then kept in a private Gist: it survives Safari clearing its storage, and the same
list appears on any device where you paste the same token.

The gist is created on the first change. Writes are debounced; the app pulls on
launch and whenever it returns to the foreground. Last write wins — the copy with
the newer timestamp replaces the older one, so avoid editing on two devices at once.

Tapping the small sync label next to ⚙ forces a pull and push.
