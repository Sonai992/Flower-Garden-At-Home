# Flower Garden - Project Analysis

## 1. Project Overview

Flower Garden is a static, image-rich website about flowers that bloom during different seasons in Bengal and other parts of India. The project combines:

- A modern visual landing page with a hero slideshow and flower gallery.
- A seasonal catalogue with pages for summer, monsoon, autumn, winter, and spring.
- Flower descriptions, gardening guidance, cultural context, and links to social profiles.
- Local image assets organized by season and by page purpose.

The project uses plain HTML and CSS. It does not currently require a framework, package manager, database, backend, or build process.

## 2. Main User Experience

There are two related entry points:

### Landing page: `index.html`

This is the most polished entry point. It contains:

- A full-screen hero section.
- A CSS crossfade slideshow using images from `images/`.
- Primary navigation to the flower gallery and `garden.html`.
- A responsive gallery with five flower cards.
- Lazy-loaded gallery images and descriptive `alt` text.
- A compact footer.

### Seasonal catalogue: `garden.html`

This page acts as the catalogue home page. It contains:

- A navigation bar linking to all seasonal pages.
- An introduction to flower gardening.
- Popular summer and monsoon flower cards.
- Social media links in the footer.

The seasonal pages are:

| Page | Theme | Main content |
| --- | --- | --- |
| `summer.html` | Summer | Hibiscus, Sunflower, Zinnia, Portulaca, Rose, Cosmos |
| `monsoon.html` | Monsoon | African Marigold, Rain Lily, Aparajita, Nayantara, Dopati, Chrysanthemum |
| `autumn.html` | Autumn | Shiuli, Kash Phool, Kanak Champa, Rajnigandha, and gardening tips |
| `winter.html` | Winter | Chandramallika, Dahlia, Winter Marigold, Petunia |
| `spring.html` | Spring | Palash, Madhabilata, Shimul, Jacaranda, Tabebuia, Kanikonna |

Each seasonal page presents an introduction followed by large image-and-text flower cards. Several pages alternate the image position with the `.reverse` class.

## 3. Technology and Implementation

- **HTML5:** Page structure, navigation, headings, image content, links, and footer content.
- **CSS3:** Responsive layouts, gradients, card layouts, hover states, transitions, shadows, slideshow animation, and scroll-based animation rules.
- **JavaScript:** `summer.html` uses `IntersectionObserver` to add a reveal class to cards as they enter the viewport.
- **External resources:** Google Fonts are loaded by the seasonal pages.
- **Assets:** Images, favicon files, and seasonal media are stored locally in the repository.

There is no JavaScript framework and no dependency manifest. The site can be opened directly in a browser or served with any simple static file server.

## 4. Repository Structure

```text
Flower Garden/
|-- index.html                  Landing page and gallery
|-- garden.html                 Seasonal catalogue home
|-- summer.html                 Summer flowers
|-- monsoon.html                Monsoon flowers
|-- autumn.html                 Autumn flowers and gardening tips
|-- winter.html                 Winter flowers
|-- spring.html                 Spring flowers
|-- style.css                   Landing page styles
|-- styles.css                  Catalogue home styles
|-- summer.css                  Summer page styles
|-- monsoon.css                 Monsoon page styles
|-- autumn.css                  Autumn page styles
|-- winter.css                  Winter page styles
|-- spring.css                  Spring page styles
|-- images/                     Landing page and gallery images
|-- Garden_overvew/             Catalogue home images
|-- Summer/                     Summer page images
|-- Monsoon/                    Monsoon page images
|-- Autumn/                     Autumn page images
|-- winter/                     Winter page images
|-- spring/                     Spring page images
|-- icon/                       Favicon used by catalogue pages
|-- Flower-Garden-Favicon.png   Favicon used by the landing page
|-- .github/                    GitHub-related project configuration
|-- .git/                       Git metadata
```

## 5. Design Analysis

### Strengths

- The project has a clear visual identity based on nature, flowers, and seasonal color palettes.
- The landing page provides a strong first impression with a full-screen hero and image gallery.
- Seasonal pages include meaningful cultural context instead of only listing flower names.
- Most images have `alt` text, and the landing page uses lazy loading for gallery images.
- Responsive breakpoints are present in the catalogue and seasonal stylesheets.
- Local assets make the core content available without an image CDN.
- The repeated card structure makes the seasonal pages easy to understand and extend.

### Visual system

- `style.css` uses a cream, leaf-green, and white palette for the landing page.
- `styles.css` uses a green glass-style navigation and catalogue cards.
- `summer.css` uses warm yellow and orange tones.
- `monsoon.css` uses green, blue, pink, and orange accents.
- `autumn.css` uses warm orange, brown, gold, purple, and pink accents.
- `winter.css` uses cool blue backgrounds with pink, orange, and lavender accents.
- `spring.css` uses fresh green backgrounds with flower-specific accent variables.

