---
name: interactive-portfolio-builder
description: Use when building, redesigning, or auditing an interactive developer/creator portfolio with tokenized design discipline, GSAP scroll choreography, playable demos, 3D viewers, gamification, and an integrated printable A4 CV.
---

# Interactive Portfolio Builder

Combine **Hallmark design discipline**, **interactive/gamified web engineering** (live demos, 3D viewers, GSAP ScrollTrigger choreography), and **CV/career best practices** into one cohesive, static-first portfolio (HTML5 + CSS3 + Vanilla JS).

## 1. Design Floor (Hallmark Rules)

Apply these non-negotiable rules before writing CSS or HTML:

1. **Tokenize everything in `tokens.css` (`:root`)**: Declare `--color-paper`, `--color-paper-2`, `--color-paper-3`, `--color-ink`, `--color-ink-2`, `--color-muted`, `--color-rule`, `--color-accent`, `--color-accent-ink`, `--space-*`, and `--font-*`. Never scatter literal hex/oklch values or raw spacing past the token block.
2. **GPU-only transitions**: Never use `transition: all` and never animate `left`, `top`, `width`, or `height`. Animate only `transform` and `opacity`.
3. **Layout & overflow safety**: Set `overflow-x: clip` on both `html` and `body` (never `100vw` containers). Use `minmax(0, 1fr)` on grid tracks and `overflow-wrap: break-word; min-width: 0` on headings.
4. **Contrast & tabular numbers**: Keep all text/badges at `>= 4.5:1` contrast. Apply `font-variant-numeric: tabular-nums` on counters, telemetry, and XP/score readouts.
5. **Accessibility & fallbacks**: Provide `:focus-visible` outlines, `@media (prefers-reduced-motion: reduce)` fallbacks on all animations, and ensure content/CV remain visible with JS off or in `@media print`.
6. **Audit**: If Hallmark is installed, run `node /home/john/.gemini/config/skills/hallmark/scripts/sloplint.mjs index.html` before shipping and resolve contrast, token, and transition issues.

## 2. Portfolio Architecture (Step-by-Step)

### A. Preloader + Smooth Cross-Fade
- Place a fixed `#clockPreloader` (or brand emblem SVG) at the top of `<body>` with `body.is-loading`.
- Put **critical inline CSS** in `<head>` using token fallbacks so the loader renders on the first byte, even on slow connections.
- Dismiss only after **both** `window.load` and a short minimum display (`~950 ms`), with a safety timeout (`8000 ms`) so external CDNs never trap the user.

### B. Hero & Scroll-Reactive Emblem
- Full-width hero with name, clear role headline, 1-sentence value proposition, primary CTA, and direct contact/CV actions.
- Keep a fixed background SVG emblem (`pointer-events: none`) whose scroll rotation is driven by a CSS variable (`--crescent-rot`) updated via passive `scroll` listener.

### C. GSAP + ScrollTrigger Project Reveal (Customizable Choreography)
- **Adapt the animation to the creator's identity**: The clock/Triforce sweep from this reference is only one possible signature. Feel free to invent **any original scroll animation** that fits the user's universe (e.g., PCB circuit-trace drawing, terminal boot sequence, magnetic card fan-out, SVG emblem split/reassembly, parallax depth reveal, or particle burst) while keeping these engineering guardrails:
  - Separate project cards with a dedicated `.project-summon-zone` (`clamp(180px, 24vh, 240px)` on desktop) when an animation needs empty stage space before each card.
  - Hide cards in CSS only when JS is active (`body.has-gsap-summon .project-card:not(.is-summoned) { opacity: 0; transform: scale(0.95); }`).
  - Trigger early (`ScrollTrigger.create({ trigger: zone, start: 'top 82%' })`), compute live coordinates via `getBoundingClientRect()`, and **reveal the project card only after its entrance animation finishes** (`tl.add(..., 'invoke+=...')`).
  - Always use `overwrite: 'auto'`, animate only `transform`/`opacity`, and include a fast-scroll/anchor-jump fallback so no card stays stuck invisible.

