# 🪔 Wedding Invite — Interactive Hindi Wedding Invitation

A single-file, mobile-first, animated digital wedding invitation in Hindi (Devanagari), with a temple-door entrance, an envelope that opens into a full-screen invitation card, a multi-event schedule carousel, venue map and background music.

No build step. No framework. One `index.html` plus your media files.

**Live demo:** https://thesurajdev.github.io/wedding-invite/

---

## ✨ Features

- **Temple door entrance**: tap the door to open it; background music starts on that first tap (browsers require a user gesture for audio).
- **Real envelope animation**: the seal lifts, the flap unfolds, the card slides out and is pulled toward the viewer until it fills the screen. Scrolling back to the top slides it back into the envelope.
- **Locked scrolling**: guests can't scroll past the first screen until they open the invitation.
- **Intro screen**: couple photo, names, date and city, with falling marigold and rose petals.
- **Event carousel**: Haldi, Mehandi, Wedding, or any events you add. Swipe, scroll, use arrow keys, dots or buttons. Each card has an **Add to Calendar** (Google Calendar) button.
- **Venue section**: embedded Google Map and a **Get Directions** button.
- **Background music**: two tracks that cross-fade as the guest moves between sections.
- **Hero video**: separate desktop and mobile clips.
- **Clear navigation hints** at every step (tap to open, swipe, scroll down).
- **Rich link previews** for WhatsApp, Facebook, Telegram, X and LinkedIn (Open Graph and Twitter Card tags).
- **Accessible**: respects `prefers-reduced-motion`, keyboard-operable door and carousel.
- **Hindi typography handled properly**: no letter-spacing on Devanagari, which would otherwise break conjuncts and matras.

---

## 📁 Project structure

```
wedding-invite/
├── index.html          # The entire site: HTML, CSS, JS and config
├── image1.jpg          # Intro / couple photo
├── og-image.jpg        # Link-preview image (1200×630)
├── desktop_arti.webm   # Hero video for desktop
├── mobile_arti.webm    # Hero video for mobile
├── ganesh_mantra.mp3   # Music for the hero screen
├── wedding_song.mp3    # Music for the rest of the page
├── README.md
└── LICENSE
```

File names are examples. You can use any names as long as `index.html` points to them.

---

## 🚀 Quick start

1. **Fork or clone** this repo.
   ```bash
   git clone https://github.com/thesurajdev/wedding-invite.git
   cd wedding-invite
   ```
2. **Edit the config** in `index.html` (see below). Everything editable is in one JSON block.
3. **Replace the media files** with your own.
4. **Preview locally**: just open `index.html`, or run a tiny server:
   ```bash
   python3 -m http.server 8000
   # then visit http://localhost:8000
   ```
