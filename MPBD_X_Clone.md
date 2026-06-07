# Master Project Blueprint Document (MPBD)
## X / Twitter UI Clone — HTML + Tailwind CSS

---

## SECTION 1 — EXECUTIVE SUMMARY

**Product Name:** X Clone (Home Feed UI)

**One-Line Vision:** A pixel-faithful, fully responsive static recreation of X (formerly Twitter)'s home feed, built purely with HTML and Tailwind CSS — no frameworks, no backend.

**What This Is:**
A frontend-only UI project that replicates the look and feel of X's home feed across all screen sizes. It is a learning/portfolio project demonstrating responsive layout design, Tailwind CSS utility-first styling, and mobile-app-like interface patterns using only HTML.

**Tech Used:**
- HTML5
- Tailwind CSS (via CDN `cdn.tailwindcss.com`)
- Google Material Symbols (icon font via Google CDN)
- No JavaScript, no backend, no build step (CDN-based Tailwind)

**Design Inspiration:** X.com (Twitter) — dark mode, three-column desktop layout, icon-only sidebar on tablet, bottom navigation bar on mobile.

---

## SECTION 2 — PRODUCT REQUIREMENTS (UI Scope Only)

### What the Application Does

This is a static HTML page rendering the X home feed UI. It has three structural zones — a left navigation sidebar, a central post feed, and a right trends/follow panel — which reorganize and collapse across breakpoints to match native X behavior on every device.

### What It Does NOT Do

- No authentication / login
- No real data or API calls
- No JavaScript interactions (likes, retweets, posts do not function)
- No routing or multiple pages
- No backend, database, or server

---

### UI Feature Breakdown

#### Left Sidebar Navigation
- **Description:** Vertical nav with X logo, 11 nav items (Home, Explore, Gork, Notifications, Follow, Lists, Bookmarks, Communities, Premium, Profile, More), a Post button, and a user profile row at the bottom.
- **Desktop (lg):** Full-width (275px), icon + label, sticky positioning within the centered max-width container.
- **Tablet (md):** Icon-only (72px), fixed to the left of the viewport.
- **Mobile (sm):** Hidden entirely. Replaced by bottom nav bar.
- **Priority:** Must Have

#### Mobile Top Header
- **Description:** Fixed top bar visible only on mobile. Contains user avatar (left), X logo (center), Subscribe button (right). Mimics the native X mobile app header.
- **Priority:** Must Have

#### Feed Tabs (For You / Following)
- **Description:** Two sticky tab headers at the top of the feed. Active tab (`For You`) has a blue `2px` bottom border. Settings icon visible on tablet/desktop.
- **Priority:** Must Have

#### Post Composer
- **Description:** Tweet input area with profile avatar, placeholder text "What is happening?!", media action buttons (image, GIF, poll, emoji, schedule, location), an "Everyone can reply" label, and a blue Post button.
- **Priority:** Must Have

#### Show Posts Bar
- **Description:** A clickable banner ("Show 321 posts") between the composer and the feed — matches the X UI pattern for new post notifications.
- **Priority:** Should Have

#### Post Cards
- **Description:** Each post card has an avatar, display name, @handle + timestamp, post text, a post image (rounded-xl), and a row of 5 action buttons: Comment, Retweet, Like, Views, Share. Hover states change icon colors (blue, green, pink).
- **3 static posts included:**
  - "Living legend" with image
  - Shreyas Iyer / IPL post with image
  - "Gm folks ☀️" with image
- **Priority:** Must Have

#### Right Sidebar — What's Happening
- **Description:** Trending section with 4 items (each showing region label, hashtag, post count). Visible only on desktop (lg+).
- **Priority:** Should Have

#### Right Sidebar — Who to Follow
- **Description:** Follow suggestions with avatar initial placeholder, display name, handle, and Follow button. Visible only on desktop (lg+).
- **Priority:** Should Have

#### Mobile Bottom Navigation Bar
- **Description:** Fixed bottom bar visible only on mobile. 5 icon buttons: Home, Search, Grok, Notifications, Messages. Matches native X app nav.
- **Priority:** Must Have

#### Mobile FAB (Floating Action Button)
- **Description:** Blue circular `+` button fixed above the bottom nav on mobile. Serves as the Post action on mobile.
- **Priority:** Must Have

---

## SECTION 3 — TECHNICAL SPECIFICATION

### Tech Stack

| Technology | Choice | Why |
|---|---|---|
| Markup | HTML5 | Static, no framework needed |
| Styling | Tailwind CSS (CDN) | Utility-first, rapid development, no build config |
| Icons | Google Material Symbols | Free, comprehensive, matches X icon vocabulary |
| Fonts | System default (no custom font set) | Keeps it lightweight |
| Build Tool | None | Tailwind loaded via `<script src="https://cdn.tailwindcss.com">` |
| Package Manager | npm (for local Tailwind script if needed) | `package.json` with a build script |

