# AI Coding Agent Instructions for LaSoanyah Portfolio

## Project Overview
Single-page portfolio website showcasing LaSoanyah's wellness applications and academic achievements. Built with vanilla HTML/CSS/JavaScript using a cosmic-themed design system. **Not a build system project** – static website deployed directly to web hosting.

## Architecture & Core Components

### File Structure
- `index.html` – Complete single-page structure with all sections (hero, about, apps, achievements, community)
- `styles.css` – Centralized styling with CSS variables for theming; animates cosmic background elements
- `script.js` – Vanilla JS interactions: mobile nav toggle, smooth scrolling, intersection observers, parallax, particle effects
- `images/` – Logo and hero images (graduation photo, casual headshots)

### Design System
**CSS Variables** (defined in `:root`):
- Colors: `--primary-color: #6366f1`, `--secondary-color: #8b5cf6`, `--accent-color: #f59e0b`, `--teal-color: #00bcd4`
- Backgrounds: `--bg-primary: #0f0f23`, `--bg-secondary: #1a1a2e`, `--bg-card: rgba(255, 255, 255, 0.05)`
- Gradients: `--gradient-primary`, `--gradient-teal` for visual emphasis

**Key Animation Patterns**:
- Starfield: `.stars` and `.twinkling` use SVG backgrounds with infinite scroll animations
- Element reveal: Intersection Observer pattern detects when cards enter viewport → triggers fade-in + translateY animation
- Stagger delays: App cards use `transitionDelay` indexed by card position (0.2s * index)

### Major Sections
1. **Navigation** (`.navbar`) – Fixed position, blurred backdrop, hamburger toggle on mobile
2. **Hero Section** – Profile image with parallax effect (scrollY * 0.5), animated title, CTAs
3. **Mini-Course Embed** – iFrame from minicoursegenerator.com (external dependency)
4. **Wellness Apps** (`.app-card` cards) – Features three Lovable apps with hover particle effects
5. **Achievements/Community** – Grid layout following same card animation pattern

## Developer Workflows

### No Build Step Required
- Serve directly with any HTTP server (`python -m http.server`, VS Code Live Server, etc.)
- CSS/JS changes are live-reload compatible
- Changes to HTML are immediately reflected without compilation

### Mobile-First Responsive Design
- Breakpoints managed via CSS media queries (check `styles.css` for specific breakpoints)
- Hamburger menu (`hamburger` class) toggles `active` state to show/hide nav menu
- Test at 320px (phone), 768px (tablet), 1920px+ (desktop)

### Animation Testing
Open DevTools → Elements → toggle `.observer.observe()` elements' classes to simulate scroll animations without scrolling

## Project-Specific Patterns & Conventions

### Intersection Observer for Animations
**Pattern in script.js**:
```javascript
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.style.opacity = '1';
            entry.target.style.transform = 'translateY(0)';
        }
    });
}, observerOptions);
```
- Applied to: `.app-card`, `.achievement-item`, `.social-card`, `.sanctuary-card`
- Always initialize with `opacity: 0` and `translateY(30px)` before observing
- **Stagger effect**: Loop through elements, set `transitionDelay = index * 0.2s` for cascading reveals

### Event Delegation for Cards
- Click handlers on `.app-card`: Trigger scale animation (0.98x), then reset
- Hover handlers on `.app-card`: Move to -10px translateY and 1.02x scale
- Particle effect on hover: Creates 5 floating divs that animate upward and fade out over 2s

### External Dependencies
- **Google Fonts**: Inter (body), Orbitron (headings) loaded via `<link>` in head
- **FontAwesome 6.0**: Icons via CDN (no build dependency)
- **Mini-Course iFrame**: Embedded from minicoursegenerator.com (external host – verify iframe URL if updating)
- **Lovable Apps**: Three external web apps linked in wellness section (validate URLs in deployment)

### Color Usage Guidelines
- Primary accent: Use `--primary-color` (#6366f1) for main CTAs and highlights
- Gradients: Apply `--gradient-primary` or `--gradient-teal` to hero titles, buttons
- Muted text: Use `--text-muted` (#9ca3af) for secondary info
- Glowing effects: Box-shadow with `var(--shadow-glow)` for card depth

## Common Tasks

### Adding a New Section
1. Add section in HTML with unique `id` (for smooth scroll nav)
2. Include section in `.nav-menu` with matching `href="#id"`
3. Apply `.container` wrapper for max-width + padding
4. Use `.section-title` and `.section-subtitle` classes
5. Add element class to intersection observer list in script.js (e.g., `.new-section-card`)
6. Set initial styles in DOMContentLoaded before observing

### Updating Wellness App Links
- URLs stored as `href` in `.app-card` anchor tags or `href` in `.app-link` class
- Validate external app URLs are live before deployment
- Test iFrame embed responsiveness at multiple breakpoints

### Tweaking Animations
- **Speed**: Adjust `duration` in `style.textContent` keyframes (e.g., `@keyframes float { 3s ⟶ 5s }`)
- **Parallax intensity**: Change multiplier in `scrolled * speed` (0.5 = current; lower = less parallax)
- **Stagger timing**: Modify `index * 0.2s` divisor in card animation loops
- **Fade-in delay**: Adjust `threshold` in `observerOptions` (0.1 = trigger when 10% visible)

## Integration Points & Dependencies

### External Services
- **Hosting**: Static file hosting (GitHub Pages, Netlify, Vercel)
- **Fonts**: CDN-hosted via Google Fonts (no fallback needed; uses system fonts if CDN unavailable)
- **Icons**: FontAwesome CDN (falls back to text if unavailable)
- **iFrame Content**: Mini-course generator and Lovable app URLs must be accessible

### Performance Notes
- CSS animations use `transform` and `opacity` only (GPU-accelerated, no layout recalculation)
- Intersection Observer is passive (doesn't block scrolling)
- Images should be optimized (compression tools like TinyPNG)
- Consider lazy-loading images if adding many more sections

## Code Style & Best Practices for This Project

- **No frameworks**: Pure vanilla JS – keep it that way for simplicity
- **CSS variables**: Always use `var(--color-name)` instead of hardcoding hex values
- **Event listeners**: Attach dynamically in DOMContentLoaded to ensure DOM is ready
- **Comments**: Add comments for non-obvious animation logic or delay calculations
- **Mobile-first**: Write mobile styles first, then add media queries for larger screens

---

**Last Updated**: February 2026  
**Contact**: For questions about portfolio structure, see `LaSoanyah Digital Academic Portfolio.md`
