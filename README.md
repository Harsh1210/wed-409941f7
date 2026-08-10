# The Pork Bun Investigation — Round Two

An interactive date invite for Erica, plus printable tickets.
Date: Wednesday 12 August, 5:30 PM · NoMa–Gallaudet U → H Street NE, Washington DC.

## What's in here

    index.html                     The invite. Single file, no build step, no dependencies.
    tickets/tickets.html           Ticket source. Fonts are embedded as base64 — works offline.
    tickets/pork-bun-tickets.pdf   The printable output. Letter size, two tickets.

## Hosting

`index.html` is fully self-contained. Any static host will do:

    npx serve .                          # local preview
    python3 -m http.server 8000          # local preview

For a real URL, drop the folder into Netlify, Vercel, Cloudflare Pages, or
GitHub Pages. No configuration needed — `index.html` is the entry point.

The only external request is a Google Fonts stylesheet (Fraunces + Archivo).
If you want it working with no network at all, download those two families
and swap the `<link>` for a local `@font-face` block. The tickets file already
does this if you need a reference.

## Editing

Everything editable lives in one place — the `CONFIG` object at the top of
the `<script>` in `index.html`:

    herName   Set to "Erica" to personalise the headline. Blank = no name.
    dateLine  The date shown under the itinerary heading.
    roundOne  Chinatown's score from the first hunt. Feeds the final scoreboard.

The six stops are the `STOPS` array directly below `CONFIG`. Each entry takes
a time, name, address, one or more note paragraphs, the label for its button,
and `rate: true` if that stop should ask for a 1–5 score.

## How it behaves

The opening screen shows the full plan. The "I can't" button dodges three
times while "Yes" grows, then gives in. After that, stops unlock one at a
time along a vertical rail. The three bun stops require a score before you can
move on, and the final screen ranks all four contenders — the three new ones
plus Chinatown from round one.

Progress and scores are saved: to the artifact store inside Claude, and to
localStorage when hosted. She can close it mid-crawl and pick up where she
left off. "Start the hunt over" clears everything.

You can go back at any point — the Back button on each stop, tapping any
finished stop, "Back to the plan" at the top, or "Change a score" on the
final screen. Scores survive going backwards.

## Printing the tickets

Letter size. Print at 100%, not "fit to page", or the cut lines drift.
Turn on background graphics or the navy and yellow will drop out.
Cardstock if you have it — the stub has to survive a pocket.

To change the names, edit the two `ticket(...)` calls in `tickets/tickets.html`
and re-render with any headless browser, or just print the HTML to PDF.