### Note on Tailwind Setup

This project uses the **CDN version** of Tailwind — no `tailwind.config.js`, no PostCSS, no purge step. The CDN version includes all utilities and is ideal for prototyping. If moving to production, switch to the CLI installation to enable tree-shaking and reduce CSS payload.

```json
// package.json (if using CLI build)
{
  "scripts": {
    "build": "tailwindcss -i ./src/input.css -o ./src/output.css --watch"
  },
  "devDependencies": {
    "tailwindcss": "^3.x"
  }
}
```

---

## SECTION 4 — PROJECT FOLDER STRUCTURE

```
x-clone/
│
├── index.html              # Main and only HTML file — entire UI lives here
├── package.json            # npm scripts for Tailwind CLI build (optional)
│
├── src/
│   ├── input.css           # Tailwind directives (@tailwind base/components/utilities)
│   └── output.css          # Compiled Tailwind CSS (generated by CLI build script)
│
└── README.md               # Project overview and setup instructions
```

**Why so flat?** This is a single-page static project. There are no components, routes, or modules — everything is in `index.html`. The `src/` folder only exists if you switch from CDN to the CLI build approach.

---

## SECTION 5 — FRONTEND SPECIFICATION

### Design System

#### Color Palette

All colors are sourced from Tailwind's default palette plus one custom brand color.

| Role | Color | Hex | Tailwind Class |
|---|---|---|---|
| Background | Pure Black | `#000000` | `bg-black` |
| Surface / Cards | Dark Zinc | `#18181b` | `bg-zinc-900` |
| Surface Hover | Darker Zinc | `#27272a` | `hover:bg-zinc-800` |
| Post Hover | Near Black | `#09090b` | `hover:bg-zinc-950` |
| Borders | Zinc | `#3f3f46` | `border-zinc-800` |
| Primary Brand (X Blue) | Twitter Blue | `#1d9bf0` | custom / `text-[#1d9bf0]` |
| Primary Brand Hover | Darker Blue | `#1a8cd8` | custom / `hover:bg-[#1a8cd8]` |
| Text Primary | White | `#ffffff` | `text-white` |
| Text Secondary | Gray | `#6b7280` | `text-gray-500` |
| Text Muted | Light Gray | `#9ca3af` | `text-gray-400` |
| Icon Hover — Comment | Blue | `#60a5fa` | `hover:text-blue-400` |
| Icon Hover — Retweet | Green | `#4ade80` | `hover:text-green-400` |
| Icon Hover — Like | Pink | `#f472b6` | `hover:text-pink-400` |
| Active Tab Underline | X Blue | `#1d9bf0` | custom `.tab-active` class |

#### Custom CSS Classes (Non-Tailwind)

```css
/* Active tab underline — applied to "For You" tab */
.tab-active {
  border-bottom: 2px solid #1d9bf0;
}

/* Mobile bottom nav safe area for notched phones */
.bottom-nav {
  padding-bottom: env(safe-area-inset-bottom);
}

/* Smooth momentum scrolling on iOS */
body {
  -webkit-overflow-scrolling: touch;
}
```

---

### Typography

No custom font is imported. The project inherits the system font stack from Tailwind's base styles (`ui-sans-serif, system-ui, sans-serif`).

| Usage | Class |
|---|---|
| Nav labels | `text-xl font-bold` |
| Username | `text-sm font-bold` |
| Handle / timestamp | `text-sm text-gray-500` |
| Post body text | `text-sm text-white` |
| Section headings (sidebar) | `text-xl font-bold` |
| Trend hashtags | `text-sm font-bold` |
| Trend meta (region/count) | `text-xs text-gray-400` |
| Post button | `text-sm font-bold` |
| Tab labels | `text-base font-bold` |

---

### Spacing & Layout System

Tailwind's default 4px base unit is used throughout. No custom spacing values are added.

#### Breakpoints (Tailwind Defaults)

| Prefix | Min Width | Layout Behavior |
|---|---|---|
| *(none)* | 0px | Mobile — full width feed, top header, bottom nav, FAB |
| `md:` | 768px | Tablet — icon-only sidebar (72px fixed), no bottom nav |
| `lg:` | 1024px | Desktop — full sidebar (275px sticky), right panel visible |

#### Desktop Centering

```html
<div class="flex min-h-screen relative lg:max-w-[1280px] lg:mx-auto">
```

