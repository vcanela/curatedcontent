This single Markdown file contains the complete technical plan, the unified CSS "HUD" styles, and the HTML structure for all three levels of your website. You can copy-paste this into a `README.md` or a project documentation file.

---

# Project Plan: Medicine & Science Research Hub (HUD Edition)

## 1. Project Overview
This project is a 21-page educational portal designed to teach **online literacy** to Year 9 students. It uses a "Heads-Up Display" (HUD) to keep students anchored within the educational framework while they navigate through various "fake" sources of information.

### The 3-Tier Hierarchy
1.  **Level 1: The Library (1 page)** – The main landing page (`index.html`).
2.  **Level 2: Topic Hubs (5 pages)** – Overview of specific subjects (e.g., `vaccines.html`).
3.  **Level 3: Source Pages (15 pages)** – The individual "fake" websites to be analyzed.

---

## 2. File Directory Structure
To ensure the breadcrumbs and relative links work, organize your files exactly like this:

```text
/root-folder/
│
├── index.html                (The Library / Home)
│
└── topics/                   (Folder for Level 2)
    ├── vaccines.html
    ├── antibiotics.html
    ├── semmelweis.html
    ├── lister.html
    ├── clinical-trials.html
    │
    └── sources/              (Folder for Level 3)
        ├── vaccine-s1.html
        ├── vaccine-s2.html
        ├── vaccine-s3.html
        └── [all other 12 source files...]
```

---

## 3. The Master HUD CSS
Copy this CSS block into the `<style>` tag of **every single HTML file**. It ensures the navigation bar stays "stuck" to the top of the screen even as the student scrolls.

```css
:root {
  --navy: #1a2744;
  --navy-mid: #243660;
  --teal: #0d7a6e;
  --white: #ffffff;
  --gold: #c8922a;
}

/* Core Layout Adjustments */
body {
  margin: 0;
  padding: 0;
  padding-top: 70px; /* Space for the fixed HUD */
  font-family: 'Source Sans 3', sans-serif;
  background-color: #f4f5f7;
}

/* The HUD Bar */
.hud-top-bar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 60px;
  background: var(--navy);
  border-bottom: 4px solid var(--teal);
  display: flex;
  align-items: center;
  z-index: 9999; /* Keeps HUD above all other content */
  box-shadow: 0 4px 10px rgba(0,0,0,0.2);
}

.hud-container {
  max-width: 1100px;
  margin: 0 auto;
  width: 100%;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Breadcrumb Styling */
.breadcrumbs {
  color: #8fa3c8;
  font-size: 0.9rem;
  letter-spacing: 0.02em;
}

.breadcrumbs a {
  color: var(--white);
  text-decoration: none;
  font-weight: 600;
  transition: color 0.2s;
}

.breadcrumbs a:hover {
  color: var(--gold);
}

.sep {
  margin: 0 10px;
  color: var(--teal);
  font-weight: bold;
}

.current-page {
  color: var(--white);
  opacity: 0.8;
  font-weight: 400;
}

/* Literacy Badge */
.hud-badge {
  background: rgba(255,255,255,0.1);
  border: 1px solid var(--teal);
  color: var(--white);
  padding: 4px 10px;
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  border-radius: 3px;
}
```

---

## 4. Tiered HTML Templates

### Level 1: index.html (The Library)
```html
<div class="hud-top-bar">
  <div class="hud-container">
    <div class="breadcrumbs">
      <strong>Research Hub Library</strong>
    </div>
    <div class="hud-badge">Year 9 Science Portal</div>
  </div>
</div>
```

### Level 2: topics/[topic-name].html (e.g., vaccines.html)
```html
<div class="hud-top-bar">
  <div class="hud-container">
    <div class="breadcrumbs">
      <a href="../index.html">Home</a>
      <span class="sep">/</span>
      <span class="current-page">Vaccines Research Area</span>
    </div>
    <div class="hud-badge">Topic Hub</div>
  </div>
</div>
```

### Level 3: topics/sources/[source-name].html (e.g., vaccine-s1.html)
```html
<div class="hud-top-bar">
  <div class="hud-container">
    <div class="breadcrumbs">
      <a href="../../index.html">Home</a>
      <span class="sep">/</span>
      <a href="../vaccines.html">Vaccines</a>
      <span class="sep">/</span>
      <span class="current-page">Source Analysis</span>
    </div>
    <div class="hud-badge">External Source Analysis</div>
  </div>
</div>
```

---

## 5. Summary of Navigation Paths
| Current Location | Link to Home | Link to Topic |
| :--- | :--- | :--- |
| **Index** | `index.html` | `topics/vaccines.html` |
| **Topic Hub** | `../index.html` | `vaccines.html` |
| **Individual Source** | `../../index.html` | `../vaccines.html` |

---

## 6. Pedagogical Features
* **The "Anchor":** By keeping the HUD top bar identical in style regardless of the "messy" design of the fake source pages, students recognize that they are still within the "safe" evaluation zone.
* **Read-Only Integrity:** Because the HUD is `position: fixed`, it effectively boxes in the research content, making it clear to the student that the information they are reading is a "specimen" to be observed, not necessarily a truth to be accepted.
* **Breadcrumb Logic:** The clear pathing forces students to see how information is categorized (Topic > Source), reinforcing the idea that individual sources belong to a wider context.