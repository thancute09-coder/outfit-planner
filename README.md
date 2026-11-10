# Twelve — family outfit planner

One shared family itinerary: each of Days 1–12 shows **Shams, Jonathan, and Ethan side by side**, with one outfit per person. The planner includes 61 tagged photos: Shams 32, Jonathan 17, and Ethan 12.

## Plan your family days

- Each day has three fixed person columns. Choose an outfit in each column to complete that family day (3/3).
- **Choose outfit** opens a photo chooser containing only that person's looks. Tap a photo to assign it. Use **Change outfit** to replace it, or clear that person's day from the chooser.
- Drag and drop works on desktop. A photo can only be dropped into its owner's column.
- Each outfit is scheduled once. Moving an already scheduled outfit onto an occupied day swaps the two outfits for that person. Other people's plans stay intact.
- The summary tracks complete family days and the 36 individual outfit slots.

## Filter and manage photos

The **Family outfit library** has a **Show photos** dropdown: All family photos, Shams, Jonathan, or Ethan. This filters only the photo library; all three people remain visible in every family day.

Each photo displays its owner and provides a **Person** dropdown, editable clothing tags, notes, and a **Wear on** day selector. Changing a photo's person clears its old day assignment and moves it into the new person's library.

To upload, choose **New photos belong to**, then upload one or several photos. Selecting a person in the photo filter also selects them as the upload recipient. You can change that recipient before uploading.

The phone layout keeps all three people side by side, with a two-column photo chooser and native selectors. Bottom navigation jumps between family days, photos, and packing. Photos are swipeable in the phone library. Use the day jump selector to move through the itinerary.

## Clothing reuse and packing

Reuse tags compare matching jacket, sweater, pants, skirt/shorts, and scarf names **within each person's plan**. The same label on another person's clothing is treated separately. Later reuse days are highlighted under the day's outfit. Expand **Clothing & reuse** for all matching days and pieces.

The family packing list groups unique scheduled pieces by person, category, and all days of use. Labels are editable and inferred from appearance; obscured pieces are left blank. New uploads need manual clothing tags.

## Website files

Publish `index.html`, `cloud-sync.js`, and `.nojekyll` in the root of `thancute09-coder/outfit-planner`. GitHub Pages deploys from `main` / root:

https://thancute09-coder.github.io/outfit-planner/

Local planning also works by opening the HTML with its companion JavaScript file in the same folder. Shared sync requires the published HTTPS site.

## Shared sync

Server: https://twelve-family-sync.thancute09.workers.dev

The private repository `thancute09-coder/outfit-planner-data` stores `family/state.json` and newly synced photos in `family/photos/`. Backend source and credential setup instructions are supplied in the downloadable package under `backend/`.

Connect both phones using **Connect shared plan**, the same server address, and the same family key. The first phone initializes the shared plan after confirmation; the other loads it. The GitHub token stays in a Worker secret and must never be placed in the HTML.

Changes save after about two seconds of inactivity. A connected, visible page checks for changes every 20 seconds. Wait for **Synced** before closing. Reconnect after refreshing or reopening; the family key stays only in memory for the open page. Profile filters are local view settings; outfit plans for all three people sync together. The original 61 photos are referenced by ID instead of being resent on each edit.

Conflicting simultaneous edits are rejected rather than silently overwriting the other phone's changes. Export a local backup, load the latest shared plan, and reapply the desired edits. There is no iOS background sync after closing the page.

## Existing plans and backups

Existing person-based day assignments are preserved and appear together in the family itinerary. The backup format and shared sync data remain compatible with the previous version. Export includes all three people and their photos; Import replaces all three after confirmation. Older single-person backups migrate to Jonathan.

Browser IndexedDB keeps local data. Before a shared plan replaces local data, a recovery copy is saved. **Recovery backup** downloads that copy. Clearing browser data removes local plans and recovery copies. Keep exported backups.

Starter collections are added once without resetting schedules. Deleted photos stay deleted after refresh. **Restore missing starter photos** adds missing looks across the family without duplicating photos whose owner was changed.

The 61 starter photos are embedded in the public website and repository. New sync uploads and shared schedules use the separate private data repository. Anyone with the family key can view and edit the whole family plan; person labels are not separate login accounts.
