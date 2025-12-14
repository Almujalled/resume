# Resume Website - AI Coding Agent Instructions

## Project Overview
Static HTML/CSS resume website hosted on GitHub Pages at `almujalled.github.io/resume/`. Single-page application with no build process or JavaScript framework dependencies.

## Architecture
- **Entry Point**: [index.html](../index.html) - Single-page resume with semantic HTML5 sections
- **Styling**: [style.css](../style.css) - Standalone CSS with mobile-first responsive design
- **Deployment**: GitHub Pages auto-deploys from main branch root directory

## Key Design Patterns

### HTML Structure
- Semantic sections: `header`, `summary`, `experience`, `education`, `honors`, `skills`, `footer`
- Single container div (`.container`) wraps all content for centering and styling
- Inline JavaScript only for dynamic year in footer (`<span id="year">`)
- External links use `target="_blank"` for new tab behavior

### Bilingual Content System
- Language toggle: `EN | NO` in header top-right corner
- Content wrapped in `<span class="en">` and `<span class="no">` pairs
- JavaScript toggles display of `.en`/`.no` elements based on selection
- Preference saved to `localStorage` key `resumeLang`
- URL hash support: `#en` or `#no` for direct language linking
- Default language: English
- Print always outputs English (configured in `@media print`)

### CSS Architecture
- **Color Palette**: Primary `#2c3e50`, links `#3498db`, gray scale for text hierarchy
- **Layout**: Max-width 900px centered container, 40px padding (20px on mobile)
- **Grid System**: Skills section uses `grid-template-columns: repeat(auto-fit, minmax(250px, 1fr))`
- **Responsive**: Single breakpoint at 768px; print styles defined in `@media print`

### Styling Conventions
- Section headers: 1.8em with bottom border `2px solid #ecf0f1`
- Job/project titles: 1.3em `#34495e`
- Metadata (company, dates): Italic gray `#95a5a6` for dates, `#7f8c8d` for companies
- Transitions: `0.3s` for link hover effects
- Language toggle: `.lang-toggle` positioned absolute, active state `#3498db`

## Development Workflow

### Local Testing
```bash
# No build step required - just open in browser
open index.html
# OR use Python simple server for testing
python3 -m http.server 8000
```

### Content Updates
1. Edit personal info in [index.html](../index.html) header section (name, title, contact links)
2. For bilingual content, always update BOTH `.en` and `.no` spans
3. Test responsive design at 768px breakpoint
4. Verify print layout (Cmd+P) - URLs append to links automatically, shows English only

### GitHub Pages Deployment
- Auto-deploys on push to `main` branch
- No build configuration needed
- Site serves from repository root (not `/docs` or gh-pages branch)

## Important Constraints
- **No JavaScript frameworks** - Keep it vanilla HTML/CSS with minimal inline JS
- **Single file architecture** - Avoid splitting into multiple HTML pages
- **Print optimization** - Maintain print-friendly CSS that shows link URLs in parentheses
- **Static content only** - No server-side processing or API calls
- **Bilingual parity** - Always keep EN and NO content in sync

## Common Modifications
- Add sections: Follow pattern in existing sections (header with border, content divs with `.en`/`.no` spans)
- Change colors: Update hex values in header/section h2 styles
- Adjust spacing: Modify section `margin-bottom` (35px default) or container padding
- Skills grid: Add/remove `.skill-category` divs - grid auto-adapts with `auto-fit`
- Add new language content: Create both `<span class="en">...</span>` and `<span class="no">...</span>`

## GitHub Actions CI/CD Workflows

### PDF Generation (`.github/workflows/pdf-generation.yml`)
**Purpose**: Auto-generate downloadable PDF versions on every push to main
- **Triggers**: Push to main (when index.html/style.css changes), manual dispatch
- **Outputs**: 
  - English PDF: `resume-en.pdf`
  - Norwegian PDF: `resume-no.pdf`
  - GitHub Release: `resume-YYYY-MM-DD-<run_number>` with both PDFs attached
  - Workflow artifacts: 90-day retention
- **Technology**: Puppeteer with inline JavaScript for language toggle automation
- **PDF Settings**: A4 format, print backgrounds enabled, 20mm top/bottom, 15mm left/right margins

### Content Validation (`.github/workflows/content-validation.yml`)
**Purpose**: Ensure code quality and bilingual content integrity
- **Triggers**: Push to main, pull requests, manual dispatch
- **Validations**:
  - HTML syntax validation (html-validate)
  - CSS syntax validation (stylelint)
  - Bilingual parity check (EN/NO span count matching)
  - Broken link detection (internal file references, email format)
  - Spell checking (English with aspell-en, Norwegian with aspell-no)
  - Footer year dynamic generation verification
- **Exit Behavior**: Warnings logged but workflow passes; errors fail the build

### Lighthouse CI (`.github/workflows/lighthouse-ci.yml`)
**Purpose**: Monitor performance, accessibility, and SEO scores
- **Triggers**: Push to main (when index.html/style.css changes), pull requests, manual dispatch
- **Audits**: Both EN (#en) and NO (#no) versions tested separately
- **Metrics**:
  - Performance: ≥90/100 (warning threshold)
  - Accessibility: ≥95/100 (error threshold)
  - Best Practices: ≥90/100 (warning threshold)
  - SEO: ≥90/100 (warning threshold)
- **Outputs**: HTML and JSON reports uploaded as artifacts (30-day retention)
- **Technology**: Lighthouse CLI running against local Python HTTP server

### Workflow Best Practices
- All workflows use Ubuntu latest runner
- Node.js 20 for consistent JavaScript execution
- Artifacts have appropriate retention (30-90 days based on importance)
- Score thresholds are warnings/errors, not hard blockers (to allow iteration)
- Manual dispatch enabled for testing without code changes

## Testing Checklist
- [ ] Language toggle switches all content correctly
- [ ] Responsive layout at 768px and below
- [ ] Print preview shows URLs in parentheses (English only)
- [ ] Links open in new tabs where appropriate
- [ ] Footer year updates dynamically
- [ ] Content fits within 900px max-width without horizontal scroll
- [ ] URL hash navigation works (`#en`, `#no`)
- [ ] GitHub Actions workflows pass (PDF generation, validation, Lighthouse CI)
- [ ] PDF downloads are properly formatted for both EN and NO
- [ ] Lighthouse scores meet thresholds (Performance 90+, Accessibility 95+, SEO 90+)
