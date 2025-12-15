# AI Coding Agent Guide (Resume Website)

**Big Picture**
- Single-page bilingual site: see [index.html](../index.html) and [style.css](../style.css).
- PDFs built from LaTeX sources in [latex-src](../latex-src) and [latex-src-no](../latex-src-no) via GitHub Actions.
- Deployed on GitHub Pages from `main` root; no build step or frameworks.

**Core Patterns**
- Bilingual content: pair every text with `<span class="en">…</span>` and `<span class="no">…</span>`; parity is enforced in CI.
- Language selection: header `EN | NO` toggles; persisted in `localStorage('resumeLang')`; direct links via `/#en` or `/#no`; print forces English via `@media print`.
- Theming & visuals: `data-theme` cycles between `matrix` and `matrix-light` using the top-right button; `particles.js` (CDN) uses `initParticles()` and CSS `--accent-color` for dynamic lines.
- Progressive reveal: `IntersectionObserver` expands `section.card` (collapsed→expanded) and animates `.job`, `.degree`, `.skill-category`, `.endorsement-card`, `.article-card`, `.honor` once.
- Details toggles: clicking a `.job` or `.degree` toggles its `.details.visible` (arrow flips via CSS); link clicks don’t toggle.
- Email obfuscation: Base64 is decoded at runtime to set the `mailto` target.
- SEO/metadata: JSON-LD `Person`, Open Graph/Twitter cards, `canonical`, favicon, and social image are defined in [index.html](../index.html).

**Workflow (Local & CI)**
- Preview locally: `open index.html` or `python3 -m http.server 8000` then visit `/index.html#en`.
- Validate: `npx html-validate index.html` and `npx stylelint style.css`.
- Lighthouse (optional local): serve, then `npx lighthouse http://localhost:8000/index.html#en --view`.
- CI/CD: workflows in `.github/workflows/` — `pdf-generation.yml` (XeLaTeX), `content-validation.yml` (syntax, parity, links, spellcheck, footer year), `lighthouse-ci.yml` (perf/a11y/SEO).
- PDF outputs: `Ghaith_Almujalled_Resume_EN.pdf` and `_NO.pdf` attached to Release (`resume-YYYY-MM-DD-<run_number>`) and available from site header.

**Conventions**
- Keep it vanilla: no JS frameworks, single HTML file architecture.
- Maintain EN/NO parity: update both spans together; CI will flag mismatches.
- Links open externally with `target="_blank"`; print CSS appends URLs in parentheses and hides Norwegian content.
- Design system: card sections with accent borders, 950px container, `scroll-margin-top` for anchors, emoji section icons, and a responsive skills grid (`auto-fit, minmax(250px,1fr)`).

**Integration Points & Files**
- Theme tokens: `[data-theme]` variants in [style.css](../style.css) (`matrix`, `matrix-light`, plus additional presets) control colors and glassmorphism.
- Particles: CDN script in [index.html](../index.html) initializes after CSS loads; call `window.initParticles()` on theme changes.
- LaTeX: modular sections under `latex-src*/cv-sections/`; fonts in `latex-src*/fonts/`; template `awesome-cv.cls`.

**CI Expectations**
- Targets: Performance ≥90, Accessibility ≥95, SEO ≥90; best practices ≥90. Failures/warnings handled per workflow.
- Triggers: push to `main`; LaTeX workflows run only when `latex-src*/` changes; manual dispatch enabled.

If anything here feels unclear or incomplete (e.g., workflow specifics, styling conventions, or bilingual edge cases), tell me what to refine and I’ll update this guide.