The entire layout is capped at `1280px` and centered with `mx-auto` on desktop, leaving equal empty gutters on both sides. On tablet and mobile the layout is full-width.

#### Column Widths

| Column | Width |
|---|---|
| Left sidebar (tablet) | `72px` fixed |
| Left sidebar (desktop) | `275px` sticky |
| Feed (desktop) | `max-w-[600px]` |
| Right sidebar | `350px` fixed-width |

---

### Responsive Design Rules

#### Mobile (< 768px)

- Left sidebar: `hidden`
- Top bar: fixed, `bg-black/90`, `backdrop-blur-md`, avatar + logo + Subscribe button
- Feed: full viewport width
- Bottom nav: fixed, 5 icons (Home, Search, Grok, Notifications, Messages)
- FAB Post button: fixed `bottom-20 right-4`, blue circle with `+` icon
- Feed content pushed down with `mt-[52px]` to clear the fixed header
- Feed bottom padded with `h-20` to clear the fixed bottom nav

#### Tablet (768px–1023px)

- Left sidebar: `fixed`, `w-[72px]`, icon-only (labels `hidden lg:block`)
- Main content: offset with `md:ml-[72px]`
- Right sidebar: hidden
- Bottom nav: hidden
- Top mobile header: hidden

#### Desktop (≥ 1024px)

- Left sidebar: `sticky`, `w-[275px]`, icons + text labels shown
- Entire layout wrapper: `max-w-[1280px] mx-auto` (centered)
- Feed: `max-w-[600px]` with `border-x border-zinc-800`
- Right sidebar: visible, `w-[350px]`, contains search, trends, follow suggestions
- Sidebar offset: `lg:ml-0` (sidebar is in-flow, not fixed)

---

### Component Reference

#### Post Card

```
[Avatar 40px circle]  [Name + Handle + Timestamp]
                      [Post text]
                      [Post image — rounded-xl, max-h-80, w-full]
                      [Actions: Comment | Retweet | Like | Views | Share]
```

Action icon hover behavior:
- Comment → `hover:text-blue-400` + `group-hover:bg-blue-950` ring
- Retweet → `hover:text-green-400` + `group-hover:bg-green-950` ring
- Like → `hover:text-pink-400` + `group-hover:bg-pink-950` ring
- Views / Share → `hover:text-blue-400` + `group-hover:bg-blue-950` ring

All transitions use `transition-colors` for smooth 150ms color change.

#### Nav Item (Sidebar)

```
[Material Symbol Icon]  [Label — hidden on tablet, shown on desktop]
```

Hover: `hover:bg-zinc-900 rounded-full` pill effect.
Width: `w-fit` so the hover pill only wraps the content.

#### Post Button (Sidebar)

- Desktop: full-width rounded pill `bg-[#1d9bf0]`, text "Post"
- Tablet: icon-only circle button with `add` icon

#### Bottom Nav Bar (Mobile)

- 5 equal-width buttons using `justify-around`
- Active: `text-white`, Inactive: `text-gray-500`
- Hover: `hover:text-[#1d9bf0]`
- Background: `bg-black border-t border-zinc-800`

#### Follow Button (Who to Follow)

- Style: `border border-white rounded-full text-white text-xs font-bold px-4 py-1.5`
- Hover: `hover:bg-zinc-700`

#### Search Bar (Right Sidebar)

```
[search icon]  [input placeholder="Search"]
```

Container: `bg-zinc-900 rounded-full px-4 py-2`

---

## SECTION 6 — LAYOUT ARCHITECTURE

### HTML Structure Overview

```
<body>
  └── Layout Wrapper (flex, max-w-[1280px] on lg, mx-auto)
      ├── Left Sidebar (hidden on mobile, icon-only on tablet, full on desktop)
      ├── Mobile Header (visible on mobile only, fixed top)
      └── Main Content Area (flex-1)
          ├── Feed Column (.second)
          │   ├── For You / Following Tabs (sticky)
          │   ├── Post Composer
          │   ├── Show Posts Bar
          │   └── Post Cards (3 static posts)
          └── Right Sidebar (.third) — desktop only
              ├── Search Input
              ├── What's Happening (trending topics)
              └── Who to Follow

  <!-- Outside the wrapper, fixed-positioned mobile elements -->
  ├── Mobile Bottom Nav Bar
  └── Mobile FAB (Post button)
```

### Z-Index Layers

| Element | z-index | Class |
|---|---|---|
| Mobile bottom nav | 50 | `z-50` |
| Mobile FAB | 50 | `z-50` |
| Mobile top header | 50 | `z-50` |
| Left sidebar (tablet fixed) | 40 | `z-40` |
| Feed tabs (sticky) | 40 | `z-40` |

---

