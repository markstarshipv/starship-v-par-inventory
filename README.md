# Starship V Par Inventory (hosted)

Weekly inventory counts for Starship V. 64 items in six categories, each with a
par level, a reorder point, and a preferred vendor (Sam's Club, Walmart,
Amazon). Count from any phone with the shared sign-in. The Order Report lists
everything below par, grouped by vendor, with REORDER flags for items at or
below their reorder point, plus Copy lists, a Received restock button per
vendor, and PDF / Excel downloads.

## Deploy on Render (Blueprint)

1. Push this repository to GitHub.
2. In Render: New + > Blueprint > connect this repository. Render reads
   render.yaml and proposes one web service (Starter) and one Postgres
   database (Basic 256 MB). Apply.
3. When prompted for APP_PASSWORD, set the shared sign-in password that Mark
   and Kori will use. REPORT_TOKEN is generated automatically; it protects
   the read-only report feed used by the Monday email job.
4. First boot seeds the 64 items automatically when the items table is empty.

## Local run

    npm install
    node server.js          # http://localhost:8080, no password, file store

Set DATABASE_URL to use Postgres instead of the local file store.

## How counts work

- REORDER: counted at or below the reorder point. Order now.
- TOP UP (shown as "Below par" in the report): below par but above the
  reorder point. Order back to par when convenient.
- Start new count clears all counts for the next weekly count.
- Received: restock sets that vendor's below-par items back to par.
