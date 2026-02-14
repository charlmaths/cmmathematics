# Development Notes - Terminal Landing Site

Documentation of changes and decisions made during development.

---

## Project Goal

Transform a simple landing site into a **terminal-themed website** using vanilla HTML, CSS, and JavaScript.

- **Live Site:** https://www.cmmathematics.tech
- **Tech Stack:** HTML5, CSS3, JavaScript (no frameworks)
- **Hosting:** GitHub Pages (deploys from `/docs` folder)

---

## Project Structure

### Final Directory Structure
```
cmmathematics/
├── README.md
├── DEV_NOTES.md (this file)
└── docs/                      # GitHub Pages root
    ├── index.html             # Homepage
    ├── CNAME                  # Custom domain config
    ├── css/
    │   └── styles.css         # All styles in one file
    ├── js/
    │   └── main.js            # Future interactivity
    ├── assets/
    │   ├── images/
    │   └── icons/
    ├── about/
    │   └── index.html
    ├── blog/
    │   └── index.html
    └── contact/
        └── index.html
```

### Key Decision: Single `docs/` Folder
**Why:** GitHub Pages deploys only from the `/docs` folder. Moved all CSS, JS, and assets inside `docs/` to ensure they deploy correctly.

---

## Changes Made

### 1. Fixed CSS File Paths

**Problem:** CSS paths were incorrect after moving files into `docs/` folder.

**Solution:**
```html
<!-- Homepage (docs/index.html) -->
<link rel="stylesheet" href="./css/styles.css" />

<!-- Subpages (docs/about/, docs/blog/, docs/contact/) -->
<link rel="stylesheet" href="../css/styles.css" />
```

**Why:**
- `./css/styles.css` - From `docs/index.html`, go to `docs/css/styles.css` (same level)
- `../css/styles.css` - From `docs/about/index.html`, go up one level to `docs/`, then to `css/`

---

### 2. Fixed Navigation Links

**Problem:** Nav links pointed to `#` (nowhere) or had incorrect paths.

**Solution:**
```html
<!-- In docs/index.html -->
<li><a href="./index.html">Home</a></li>
<li><a href="./about/index.html">About</a></li>
<li><a href="./contact/index.html">Contact</a></li>
<li><a href="./blog/index.html">Blog</a></li>

<!-- In subpages (about/blog/contact) -->
<li><a href="../index.html">Home</a></li>
<li><a href="../about/index.html">About</a></li>
<li><a href="../contact/index.html">Contact</a></li>
<li><a href="../blog/index.html">Blog</a></li>
```

---

### 3. Added Terminal Styling (Phase 1)

**File:** `docs/css/styles.css`

#### CSS Reset
Added a CSS reset to remove browser defaults and ensure consistent styling:
```css
*,
*::before,
*::after {
  box-sizing: border-box;  /* Include padding/border in width calculations */
  margin: 0;
  padding: 0;
}
```

#### Terminal Color Scheme
```css
body {
  background-color: #0c0c0c;  /* Nearly black background */
  color: #00ff00;              /* Classic terminal green */
  font-family: "Courier New", Courier;  /* Monospace font */
  margin: 0;
  padding: 20px;
  min-height: 100vh;          /* Full viewport height */
}
```

**Why these choices:**
- `#0c0c0c` - Dark but not pure black (easier on eyes)
- `#00ff00` - Classic CRT terminal green
- Monospace font - All characters same width (like a real terminal)
- `100vh` - Ensures background covers full screen

#### Terminal Container
```css
.terminal {
  max-width: 900px;
  margin: 0;
  padding: 20px;
  border: 2px solid #00ff00;  /* Green border for window effect */
}
```

**Why:**
- Container creates visual "terminal window" effect
- `max-width` prevents text from being too wide on large screens
- Green border reinforces terminal aesthetic

---

### 4. HTML Structure Updates

**File:** `docs/index.html`

Added `.terminal` container divs to wrap content:
```html
<body>
  <div class="terminal">
    <nav class="menu">
      <!-- navigation -->
    </nav>
  </div>
  <div class="terminal">
    <h1>Desk notes</h1>
    <p>Content...</p>
  </div>
</body>
```

**Why:** Wrapping content in `.terminal` divs allows us to style sections as separate terminal windows.

---

## CSS Architecture Decision

**Choice:** Single stylesheet (`docs/css/styles.css`)

**Why this works:**
- Small project (4 pages)
- Consistent design across all pages
- Easy to maintain and understand
- Professional choice for this scale

**When to split CSS:**
- Large applications (50+ components)
- Multiple developers
- Dramatically different page styles

---

## Key Concepts Learned

### CSS Relative Paths
- `./` = current directory
- `../` = go up one directory level
- `../../` = go up two levels

### CSS Class Selectors
- `.terminal` in CSS targets any element with `class="terminal"`
- The dot (`.`) indicates a class selector

### Box Sizing
- `box-sizing: border-box` makes width/height include padding and borders
- Easier layout calculations

### CSS Variables (For Future Use)
Can define reusable values:
```css
:root {
  --terminal-bg: #0c0c0c;
  --terminal-fg: #00ff00;
}

body {
  background-color: var(--terminal-bg);
  color: var(--terminal-fg);
}
```

---

## GitHub Pages Deployment

### Configuration
- **Source:** Deploy from `main` branch, `/docs` folder
- **Custom Domain:** www.cmmathematics.tech (via CNAME file)

### Deployment Process
1. Make changes locally
2. Commit changes
3. Push to `main` branch on GitHub
4. GitHub Pages auto-deploys (takes 1-10 minutes)
5. Hard refresh browser (`Cmd/Ctrl + Shift + R`) to clear cache

---

## Next Steps (Planned)

### Phase 2: Enhanced Terminal Styling
- [ ] Terminal window titlebar with buttons
- [ ] Terminal prompt styling (e.g., `user@cmmathematics:~$`)
- [ ] Navigation styled as commands

### Phase 3: JavaScript Interactivity
- [ ] Typing animation effect
- [ ] Blinking cursor
- [ ] Interactive command input
- [ ] Command history

---

## Troubleshooting Notes

### Issue: Changes not showing on live site
**Solutions:**
1. Hard refresh: `Cmd + Shift + R` (Mac) or `Ctrl + Shift + R` (Windows)
2. Open in incognito/private browsing mode
3. Wait 5-10 minutes for GitHub Pages deployment
4. Check GitHub Actions tab for deployment status

### Issue: CSS not loading
**Check:**
1. CSS file path is correct for each page's location
2. CSS file exists at `docs/css/styles.css`
3. No typos in the `<link>` tag

---

## Resources & References

- [MDN CSS Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model)
- [MDN CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)

---

**Last Updated:** 2026-02-13
