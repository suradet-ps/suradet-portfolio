# Detrix

```
██████╗ ███████╗████████╗██████╗ ██╗██╗  ██╗
██╔══██╗██╔════╝╚══██╔══╝██╔══██╗██║╚██╗██╔╝
██║  ██║█████╗     ██║   ██████╔╝██║ ╚███╔╝
██║  ██║██╔══╝     ██║   ██╔══██╗██║ ███╔╝
██████╔╝███████╗   ██║   ██║  ██║██║██╔██╗
╚═════╝ ╚══════╝   ╚═╝   ╚═╝  ╚═╝╚═╝╚═╝ ╚═╝
```

---

## ◆ PULSE

A portfolio is a living document, not a static page. Detrix presents the
professional record of a healthcare technologist - works, innovations,
speaking, and academic contributions - fetched from Supabase and grouped
by category, so the story updates without a redeploy. The page reads
quiet and editorial: white canvas, dark ink, signature color bands that
punctuate the scroll, nothing fighting for attention until a section
needs to.

| Works ▣ | Innovation ▣ | Speaker ▣ | Academic ▣ |
|---|---|---|---|

*The record is content, not markup: add an entry through the key-protected
route and the page tells it.*

> Built with Svelte 5 runes + SvelteKit 2, strict TypeScript with zero
> `any`, rendered on the server, served through Supabase.
>
> **suradet-ps**, artifact keeper

---

## ◆ IGNITION

One runtime, four commands.

```
⟫ bun install
⟫ bun run dev
```

Open [http://localhost:5173](http://localhost:5173).

```
⟫ bun run build       # SSR + client bundle
⟫ bun run check       # svelte-check, strict types
```

<details>
<summary>Environment</summary>

A `.env` file with three keys:

```
PUBLIC_SUPABASE_URL="https://your-project.supabase.co"
PUBLIC_SUPABASE_ANON_KEY="your-anon-key"
SECRET_ADD_POST_KEY="your-secret-key"
```

`SECRET_ADD_POST_KEY` is read only server-side via `$env/static/private` -
never shipped to the client.

</details>

---

## ◆ ANATOMY

One page, three layers, no shared secrets.

- **Serves** - SvelteKit renders on the server: no `window` or
  `document` in the SSR path, Supabase queries run in the load function,
  not in components.
- **Groups** - portfolio items fetched once, grouped by category
  (Speaker, Academic Work, Innovation, and the rest), and revealed on
  scroll through an Intersection Observer - the motion is a layer on top
  of content that already exists.
- **Guards** - the `/add` route verifies a secret key server-side, with
  CSRF origin checks, IP rate limiting (30 req/min), input validation,
  and security headers on every response. No client-side secrets exist
  to leak.
- **Talks** - toasts replace `alert()`, a focus-trapped modal holds the
  detail view, and every interactive element answers to the keyboard -
  the page is readable by humans and by assistive technology alike.
- **Wears** - one design system in `DESIGN.md`: tokens.css owns spacing,
  typography, and color; dark mode is a `prefers-color-scheme` toggle
  away, never a fork of the markup.

---

## ◆ RITUALS

**The core ceremony** - the daily add:

1. Open the key-protected route, enter the secret.
2. Fill the form: category, title, dates, description. The server
   validates category against a whitelist, lengths against limits, dates
   against a format.
3. Submit. A toast confirms or reports - no `alert()`, no silent
   failure.
4. Refresh the page. The new entry is grouped, revealed, and told.

**The ceremony of access** - every card opens into a keyboard-navigable
modal with a focus trap and an Escape exit; focus returns where it
started. Notifications speak through `aria-live`, errors through
`role="alert"`.

**The ceremony of restraint** - reduced motion is respected, scroll
reveals yield, and the whitespace does the selling. The brand voltage
comes from signature color bands every few screens, not from gradient
washes.

---

## ◆ ECHOES

**Where this artifact is heading**

```
content   ▸ Supabase-backed items, no redeploy for updates ──────── ▸ sealed
guards    ▸ server-side key, CSRF, rate limits, security headers ── ▸ sealed
access    ▸ keyboard-first, focus traps, ARIA, reduced motion ───── ▸ sealed
delivery  ▸ adapter-vercel, SSR + client bundle ──────────────────── ▸ sealed
```

**Raising the artifact** - contributions follow conventional commits and
open a pull request first. The design language is specified in
`DESIGN.md`; the code keeps strict TypeScript, zero `any`, and no
unchecked access.

**Status** - every push is checked by the [CI workflow](.github/workflows)
on its way to Vercel.

---

```
  ─────────────────────────────────────────
   A portfolio is not a resume.
   It is a body of work that keeps speaking.
  ─────────────────────────────────────────
```

Distributed under the [MIT License](LICENSE).