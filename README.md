# instantsearch.js: the first write after a popstate that leaves the search unchanged is skipped

A plain page with `instantsearch.js` 4.118.1 from jsDelivr, `routing: true`, and Algolia's public demo index.

Live: https://franknoel.github.io/instantsearch-popstate-repro/

1. Click "Go to #details". The URL ends in `#details`.
2. Press Back. The URL has no query string.
3. Click page 2. The hits are page 2, and the URL still has no query string.
4. Click page 3. The URL has `?instant_search[page]=3`.

Without steps 1 and 2, page 2 is written to the URL.

The history router's `_onPopState` sets `inPopState`, and only a write clears it. A step back that leaves the search as it was brings no write, so the next change is the write that gets skipped.
