# GitHub Actions CI/CD Pipeline

This resume repository uses three automated workflows to maintain quality and generate artifacts:

## 🤖 Workflows

### 1. PDF Generation (`pdf-generation.yml`)
**Automatically generates downloadable PDF resumes on every push**

- **When**: Triggered on push to `main` when `index.html` or `style.css` changes
- **What it does**:
  - Generates `resume-en.pdf` (English version)
  - Generates `resume-no.pdf` (Norwegian version)
  - Creates GitHub Release: `resume-YYYY-MM-DD-<run_number>`
  - Uploads both PDFs to the release
  - Stores PDFs as workflow artifacts (90-day retention)
- **Technology**: Puppeteer with headless Chrome
- **PDF Format**: A4, print backgrounds, 20mm/15mm margins

**Access PDFs**: Go to [Releases](../../releases) to download the latest versions

---

### 2. Content Validation (`content-validation.yml`)
**Ensures code quality and bilingual content integrity**

- **When**: Triggered on push to `main`, pull requests, or manual dispatch
- **What it checks**:
  - ✅ HTML syntax validation
  - ✅ CSS syntax validation  
  - ✅ Bilingual parity (EN/NO sections match)
  - ✅ Broken links and file references
  - ✅ Email format validation
  - ✅ Spell checking (English + Norwegian)
  - ✅ Dynamic footer year generation
- **Technology**: html-validate, stylelint, aspell, custom Node.js scripts

**View Results**: Check the workflow run logs for detailed validation output

---

### 3. Lighthouse CI (`lighthouse-ci.yml`)
**Monitors performance, accessibility, and SEO scores**

- **When**: Triggered on push to `main` (HTML/CSS changes), pull requests, or manual dispatch
- **What it audits**:
  - 🚀 Performance (threshold: 90/100)
  - ♿ Accessibility (threshold: 95/100)
  - ✨ Best Practices (threshold: 90/100)
  - 🔍 SEO (threshold: 90/100)
- **Audits both versions**: `#en` and `#no` separately
- **Outputs**: HTML and JSON reports (30-day artifact retention)
- **Technology**: Google Lighthouse CLI

**View Reports**: Download HTML reports from workflow artifacts to see detailed recommendations

---

## 🎯 Score Thresholds

| Metric | Threshold | Type |
|--------|-----------|------|
| Performance | ≥90 | Warning |
| Accessibility | ≥95 | Error |
| Best Practices | ≥90 | Warning |
| SEO | ≥90 | Warning |

---

## 🚀 Manual Workflow Dispatch

All three workflows support manual triggering:

1. Go to **Actions** tab
2. Select the workflow you want to run
3. Click **Run workflow** dropdown
4. Click **Run workflow** button

---

## 📦 Artifacts & Retention

| Workflow | Artifact | Retention |
|----------|----------|-----------|
| PDF Generation | `resume-pdfs` | 90 days |
| PDF Generation | GitHub Release | Permanent |
| Lighthouse CI | `lighthouse-reports` | 30 days |
| Content Validation | Logs only | N/A |

---

## 🛠️ Local Testing

### Test PDF Generation Locally
```bash
# Install dependencies
npm install -g puppeteer

# Run the PDF generation script
node -e "
const puppeteer = require('puppeteer');
(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto('file://' + process.cwd() + '/index.html#en', { waitUntil: 'networkidle0' });
  await page.pdf({ path: 'resume-en.pdf', format: 'A4', printBackground: true });
  console.log('✅ PDF generated: resume-en.pdf');
  await browser.close();
})();
"
```

### Test Content Validation Locally
```bash
# Install validation tools
npm install -g html-validate stylelint stylelint-config-standard

# Validate HTML
npx html-validate index.html

# Validate CSS
npx stylelint style.css
```

### Test Lighthouse Locally
```bash
# Install Lighthouse
npm install -g lighthouse

# Start local server
python3 -m http.server 8080

# Run Lighthouse (in another terminal)
lighthouse http://localhost:8080/index.html#en --view
```

---

## 📝 Workflow Maintenance

### Updating Score Thresholds
Edit the respective workflow YAML file and modify the assertion values:

```yaml
# In lighthouse-ci.yml
"categories:accessibility": ["error", {"minScore": 0.95}]  # Change 0.95 to new threshold
```

### Adding New Validations
Edit `content-validation.yml` and add a new step:

```yaml
- name: Your New Check
  run: |
    # Your validation script here
```

### Changing PDF Format
Edit `pdf-generation.yml` and modify the PDF options:

```javascript
await page.pdf({
  path: pdfPath,
  format: 'A4',         // Change format
  printBackground: true,
  margin: {             // Adjust margins
    top: '20mm',
    bottom: '20mm',
    left: '15mm',
    right: '15mm'
  }
});
```

---

## 🐛 Troubleshooting

### PDF Generation Fails
- Check if Puppeteer can access the HTML file
- Verify language toggle JavaScript executes correctly
- Review workflow logs for Puppeteer errors

### Validation Fails on Spell Check
- Some technical terms may be flagged (expected)
- Add technical terms to aspell personal dictionary if needed
- Warnings don't fail the build

### Lighthouse Scores Below Threshold
- Review the HTML report in artifacts
- Address recommendations in order of impact
- Thresholds are warnings, not hard blockers

---

## 📚 Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Puppeteer API](https://pptr.dev/)
- [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci)
- [html-validate](https://html-validate.org/)
- [Stylelint](https://stylelint.io/)

---

**Last Updated**: 2025-01-20
