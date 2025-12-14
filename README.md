[![Live Site](https://img.shields.io/badge/🌐_Live_Site-almujalled.github.io%2Fresume-blue?style=for-the-badge)](https://almujalled.github.io/resume/)
[![PDF Generation](https://img.shields.io/badge/📄_Auto_PDF-Enabled-success?style=for-the-badge)](../../releases)
[![Lighthouse CI](https://img.shields.io/badge/🚀_Performance-90%2B-brightgreen?style=for-the-badge)](../../actions)

**EN** | **NO** • Static HTML/CSS • GitHub Pages • Automated CI/CD

</div>

---

## 🎯 What Makes This Resume Special?

This isn't just another static resume website. It's a **fully automated, bilingual, CI/CD-powered professional portfolio** that:

- 🌍 **Speaks Two Languages**: Instant toggle between English and Norwegian (with localStorage persistence!)
- 🤖 **Auto-Generates PDFs**: Every push creates fresh EN/NO PDFs in [Releases](../../releases)
- 🔍 **Self-Validates**: HTML/CSS syntax, bilingual parity, spell checking, link verification
- ⚡ **Performance Monitored**: Lighthouse CI ensures 90+ scores on every deployment
- 📱 **Responsive AF**: Looks perfect on phones, tablets, desktops, and **printers**
- 🎨 **Design System**: Accent borders, emoji icons, 2-column responsive skills grid

## 🚀 Quick Start

```bash
# Clone & preview
git clone https://github.com/Almujalled/resume.git
cd resume
open index.html  # or python3 -m http.server 8080

# Bilingual magic
# Click "EN | NO" in top-right corner
# Or navigate to: /#en or /#no
# Language preference saved to localStorage
```

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | Vanilla HTML5 + CSS3 + ES6 JavaScript |
| **Design** | Mobile-first responsive, print-optimized |
| **PDF Source** | LaTeX (XeLaTeX compiler) - Awesome-CV template |
| **Deployment** | GitHub Pages (auto-deploy from `main`) |
| **CI/CD** | 3 GitHub Actions workflows |
| **PDF Engine** | XeLaTeX compilation (professional typography) |
| **Validation** | html-validate, stylelint, aspell |
| **Monitoring** | Lighthouse CI (Performance/A11y/SEO) |

## 🤖 Automation Workflows

Every push to `main` triggers:

### 📄 **PDF Generation (LaTeX)**
- XeLaTeX compiles professional PDFs from `latex-src/` and `latex-src-no/`
- Awesome-CV template with custom fonts and styling
- Creates tagged GitHub Release: `resume-YYYY-MM-DD-<run>`
- 90-day artifact retention + permanent release storage
- **Triggers**: Changes to `latex-src/**` or `latex-src-no/**`

### ✅ **Content Validation**
- HTML/CSS syntax validation
- Bilingual parity check (EN/NO span count matching)
- Broken link detection
- Email format validation
- English + Norwegian spell checking
- Dynamic footer year verification

### 🚀 **Lighthouse CI**
- Performance: ≥90/100 ⚡
- Accessibility: ≥95/100 ♿
- Best Practices: ≥90/100 ✨
- SEO: ≥90/100 🔍
- Generates HTML reports for both languages

**View workflow details**: [.github/workflows/README.md](.github/workflows/README.md)

## 📐 Architecture

```
resume/
├── index.html           # Bilingual single-page web app
├── style.css            # Responsive design system
├── latex-src/           # English LaTeX source (Awesome-CV)
│   ├── resume_cv.tex    # Main LaTeX file
│   ├── cv-sections/     # Modular CV sections
│   ├── fonts/           # Custom fonts
│   └── awesome-cv.cls   # Template class
├── latex-src-no/        # Norwegian LaTeX source
│   └── (same structure)
├── .github/
│   ├── copilot-instructions.md   # AI agent guidance
│   └── workflows/
│       ├── pdf-generation.yml    # XeLaTeX PDF compilation
│       ├── content-validation.yml # HTML/CSS quality checks
│       ├── lighthouse-ci.yml      # Performance monitoring
│       └── README.md              # Workflow documentation
└── README.md            # You are here 👈
```

## 🎨 Design Philosophy

- **Container**: 950px max-width, centered, 40px padding (20px mobile)
- **Color Palette**: Primary `#2c3e50`, Accent `#3498db`, Gray scale hierarchy
- **Typography**: 1.8em section headers, 1.3em job titles, 1.05em body
- **Spacing**: Tightened to 28px sections, 20px jobs (dense but breathable)
- **Accents**: 4px left border `#3498db` on sections, 3px on skill cards
- **Responsive**: 768px mobile breakpoint, 1200px widescreen 2-column grid

## 🌐 Bilingual System

```javascript
// Language toggle architecture
<span class="en">English content</span>
<span class="no">Norwegian content</span>

// localStorage key: 'resumeLang'
// URL hash support: #en, #no
// Print always outputs: English
```

**Key Rule**: Always update BOTH `.en` and `.no` spans to maintain parity!

## 📦 Download PDF

**Latest versions available in [Releases](../../releases):**
- `Ghaith_Almujalled_Resume_EN.pdf`
- `Ghaith_Almujalled_Resume_NO.pdf`

PDFs auto-generated on every content change with perfect print styling.

## 🧪 Local Testing

```bash
# Validate HTML
npx html-validate index.html

# Validate CSS
npx stylelint style.css

# Generate PDF locally
npm install -g puppeteer
node -e "const p=require('puppeteer');(async()=>{const b=await p.launch();const pg=await b.newPage();await pg.goto('file://'+__dirname+'/index.html#en',{waitUntil:'networkidle0'});await pg.pdf({path:'resume.pdf',format:'A4',printBackground:true});await b.close();})()"

# Run Lighthouse
python3 -m http.server 8080 &
npx lighthouse http://localhost:8080/index.html#en --view
```

## 🔧 Customization Guide

1. **Personal Info**: Edit `<header>` in `index.html`
2. **Content**: Update bilingual `<span class="en">` / `<span class="no">` pairs
3. **Colors**: Search/replace hex codes in `style.css`
4. **Layout**: Modify `.container` max-width or section spacing
5. **Skills Grid**: Add/remove `.skill-category` divs (auto-responsive)

**Remember**: Keep EN/NO content in sync! The validation workflow will catch mismatches.

## 🏆 Lighthouse Scores

Current targets (enforced by CI):
- **Performance**: 90+ ⚡
- **Accessibility**: 95+ ♿  
- **Best Practices**: 90+ ✨
- **SEO**: 90+ 🔍

Check latest scores in [Actions](../../actions/workflows/lighthouse-ci.yml) artifacts.

## 🤝 Contributing

This is a personal resume, but feel free to:
- **Fork** as a template for your own bilingual resume
- **Star** if you find the automation setup useful
- **Report issues** with the workflows or design

## 📜 License

Open source. Use this as a template for your own resume. No attribution required (but appreciated!).

---

<div align="center">

**Built with** 💙 **and excessive automation** 🤖

[View Live](https://almujalled.github.io/resume/) • [Download PDF](../../releases) • [CI/CD Docs](.github/workflows/README.md)

</div>