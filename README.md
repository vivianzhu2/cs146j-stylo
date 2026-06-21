<div align="center">

# ✦ Stylo

**A digital‑closet and outfit social platform — style, share, and remix your wardrobe.**

[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-5-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![SQLite](https://img.shields.io/badge/SQLite-better--sqlite3-003B57?logo=sqlite&logoColor=white)](https://github.com/WiseLibs/better-sqlite3)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](#license)

</div>

---

Stylo lets users build a virtual wardrobe, compose outfits on a drag‑and‑drop
studio canvas, publish them to a shared feed, and **remix** other people's looks
into their own. It's a full‑stack web application built from scratch — no
front‑end framework — with a Node/Express API and a SQLite database, developed as
a final project for **CS 146J**.

## Key Features

- **🎨 Outfit Studio** — Drag clothing from your closet onto a canvas, then move,
  scale, rotate, and layer each piece. Shuffle a random outfit from items you own,
  and publish a rendered look in one click.
- **🖼️ Discovery Feed** — A masonry feed with **Discover** and **Following** tabs,
  filtering by aesthetic and tag, and sorting by recency or popularity. Open any
  post to view, like, and comment.
- **🔁 Remix** — Recreate any feed outfit on your own canvas with its original
  layout intact; pieces you don't own are surfaced to add to your closet or
  wishlist.
- **👗 Closet Management** — A filterable wardrobe grid (by status and category)
  with an add‑item flow including photo upload.
- **👤 Profiles & Social Graph** — Public/private profiles, follow/unfollow, profile
  editing, and follower stats. Private profiles are gated to the owner and their
  followers.

## Tech Stack

| Layer        | Technologies                                                   |
| ------------ | -------------------------------------------------------------- |
| **Frontend** | HTML5, CSS3, JavaScript (ES6+) — no framework, no build step   |
| **Backend**  | Node.js, Express 5                                             |
| **Database** | SQLite via `better-sqlite3`                                    |
| **Tooling**  | `cors`, `dotenv`                                               |
| **Assets**   | Google Fonts (Instrument Serif, Albert Sans), Material Symbols |

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) **v18 or newer**
- npm (bundled with Node.js)

### Installation

```bash
git clone https://github.com/cs146j-26sp/cs146j-stylo.git
cd cs146j-stylo
npm install
```

### Running locally

```bash
npm start
```

Open **http://localhost:3000** — the root redirects to the Studio page. On first
launch the server creates and seeds `server/stylo.db` automatically, so the app is
populated with demo content out of the box.

### Configuration (optional)

Create a `.env` file in the project root to override defaults:

```bash
PORT=3000                 # server port
DB_PATH=./server/stylo.db # SQLite database location
```

## Project Structure

```
cs146j-stylo/
├── server/
│   └── index.js              # Express server, SQLite schema, seed data, all API routes
├── frontend/
│   ├── data.js               # Shared data layer — loads user + closet, fires stylo:ready
│   ├── components.js         # Shared UI helpers — header, item cards
│   ├── styles.css            # Shared design system — colors, header, buttons, layout
│   ├── stylo-studio/         # Studio — build & remix outfits on a canvas
│   ├── stylo-feed/           # Feed — discovery grid, post modal, remix
│   ├── stylo-closet/         # Closet — wardrobe grid & add-item flow
│   └── stylo-profile/        # Profile — identity, follow, edit, privacy
├── CODEBASE_GUIDE.md         # Detailed technical documentation
└── package.json
```

## API Reference

The backend exposes a REST API under `/api`. Selected endpoints:

| Method                    | Endpoint                 | Purpose                                    |
| ------------------------- | ------------------------ | ------------------------------------------ |
| `GET`                     | `/api/outfits`           | Feed outfits (newest user posts first)     |
| `POST`                    | `/api/outfits`           | Publish an outfit (supports remixes)       |
| `GET`                     | `/api/users/:id`         | Profile info + follower/following counts   |
| `PUT`                     | `/api/users/:id`         | Edit display name, bio, and privacy        |
| `GET` · `POST`            | `/api/users/:id/items`   | Read / add wardrobe items (privacy‑gated)  |
| `GET`                     | `/api/users/:id/outfits` | A user's published outfits (privacy‑gated) |
| `GET`                     | `/api/users/:id/remixes` | A user's remixed outfits (privacy‑gated)   |
| `POST` · `DELETE`         | `/api/follow/:id`        | Follow / unfollow a user                   |
| `GET` · `POST` · `DELETE` | `/api/clothing-items`    | Manage clothing items                      |
