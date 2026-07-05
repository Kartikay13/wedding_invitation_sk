# Kartikay & Shivani — Wedding Invitation Website

A single-page, mobile-first wedding invitation with a tap-to-open door animation,
background music, live countdown, event timeline, Google Maps buttons for both
venues, and a photo gallery. No app, database, or server needed — it's one HTML
file you can open directly or host for free.

---

## 1. One assumption worth double-checking

You'd earlier said Shivani's father is Ramesh Sharma, with her mother's name
still pending. Your latest message gave "D/O Dinesh Kumar Sharma and Geeta
Devi" as the format example — I've taken that as the actual names and used
it on the invitation (replacing Ramesh Sharma). If that was just an example
of the S/O · D/O style rather than her real parents' names, open
`index.html`, search for `WEDDING`, and fix this line:

```js
bride: { name: "Shivani", relation: "D/O Dinesh Kumar Sharma &amp; Geeta Devi" },
```

---

## 2. Everything else you can personalize

Near the top of the `<script>` tag at the bottom of `index.html`, there's a
single `WEDDING = { ... }` object with **all** the editable content:
names and relation lines (the `groom` / `bride` objects — each has a `name`
and a `relation` like `"S/O Suresh Kumar Sharma & Rajo Devi Sharma"`), the
countdown date/time, calendar details, both venue addresses, the event
schedule, and the list of gallery photo filenames. You should not need to
touch any HTML or CSS to make changes — just edit values inside that
object and save.

---

## 3. Adding your photos

Drop your images into the `assets/photos/` folder using these exact filenames
(the page is already wired to look for them — nothing else to configure):

| Filename                | Used for                          |
|-------------------------|------------------------------------|
| `engagement.jpg`        | "Our Story" — left photo (portrait frame) |
| `couple.jpg`            | "Our Story" — right photo (landscape frame) |
| `family-groom.jpg`      | "Our Families" — Kartikay with his parents (landscape frame) |
| `family-bride.jpg`      | "Our Families" — Shivani's family (landscape frame) |
| `photo1.jpg` … `photo5.jpg` | Gallery (portrait frames) |
| `photo6.jpg`            | Gallery (landscape frame) |
| `hero-share.jpg`        | Thumbnail shown when the link is shared on WhatsApp/social media — see note below |

**About frame shapes:** each slot has a "portrait" or "landscape" frame that
matches the real dimensions you gave me, so photos display in full without
odd cropping. If you swap in a photo with a different orientation, open
`index.html`, find the `storyPhotos` / `familyPhotos` / `galleryPhotos`
arrays near the top of the `<script>`, and change that photo's
`orientation` to `"portrait"` or `"landscape"` to match.

Until you add a photo, that slot shows a neat placeholder frame with the
expected filename, so the page still looks complete.

To use different filenames or add more gallery photos, edit the
`galleryPhotos` array in the `WEDDING` object.

---

## 4. Adding music

Add one MP3 file named `music.mp3` inside `assets/music/`. The site will
play it the moment a guest taps to open the invitation (this also satisfies
phone browsers' "no autoplay without a tap" rule), and there's a floating
button in the corner to mute/unmute afterwards.

**A note on the track itself:** avoid using a copyrighted Bollywood/film
track directly, since publishing it on a public website can trigger a
copyright claim. Safer options that still sound right for this:
- An instrumental shehnai/santoor track from a royalty-free library like
  Pixabay Music or YouTube Audio Library (both free, no attribution
  headaches)
- A soft instrumental cover of a song you like, if you can find a
  royalty-free version
- Or, several inexpensive Indian wedding invitation music packs (labeled
  "royalty-free" or "commercial use") are sold on stock-audio sites

---

## 5. Hosting it as a real link

### Option A — GitHub Pages (free, recommended, permanent link)
1. Create a free GitHub account if you don't have one, and create a new
   repository (e.g. `kartikay-shivani-wedding`) — make it **Public**.
2. Upload the entire contents of this folder (`index.html`, the `assets`
   folder with your photos/music, `README.md`) into that repository —
   either drag-and-drop on github.com, or via git.
3. In the repository, go to **Settings → Pages**, set the source branch to
   `main` and folder to `/ (root)`, then save.
4. After a minute, your live link appears at:
   `https://<your-username>.github.io/kartikay-shivani-wedding/`
5. Share that link on WhatsApp, Instagram, or wherever you like.

### Option B — Netlify (free, drag-and-drop, fastest to set up)
1. Go to app.netlify.com, sign up free.
2. Drag this whole folder onto the "Deploy manually" area.
3. Netlify gives you an instant live link (you can rename the subdomain in
   site settings, e.g. `kartikay-and-shivani.netlify.app`).

### Option C — Vercel
Similar to Netlify — sign up, drag-and-drop the folder or connect the GitHub
repo from Option A, and it deploys automatically.

### Custom domain (optional)
If you'd like something like `kartikayweds shivani.com`, buy a domain from
Namecheap or GoDaddy (~₹700–1200/year) and point it at whichever host you
picked above — each has a simple "Add custom domain" option in settings.

---

## 6. Getting the link preview thumbnail to show up

Two things were causing the missing thumbnail:

1. **The link you shared was the GitHub *settings* page, not your live
   site.** `.../settings/pages` is only visible to you when logged into
   GitHub — it's not the public invitation. Open that same Settings → Pages
   screen and look for a green box that says "Your site is live at
   `https://kartikay13.github.io/wedding_invitation_ks/`" — **that** green
   link is the one to share with guests.
2. **The preview image needs to be small.** I've pointed `og:image` at
   `https://kartikay13.github.io/wedding_invitation_ks/assets/photos/hero-share.jpg`
   in `index.html` (double-check that matches your actual repo name/username
   exactly, capitalization included, and fix it there if not). But your
   `hero-share.jpg` is a 6000×4000 original — most likely several MB —
   and WhatsApp's crawler often times out or refuses images that large.
   **Resize it to roughly 1200×800px and compress it to under ~300KB**
   (any free tool like squoosh.app or tinypng.com works) before re-uploading.

WhatsApp also **caches link previews aggressively** per URL. After fixing
the image, sending the exact same link again may still show the old
(missing) preview for a while. To force a fresh check: paste the link into
Facebook's Sharing Debugger at `developers.facebook.com/tools/debug/` and
click "Scrape Again," or simply share the link in a chat that's never seen
it before.

---

## 7. Testing before you share it

Just double-click `index.html` to open it in any browser first — everything
except the music (browsers block local-file audio playback in some cases)
will work exactly as it will once hosted. Once it's uploaded to GitHub
Pages/Netlify/Vercel, test the real link on an actual phone (both an
iPhone and an Android if you can) before sending it to guests.
