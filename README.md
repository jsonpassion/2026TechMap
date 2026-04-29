# Apple Developer Academy — TechMap

An interactive puzzle map of tech sessions run by mentors at the Apple Developer Academy. Each session is represented as an interlocking puzzle piece in a neo-brutalist style.

## Features

- 4×4 interlocking puzzle grid (13 sessions + 3 placeholders)
- Real SVG puzzle piece shapes with tabs and blanks
- Neo-brutalism design — bold borders, hard shadows, vivid colors
- Hover/tap tooltips with session details
- Responsive — works on desktop and mobile
- Zero dependencies — pure HTML, CSS, JavaScript

## File Structure

```
TechMap/
├── index.html          # Main SPA entry point
├── style.css           # Neo-brutalism styles
├── script.js           # Puzzle generation & interactions
├── .gitignore
├── README.md
└── assets/
    └── images/
        └── sessions/
            ├── debugging/
            │   └── placeholder.svg
            ├── healthcare/
            ├── testing-lab/
            ├── concurrency-lab/
            ├── package-lab/
            ├── spatial-computing/
            ├── ai-app/
            ├── local-database/
            ├── createml/
            ├── aiml/
            ├── networking/
            ├── animation-swiftui/
            └── computational-thinking/
```

## Running Locally

Open `index.html` directly in any modern browser — no server required.

```bash
open index.html
# or
python3 -m http.server 8080   # then visit http://localhost:8080
```

## Deploying to GitHub Pages

### Option 1 — Deploy from `main` branch root

1. Push all files to a GitHub repository.
2. Go to **Settings → Pages**.
3. Under **Source**, select **Deploy from a branch**.
4. Choose `main` branch and `/ (root)` folder.
5. Click **Save**. Your site will be live at `https://<username>.github.io/<repo>/`.

### Option 2 — GitHub Actions (recommended)

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - id: deployment
        uses: actions/deploy-pages@v4
```

Then in **Settings → Pages**, set source to **GitHub Actions**.

## Adding Real Session Images

Replace `assets/images/sessions/<session-id>/placeholder.svg` with real images. Supported formats: SVG, PNG, JPEG.

## Adding New Sessions

Edit the `SESSIONS` array in `script.js`. The grid expands automatically:

```javascript
{
  id: 'my-session',
  title: 'My New Session',
  mentor: 'MentorName',
  emoji: '🚀',
  color: '#FF0000',
  textColor: '#fff',
  description: 'Session description here.',
  url: 'https://your-session-url.com',
  status: 'active',   // 'active' | 'coming-soon' | 'future'
}
```

## Customization

| What | Where |
|------|-------|
| Colors, fonts, spacing | `style.css` |
| Session data & descriptions | `SESSIONS` array in `script.js` |
| Grid columns | `COLS` constant in `script.js` |
| Piece dimensions | `PW`, `PH`, `TAB_SIZE` in `script.js` |
| Puzzle path shape | `piecePath()` function in `script.js` |