### D. Playable Demos, Windowed Games & 3D Rail
- **Windowed Game Modal (`#gameWindowModal`)**: Launch embedded Web games (Godot HTML5, canvas demos) inside a centered `16:9` modal window (`max-width: 960px`) with an expand toggle (`96vw`) and an explicit **`✕` close button** + `Escape` handler (clearing `iframe.src = 'about:blank'` on close). Avoid forcing native browser fullscreen on launch.
- **Attention CTAs (`.btn-attention`)**: Apply a subtle pulsing glow and periodic diagonal sheen sweep on playable game/challenge buttons (paused on hover/focus and disabled under `prefers-reduced-motion`).
- **3D Asset Rail (`#lab3d`)**: Horizontal scrollable rail of `<model-viewer>` `.glb` cards (`camera-controls`, `auto-rotate`, `autoplay`) paired with fallback `<canvas>` wireframes.
- **Individual Skill Cards (`.skill-mini-grid`)**: Present languages, tools, and OS (e.g., `Python`, `C++`, `C#`, `GDScript`, `Linux`, `KiCad`, `Proteus`, `Godot`, `Blender`) as compact separate cards instead of a cramped scrolling ticker.

### E. Gamification Loop
- Turn the navbar mission counter into an interactive **Quest Log button** (`Missions : X/5 · XP`).
- Clicking it opens `#questModal` showing:
  - Progressive rank (`Visiteur` -> `Apprenti` -> `Explorateur` -> `Ingénieur` -> `Maître`)
  - XP progress bar (`+100 XP` per completed interactive demo/game/3D inspection)
  - Clickable mission items that smooth-scroll directly to each section.
- Pair completions with a toast notification and optional WebAudio SFX (`Son : On / Off`).

## 3. Integrated A4 CV & Career Polish

Include a built-in printable CV modal (`#cvModal` / `#cvSheet`) engineered with the 5 career rules:

1. **Print-Ready 1-Page A4 (`@media print`)**:
   - Set `@page { size: A4 portrait; margin: 6mm; }` and `print-color-adjust: exact !important`.
   - Hide `.navbar`, `main`, `footer`, preloader, game/quest modals, and `.no-print`.
   - Use `break-inside: avoid` on blocks and verify rendered height stays `<= 1122 px` at 96 DPI.
2. **Quantified Achievement Bullets**:
   - Replace passive duty descriptions with strong action verbs + real metrics (e.g., number of PCBs built, prototypes delivered, team/club members led). Never invent numbers.
3. **Role Tailoring & Clickable Links**:
   - Align the CV headline, summary, and skill order to the target role (e.g., Embedded Systems & Automation).
   - Make email, phone/WhatsApp, LinkedIn, GitHub, and live portfolio URL clickable with clean SVG icons.
   - If the user applies through automated ATS portals, offer a 1-column plain-text-friendly variant alongside the visual 2-column A4 sheet.
4. **Companion Cover Letter**:
   - Generate a 250–400 word tailored cover letter connecting the portfolio's real metrics and projects to `[Company Name]` with a strong opening hook and clear call to action.

## 4. Verification & Static Deployment Checklist

1. Validate JS syntax (`node -c app.js`) and check Hallmark `sloplint.mjs`.
2. Test locally (`python3 -m http.server 8000`) on desktop (`1280×950`) and mobile (`390×844`): preloader fade, ScrollTrigger reveal timing, windowed game open/`✕` close, 3D viewer, and `Ctrl+P` 1-page A4 print preview.
3. Deploy cleanly to **GitHub Pages**, **Vercel**, or **Netlify** (for large `.wasm`/`.glb` assets > 50 MB total, connect GitHub repo to Netlify/Vercel rather than single-zip proxy upload), then update the live URL inside the CV, `README.md`, and cover letter.