The seasonal stylesheets are visually related but are not yet based on one shared component stylesheet or design-token file.

## 6. Current Issues and Technical Risks

These notes describe the current source files and recent fixes.

### High priority

1. **Navigation is split between two entry points.** `index.html` links to `garden.html`, while the seasonal footer links back to `garden.html` rather than consistently linking to the landing page. Decide whether `index.html` or `garden.html` is the canonical home page and use it everywhere.
2. **Some HTML is invalid or poorly formed.** Examples include custom attributes such as `1st`, `2nd`, and `3rd`, inline `<style>` blocks inside footers, a literal Markdown-style code fence in `autumn.html`, and content placed after `</body>` in `summer.html`.
3. **The page structure is duplicated.** Footer markup and footer CSS are repeated across multiple pages, increasing the chance of inconsistent fixes.
4. **Content labels and images sometimes disagree.** For example, some autumn cards use class names and image `alt` text from different flowers, and the winter page stylesheet is linked while the page still uses autumn-oriented class names.
5. **GitHub Pages image paths are case-sensitive.** The Spring page previously referenced five files with lowercase names even though the repository files began with uppercase letters. Windows served those paths locally, but GitHub Pages returned 404 errors. The references in `spring.html` were corrected to match the exact filenames: `Madhabilata.jpg`, `Shimul.jpg`, `Jacaranda.jpg`, `Tabebuia.jpg`, and `Kanikonna.jpg`.

### Medium priority

1. **Accessibility can be improved.** Seasonal pages need more consistent landmarks, descriptive page metadata, keyboard-visible focus states, and better control of decorative emoji and external links.
2. **External font loading is repeated.** Several pages include multiple Google Font requests, sometimes requesting overlapping families. These can be consolidated into one request per page or moved to a shared stylesheet strategy.
3. **Image filenames are difficult to maintain.** Many seasonal images use long generated names. Human-readable names or a content manifest would make future maintenance easier.
4. **The landing page has a text typo.** The gallery caption `Yello Golden garden glow` should be corrected.
5. **There are inconsistent typography declarations.** A few styles reference fonts that are not imported on that page, and `autumn.css` contains a misspelled `Plfair Display` family name.
6. **Some CSS is duplicated or contains old rules.** For example, `styles.css` repeats `width` and `backdrop-filter` declarations, and `summer.css` contains selectors that do not match the page header classes.
7. **The project has no automated validation.** There are no tests, HTML validation checks, link checks, image checks, or accessibility checks configured.

## 7. Recommended Improvement Plan

### Phase 1: Correctness

- Choose one canonical home page and update every navigation link.
- Remove invalid attributes and move inline styles into the relevant CSS files.
- Remove the literal code fence from `autumn.html`.
- Place the `summer.html` footer inside the `<body>` element.
- Correct mismatched titles, headings, class names, `alt` text, and flower descriptions.
- Check every local image reference for case-sensitive path correctness. This check has been applied to the Spring page after a GitHub Pages deployment issue.

### Phase 2: Shared structure

- Create one shared navigation and footer pattern.
- Extract shared seasonal card rules into a common stylesheet.
- Keep only palette and page-specific rules in `spring.css`, `summer.css`, `monsoon.css`, `autumn.css`, and `winter.css`.
- Introduce CSS custom properties for common spacing, content widths, borders, and typography.

### Phase 3: Accessibility and performance

- Add unique meta descriptions to every page.
- Add visible `:focus-visible` styles to all links.
- Mark decorative emoji and decorative images appropriately.
- Add `loading="lazy"` to below-the-fold seasonal images.
- Optimize large images and use responsive `srcset` images where practical.
- Add a reduced-motion rule for slideshow, hover, and scroll-reveal effects.

### Phase 4: Quality checks

- Validate all HTML documents.
- Run a broken-link and missing-asset check.
- Test at mobile, tablet, and desktop widths.
- Check contrast and keyboard navigation.
- Add a short contribution guide if other people will maintain the project.

## 8. How to Run

Because this is a static website, no installation is required.

### Direct opening

Open `index.html` in a browser. Local assets should load correctly from the project folder.

### Static server

For more reliable local behavior, serve the folder with a static server. For example, with Python installed:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/
```

## 9. Project Status

The project is a visually expressive static prototype with substantial seasonal content and local assets. The Spring image-loading issue on GitHub Pages has been fixed by matching image-reference casing to the committed filenames. The strongest next step is structural cleanup: unify navigation, repair invalid markup, consolidate repeated footer and card styles, and add basic validation before expanding the content further.
