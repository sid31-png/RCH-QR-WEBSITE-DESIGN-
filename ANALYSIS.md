# RCH Qatar redesign — analysis (phase 0, awaiting validation)

CSS/JS/Three.js overlay for rch.qa (WordPress + Elementor + PhastPress + Polylang).
No back-end, PHP, DOM-structure or SEO changes — visual + animation layer only.

## Saudi reference (`reference/rch-saudi.html`)
Bundled React/Vite SPA (~15 MB, React inlined) — decoded for *direction*, not code reuse.

- **Palette (Saudi, do NOT reuse as-is):** accent `#AF1882` (purple-magenta), structure
  `#293d81` (indigo), text `#181d27`/`#0a0d12`, grays `#535862`/`#717680`/`#d5d7da`,
  cool bg `#f5f7ff`. Skews purple/indigo.
- **Typography:** Inter (Regular/Medium/Semibold) + Noto Sans Arabic / Tajawal (AR).
- **Layout:** very airy, full-width alternating white / cool-gray sections, large rounded
  cards, editorial hero, service grids, clients + partners logo rows.
- **Animation:** GSAP + IntersectionObserver, scroll reveals, marquee, animated counters.
- **Sections:** hero, services, offices/plans, "Everything Your Business Needs", clients,
  partners, blog, CTA, footer.

### Keep / adapt / discard for Qatar
- **Keep:** airy editorial rhythm, scroll reveals, client marquee, stat counters, Inter,
  white / cool-gray alternation.
- **Adapt:** palette → Qatar magenta `#D6286B` + navy `#1A3A5C`; radius 8/12/16;
  subtle navy-tinted shadows; magenta used sparingly.
- **Discard:** all Saudi *content* (Saudi sells physical coworking; Qatar sells PRO
  services + company formation), the indigo/purple, Saudi office/plan modules,
  "Book a Tour" CTA.

Qatar homepage section order is a 1:1 reskin of the existing Elementor: Hero (title +
tagline + CTA + stats + 3D logo), CEO quote, Mission/Vision, RAPID values, Services
(Company Formation, PRO Services, Partnership, Supporting, Business Consultation),
Company Profile, Case Studies, Clients, Blog, Footer.

## 3D logo (`assets/rch-logo.glb`)
- glTF v2, valid, **10.1 MB** (mostly textures).
- 1 mesh / 1 primitive, centered at origin, identity transform.
- Bounding box: X [-0.95, 0.95], Y [-0.24, 0.24], Z [-0.75, 0.75] — flat, elongated
  paper plane, ideal for a 3/4 view.
- 1 PBR material, 4 JPEG textures (baseColor + metallic-rough + normal + emissive).
  baseColorFactor white, **metallic 1.0 / roughness 1.0** → will look chromed; override
  to ~metalness 0.15 / roughness 0.6 so magenta reads as matte paper.
- **Framing:** ~35° FOV, 3/4 view (yaw ~-25°, pitch ~10°), transparent bg, in `#rch-logo-3d`.
- **Lighting:** key (front-top) + navy fill (`#1A3A5C`, low) + ambient ~0.6 + rim.
  antialias on, dpr capped at 2.
- **Motion:** autoplay gentle Y-rotation + light mouse parallax (±8°), optional scroll link.
- **Fallback:** WebGL absent or `prefers-reduced-motion` → static image.
  `assets/rch-logo-fallback.png` is only 78×62 — too small; needs an HD poster (TBD).

## Open questions (blocking hero build)
1. Fallback logo: generate an HD poster from the GLB, or Sid provides a crisp PNG?
2. GLB is 10 MB — lazy-load after first paint (recommended), or Draco-compress a copy?

## Status
Awaiting Sid's validation of the visual direction before building the hero PoC.
