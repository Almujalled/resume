# Resume Website - AI Coding Agent Instructions

## Project Overview
Static HTML/CSS resume website hosted on GitHub Pages at `almujalled.github.io/resume/`. Single-page application with no build process or JavaScript framework dependencies.

## Architecture
- **Entry Point**: [index.html](../index.html) - Single-page resume with semantic HTML5 sections
- **Styling**: [style.css](../style.css) - Standalone CSS with mobile-first responsive design
- **Deployment**: GitHub Pages auto-deploys from main branch root directory

## Key Design Patterns

### HTML Structure
- Semantic sections: `header`, `summary`, `experience`, `education`, `skills`, `projects`, `footer`
- Single container div (`.container`) wraps all content for centering and styling
- Inline JavaScript only for dynamic year in footer (`<span id="year">`)
- External links use `target="_blank"` for new tab behavior

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
2. Update sections by replacing placeholder text - structure is already semantic
3. Test responsive design at 768px breakpoint
4. Verify print layout (Cmd+P) - URLs append to links automatically

### GitHub Pages Deployment
- Auto-deploys on push to `main` branch
- No build configuration needed
- Site serves from repository root (not `/docs` or gh-pages branch)

## Important Constraints
- **No JavaScript frameworks** - Keep it vanilla HTML/CSS with minimal inline JS
- **Single file architecture** - Avoid splitting into multiple HTML pages
- **Print optimization** - Maintain print-friendly CSS that shows link URLs in parentheses
- **Static content only** - No server-side processing or API calls

## Common Modifications
- Add sections: Follow pattern in existing sections (header with border, content divs)
- Change colors: Update hex values in header/section h2 styles
- Adjust spacing: Modify section `margin-bottom` (35px default) or container padding
- Skills grid: Add/remove `.skill-category` divs - grid auto-adapts with `auto-fit`

## Testing Checklist
- [ ] Responsive layout at 768px and below
- [ ] Print preview shows URLs in parentheses
- [ ] Links open in new tabs where appropriate
- [ ] Footer year updates dynamically
- [ ] Content fits within 900px max-width without horizontal scroll