5. **Deploy** (see [Deployment](#-deployment)).

---

## ⚙️ Customising

All content lives in one place, the `<script id="wedding-config" type="application/json">` block near the top of `<body>`. You don't need to touch the HTML or JavaScript to change text, dates, venue or media.

```json
{
  "couple": {
    "brideName": "पलक",
    "groomName": "सूरज",
    "coupleShort": "Palak weds Suraj"
  },
  "hosts": {
    "blessingsLine": "माता-पिता एवं समस्त परिवारजनों के आशीर्वाद से",
    "invitationNote": "सादर आमंत्रित"
  },
  "event": {
    "titleHindi": "शुभ विवाह",
    "dateDisplay": "21 November 2026, Saturday",
    "cityLine": "नई दिल्ली"
  },
  "venue": {
    "name": "Venue name",
    "city": "Full address",
    "mapQuery": "",
    "mapLink": "https://maps.app.goo.gl/xxxx",
    "parkingNote": "Valet parking available at venue"
  },
  "schedule": {
    "events": [
      {
        "title": "हल्दी समारोह",
        "titleEnglish": "HALDI CEREMONY",
        "dateDisplay": "20 नवंबर 2026, शुक्रवार",
        "dateISO": "2026-11-20T11:00:00+05:30",
        "timeDisplay": "प्रातः 11:00 बजे",
        "venueLine": "Residence, Vikaspuri"
      }
    ]
  },
  "media": {
    "introImage": "image1.jpg",
    "heroVideoDesktop": "desktop_arti.webm",
    "heroVideoMobile": "mobile_arti.webm",
    "bgMusicPrimary": "ganesh_mantra.mp3",
    "bgMusicSecondary": "wedding_song.mp3"
  },
  "footer": {
    "line": "आपका शुभ आगमन ही हमारे लिए सबसे बड़ा आशीर्वाद होगा"
  }
}
```

### Config reference

| Key | What it controls |
|---|---|
| `couple.brideName` / `groomName` | Names on the envelope card, letter and intro screen. The first letter of `brideName` appears on the wax seal. |
| `couple.coupleShort` | Short English line in the footer and link preview. |
| `hosts.blessingsLine` | Line above the invitation text on the intro screen. |
| `hosts.invitationNote` | Closing line on the intro screen. |
| `event.titleHindi` | Main title ("शुभ विवाह") used on the preloader, card and intro. |
| `event.dateDisplay` / `cityLine` | Shown on the letter and intro screen. |
| `venue.name` / `city` | Venue text under the map. |
| `venue.mapQuery` | Optional search text for the embedded map. If empty, `name + city` is used. |
| `venue.mapLink` | Link used by **Get Directions** (a Google Maps share link works well). |
| `venue.parkingNote` | Optional extra line under the address. |
| `schedule.events[]` | One carousel card per entry. Add as many as you like. |
| `events[].dateISO` | Start time with timezone offset, used by **Add to Calendar** (default duration 3 hours). |
| `media.*` | Image, video and audio paths or URLs. Leave a value empty to skip it safely. |
| `footer.line` | Closing blessing in the footer. |

### Things that live outside the config

Because social crawlers do **not** run JavaScript, these must be edited directly in `<head>`:

- `<title>` and `<meta name="description">`
- All `og:*` and `twitter:*` tags (title, description, `og:url`, `og:image`)

Use an absolute URL for `og:image` and keep the image at **1200×630**. After changing it, refresh WhatsApp's cache with a new `?v=2` query on the link, or use the [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/).

### Colours and fonts

Colours are defined in the Tailwind config at the top of the file:

```js
colors: {
  maroon:   { deep: '#3A0B12', DEFAULT: '#7A1E2B', light: '#9C2C3A' },
  marigold: { DEFAULT: '#E8961F', light: '#F4B94D' },
  brass:    { DEFAULT: '#C9A34E', light: '#F0D896', dark: '#8A6420' },
  cream: '#F6EEDD',
  ink: '#2A1810'
}
```

Fonts: **Yatra One** (headings), **Mukta** (body), **Cormorant Garamond** (italic accents), loaded from Google Fonts.

### Animation timing

The envelope sequence is controlled by the `later(...)` timers in the *"ENVELOPE ↔ LETTER"* section of the script. The card grow/shrink speed (`.9s`) is set in the `#letterCard.anim` CSS rule.

---

## 🌐 Deployment

### GitHub Pages (free)

1. Push the repo to GitHub.
2. Go to **Settings → Pages**.
3. Under **Source**, choose **Deploy from a branch**, select `main` and `/ (root)`, then **Save**.
4. Your site appears at `https://<username>.github.io/<repo>/`.
5. Update `og:url` and `og:image` in `index.html` to match.

### Other hosts

It's a static site, so it also works on Netlify, Vercel, Cloudflare Pages or any web server. Just upload the files.

---

## 🔒 Privacy: read before publishing your own

This repo is open source, which means **everything you commit is public**, including the config block, photos, video and audio.

Before you deploy your own invitation:

- **Don't put private phone numbers or home addresses** in the config or HTML. Share those in your WhatsApp message instead.
- Use only photos you're comfortable sharing publicly.
- Add `<meta name="robots" content="noindex, nofollow">` to `<head>` if you don't want search engines to list your invitation.
- Share the link privately (WhatsApp, SMS), not on public pages.

The names, dates and venue in this repo's demo are those of the original couple. **Replace them with your own** before using the template.

---

## 🎵 Media & licensing notes

- The music files in this repo may be copyrighted by their respective owners. For your own deployment, use music you have the rights to, or royalty-free tracks.
- Browsers block audio until a user interacts, so music starts when the guest taps the door.
- Keep videos small (aim for under 3–4 MB each) so the page loads quickly on mobile data. `.webm` with VP9 compresses well.

---

## 🛠️ Tech stack

- Plain **HTML, CSS and JavaScript** (no build tools)
- **Tailwind CSS** via the Play CDN, for utility classes
- **Google Fonts**: Yatra One, Mukta, Cormorant Garamond
- **Google Maps** embed and **Google Calendar** template links

> The Tailwind Play CDN is great for a single invitation page. For a high-traffic production site, you can compile Tailwind to a static CSS file instead.

## 🌍 Browser support

Works on current versions of Chrome, Edge, Safari (iOS and macOS), Firefox and Samsung Internet. It uses CSS scroll-snap, `IntersectionObserver`, `dvh` units (with a JS fallback), and CSS 3D transforms.

---

## 🧩 How it works (short tour)

| Part | Idea |
|---|---|
| **Config block** | A JSON `<script>` is parsed at load and pushed into the DOM, so content and code stay separate. |
| **Scroll lock** | Scrolling is disabled on load. It unlocks only when the letter fills the screen, and locks again when the guest returns to the envelope. |
| **Envelope → letter** | The SVG card's on-screen position is measured with `getBoundingClientRect()`. A fixed overlay card starts at exactly that rectangle and animates to full viewport size. |
| **Clean hand-off** | While the letter dissolves, the intro's text is held hidden, then released so it rises in without overlapping. |
| **Navigation hints** | A single scroll hint (also a button) is shown only where scrolling is the correct next action. The carousel section shows its own swipe hint until the last event. |
| **Music** | Two `<audio>` elements cross-fade based on which section is visible. |

---

## 🤝 Contributing

Contributions are welcome, such as new languages, themes, accessibility improvements or bug fixes.

1. Fork the repo
2. Create a branch: `git checkout -b feature/my-change`
3. Commit your changes: `git commit -m "Add my change"`
4. Push: `git push origin feature/my-change`
5. Open a Pull Request

Please keep the project dependency-free and single-file friendly.

---

## 📄 License

Released under the **MIT License**. You're free to use, modify and share this template, including for your own wedding. See the [LICENSE](LICENSE) file for details.

The couple's photos, names, personal details and any music or video in the original demo are **not** covered by the MIT license and must not be reused.

---

## 🙏 Credits

Built by [Suraj Kumar](https://github.com/thesurajdev) for the wedding of Palak and Suraj.

*॥ शुभमस्तु ॥*
