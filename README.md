# Twelve — family outfit planner

Outfit libraries, editable clothing tags, 12-day itineraries, and packing lists for Shams, Jonathan, and Ethan. Jonathan's original 17 outfit photos are included. Shams and Ethan start empty. The phone layout includes swipeable outfit cards, native day selectors, and bottom navigation.

## Website files

Publish **both** `index.html` and `cloud-sync.js` in the root of `thancute09-coder/outfit-planner`. GitHub Pages deploys from `main` / root. The website URL is:

https://thancute09-coder.github.io/outfit-planner/

Local planning works when the files are opened directly. Shared sync requires the published HTTPS website; file URLs are intentionally not allowed by the backend.

## Shared sync

The Cloudflare endpoint is:

https://twelve-family-sync.thancute09.workers.dev

The separate private repository `thancute09-coder/outfit-planner-data` stores shared metadata in `family/state.json` and newly uploaded photos in `family/photos/`. Backend setup is documented in `backend/SETUP.md`. Sync remains unavailable until the two Worker secrets are configured.

On your first phone:

1. Open the published website and choose **Connect shared plan**.
2. Use the default server address and enter your family sync key.
3. If the server is empty, confirm publishing this device's three profiles as the family plan.
4. Wait for **Synced** before closing the page.

On the other phone:

1. Open the same website, choose **Connect shared plan**, and enter the same family key.
2. Confirm loading the shared plan.

Changes save after about two seconds of inactivity. A connected, visible page checks for changes about every 20 seconds. Keep it open until it says Synced; closing Safari before sync finishes can leave edits only on that device. The family key stays in memory for the open page; reconnect after a refresh or reopening. Profile selection stays specific to each phone, while the three people's plans are shared.

The initial 17 photos are already in the HTML and are referenced by ID during sync. Only new photos are uploaded once; subsequent schedule edits transfer small JSON updates. GitHub records saved versions as commits. New sync photos are limited to 4 MB after browser resizing; plans support up to 300 outfits per person and a 512 KB metadata request.

If both phones edit at once, the later save can report a conflict. Local edits stay intact. Export a backup, then choose **Load shared plan** and reapply the desired edits. The app does not silently overwrite the other phone's save or automatically merge conflicts.

## Backups and local storage

Browser IndexedDB keeps this device's plan. Export backup includes all three profiles and photos. Import replaces all three after confirmation; older backups migrate to Jonathan. Before a shared plan replaces local data, a recovery copy is stored locally. **Recovery backup** downloads the most recent copy; use Import backup to restore it. Clearing browser data removes both the local plan and that recovery copy.

Disconnecting stops sharing and clears the family key from memory. It does not delete shared GitHub data. Anyone with the family key can read and edit all three profiles; these are not separate login accounts.

The 17 starter photos are embedded in the public website and repository. Newly synced photos and schedule data go into the separate private repository. Clothing matches are inferred from appearance and editable. Tags on new uploads are entered manually.

## Development

No frontend installation or build is needed. The backend is a Cloudflare Worker ES module in `backend/worker.mjs`, configured by `backend/wrangler.jsonc`. Secrets must never be committed. Uploading the backend source files to GitHub Pages does not run them; the Worker must be deployed separately.