## SECTION 7 — ICONS

All icons use **Google Material Symbols Outlined** loaded via:

```html
<link rel="stylesheet"
  href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0" />
```

Usage pattern:
```html
<span class="material-symbols-outlined">home</span>
```

### Icon Map

| Feature | Icon Name |
|---|---|
| Home | `home` |
| Search / Explore | `search` |
| Grok | `smart_toy` |
| Notifications | `notifications` |
| Follow | `person_add` |
| Lists | `list` |
| Bookmarks | `bookmark` |
| Communities | `groups` |
| Premium | `workspace_premium` |
| Profile | `account_circle` |
| More | `more_horiz` |
| Post (FAB) | `add` |
| Settings | `settings` |
| Globe (reply scope) | `public` |
| Comment | `chat_bubble` |
| Retweet | `repeat` |
| Like | `favorite` |
| Views | `bar_chart` |
| Share | `share` |
| Image (composer) | `image` |
| GIF (composer) | `gif_box` |
| Poll (composer) | `bar_chart` |
| Emoji | `sentiment_satisfied` |
| Schedule | `schedule` |
| Location | `location_on` |
| Messages (bottom nav) | `mail` |

---

## SECTION 8 — KNOWN LIMITATIONS & FUTURE IMPROVEMENTS

### Current Limitations (Static-Only Scope)

| Limitation | Notes |
|---|---|
| No interactivity | Like, retweet, post buttons do nothing |
| Hardcoded posts | 3 static posts with real Twitter image URLs — not dynamic |
| No active state routing | All nav items look the same (no active highlight except For You tab) |
| Real images from Twitter CDN | Will break if Twitter CDN blocks external requests |
| No dark/light mode toggle | Dark only |
| Tab switching not wired | Clicking "Following" does not change feed content |

### Future Improvements (If Extending)

| Improvement | What to Add |
|---|---|
| Interactive tabs | Add JS to toggle active state and swap post sets |
| Like / Retweet toggle | JS to toggle icon fill state and count |
| Post composer submit | JS to prepend a new post card to the feed |
| Local avatar images | Replace Twitter CDN URLs with local `/assets/` images |
| Tailwind CLI build | Replace CDN with proper CLI build for production performance |
| Multiple pages | Profile page, Explore page, Notifications page |
| Dark/Light toggle | Add JS + Tailwind `dark:` class strategy |
| Accessibility | Add `aria-label` to all icon buttons, keyboard nav |

---

## SECTION 9 — SETUP & RUNNING THE PROJECT

### Option A — CDN (Zero Setup)

Just open `index.html` in any browser. No installation needed. Tailwind is loaded from the CDN.

```bash
# Simply open in browser
open index.html
```

### Option B — Tailwind CLI (Production Build)

```bash
# 1. Install dependencies
npm install

# 2. Run build/watch script
npm run build

# 3. Switch the HTML to use the compiled CSS instead of CDN
# In index.html, replace:
<script src="https://cdn.tailwindcss.com"></script>
# With:
<link rel="stylesheet" href="src/output.css">
```

---

## SECTION 10 — PRE-LAUNCH / SUBMISSION CHECKLIST

### Layout
- [ ] Three-column desktop layout renders correctly at 1280px+
- [ ] Centered layout with equal gutters on desktop
- [ ] Icon-only sidebar on tablet (768px–1023px)
- [ ] Full-width single-column feed on mobile
- [ ] No horizontal scroll on any breakpoint

### Mobile
- [ ] Top header visible on mobile, hidden on tablet/desktop
- [ ] Bottom navigation bar visible on mobile, hidden on tablet/desktop
- [ ] FAB button visible on mobile, hidden on tablet/desktop
- [ ] Feed not hidden behind fixed header or bottom nav (correct mt/pb padding)
- [ ] Safe area inset applied to bottom nav (notch-friendly)

### Visual Consistency
- [ ] All hover states working (nav items, post actions, buttons)
- [ ] Active tab underline on "For You"
- [ ] Post images loading and clipped with `rounded-xl`
- [ ] Correct brand blue (`#1d9bf0`) used on Post button, FAB, links, active tab

### Icons
- [ ] Material Symbols font loaded via CDN
- [ ] All icons rendering (no missing/broken icons)

### Cross-Browser
- [ ] Chrome
- [ ] Firefox
- [ ] Safari (especially iOS safe area behavior)
- [ ] Mobile Chrome / Mobile Safari

### Code Quality
- [ ] No broken image `src` links
- [ ] No duplicate `id` attributes
- [ ] Semantic HTML used where appropriate (`<ul>`, `<li>`, `<button>`)
- [ ] `alt` attributes present on all `<img>` tags
