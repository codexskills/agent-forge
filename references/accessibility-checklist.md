# Accessibility Checklist (WCAG 2.2 AA)

## Core Principles (POUR)

| Principle | Meaning |
|-----------|---------|
| **P**erceivable | Users must be able to perceive the content (at least one sense) |
| **O**perable | Users must be able to operate the interface |
| **U**nderstandable | Users must be able to understand the content and interface |
| **R**obust | Content must be interpretable by assistive technologies |

## Keyboard Navigation

### Focus Management
- [ ] All interactive elements reachable via Tab key
- [ ] Visible focus indicator on all elements (3:1 contrast ratio minimum)
- [ ] Logical tab order follows visual order (DOM order matches visual order)
- [ ] No focus traps (user can Tab out of any component)
- [ ] Skip navigation link present (first focusable element)
- [ ] Focus is managed dynamically (modal opens → focus trap, closes → return focus)
- [ ] Custom components have appropriate ARIA roles and keyboard handlers

### Keyboard Interactions
- [ ] Enter/Space activates buttons and links
- [ ] Arrow keys work for lists, menus, tabs, sliders
- [ ] Escape closes modals, menus, popovers
- [ ] Tab moves between focusable elements
- [ ] Home/End for scrollable containers
- [ ] No keyboard-only functionality broken

### Focus Indicators
```css
/* Default focus ring */
:focus-visible {
  outline: 2px solid #4A90D9;
  outline-offset: 2px;
}

/* Never do this */
:focus {
  outline: none;  /* Remove only with alternative focus indicator */
}
```

## Screen Reader Support

### Semantic HTML
- [ ] Correct heading hierarchy (h1 → h2 → h3, no skipping)
- [ ] Landmarks used: `<nav>`, `<main>`, `<aside>`, `<footer>`, `<header>`
- [ ] Lists use `<ul>`/`<ol>` (not styled divs)
- [ ] Buttons are `<button>` elements (not clickable divs)
- [ ] Links are `<a>` elements with href
- [ ] Tables use `<th>`, `<caption>`, `<thead>`, `<tbody>`

### ARIA (Accessible Rich Internet Applications)
- [ ] ARIA roles only used when semantic HTML is insufficient
- [ ] `aria-label` on elements without visible text (icon buttons)
- [ ] `aria-labelledby` linking to visible text labels
- [ ] `aria-describedby` for additional descriptions
- [ ] `aria-expanded` on expandable elements (accordions, menus)
- [ ] `aria-selected` on tab panels
- [ ] `aria-current` on active navigation items
- [ ] `aria-live` regions for dynamic content updates
  - `polite`: non-critical updates (status messages)
  - `assertive`: critical updates (errors)
- [ ] `aria-hidden="true"` on decorative elements (icons, spacers)
- [ ] `role="alert"` for error messages
- [ ] `role="status"` for non-critical status updates
- [ ] `role="progressbar"` with `aria-valuenow`, `aria-valuemin`, `aria-valuemax`

### Alt Text
- [ ] All images have alt text (`alt=""` for decorative)
- [ ] Alt text describes content and function (not "image of...")
- [ ] Complex images (charts, diagrams) have detailed description nearby
- [ ] Functional images (icon links) have alt describing action
- [ ] Alt text is concise (under 125 characters)

### Screen Reader Announcements
```html
<!-- Live region for dynamic updates -->
<div aria-live="polite" aria-atomic="true">
  Cart updated: 3 items
</div>

<!-- Status updates -->
<div role="status" aria-live="polite">
  Search results loaded (12 results)
</div>

<!-- Error announcements -->
<div role="alert">
  Please correct the following errors: Email is required
</div>
```

## Visual Design

### Color and Contrast
- [ ] Normal text: contrast ratio ≥ 4.5:1 (AA)
- [ ] Large text (≥ 18px or ≥ 14px bold): contrast ratio ≥ 3:1
- [ ] UI components and graphical objects: contrast ratio ≥ 3:1
- [ ] Information not conveyed by color alone (add icons, labels, patterns)
- [ ] Focus indicators have ≥ 3:1 contrast against background
- [ ] Link text distinguishable from body text (not just color)
- [ ] Error states indicated by more than color (icon + text)

### Text and Typography
- [ ] Text can be resized to 200% without loss of content
- [ ] No horizontal scroll at 400% zoom (1280px viewport at 400% = 320px)
- [ ] Line height at least 1.5
- [ ] Paragraph spacing at least 1.5x line height
- [ ] Letter spacing at least 0.12em
- [ ] Word spacing at least 0.16em
- [ ] Fonts support text spacing overrides

### Layout and Responsive
- [ ] Content reflows at 320px viewport width (no horizontal scroll)
- [ ] Touch targets at least 24x24px (prefer 44x44px)
- [ ] No content overlap at any viewport size
- [ ] Orientation not locked (works in portrait and landscape)

## Forms

### Labels and Instructions
- [ ] All inputs have associated `<label>` elements
- [ ] Required fields indicated (asterisk + "required" text)
- [ ] Input format/hints provided (e.g., "MM/DD/YYYY")
- [ ] Autocomplete attributes on form fields (`autocomplete="email"`)
- [ ] Error messages linked to inputs (`aria-describedby`)

### Error Handling
- [ ] Errors clearly identified (not just red border)
- [ ] Error messages describe what's wrong and how to fix
- [ ] Errors listed at top of form (summary)
- [ ] Focus moved to first error after submission
- [ ] Success confirmation announced to screen readers

```html
<!-- Form field with error -->
<label for="email">Email address</label>
<input
  id="email"
  type="email"
  aria-describedby="email-error"
  aria-invalid="true"
/>
<span id="email-error" role="alert">
  Please enter a valid email address
</span>

<!-- Error summary -->
<div role="alert" aria-labelledby="error-summary">
  <h2 id="error-summary">2 errors found</h2>
  <ul>
    <li><a href="#email">Email is required</a></li>
    <li><a href="#password">Password is required</a></li>
  </ul>
</div>
```

## Dynamic Content

### Modals and Dialogs
- [ ] Modal triggered by button
- [ ] Focus trapped inside modal when open
- [ ] Escape key closes modal
- [ ] Focus returns to trigger element on close
- [ ] `role="dialog"` and `aria-modal="true"`
- [ ] `aria-labelledby` pointing to modal title

### Tabs
- [ ] Tab list with `role="tablist"`
- [ ] Each tab has `role="tab"`, `aria-selected`, `aria-controls`
- [ ] Tab panel has `role="tabpanel"`, `aria-labelledby`
- [ ] Keyboard: Arrow keys switch tabs, Home/End for first/last

### Accordions
- [ ] Button has `aria-expanded="true/false"`
- [ ] Panel has `aria-labelledby` pointing to button
- [ ] Panel has `role="region"` (optional but helpful)

### Carousels / Sliders
- [ ] Pause, play, next, prev controls
- [ ] Auto-rotating carousels have pause mechanism
- [ ] No auto-play for moving content (or pause on focus)
- [ ] All slides accessible via keyboard

## Testing Tools

### Automated
```bash
# axe-core (best for CI)
npx @axe-core/cli https://example.com

# Lighthouse Accessibility audit
npx lighthouse https://example.com --preset=accessibility

# Pa11y CI
npx pa11y-ci https://example.com

# WAVE (browser extension)
# https://wave.webaim.org/

# Accessibility Insights
# https://accessibilityinsights.io/
```

### Manual Testing
- [ ] Keyboard-only navigation (Tab, Enter, Escape, Arrow keys)
- [ ] Screen reader testing (VoiceOver, NVDA, JAWS)
- [ ] Zoom to 200% and 400%
- [ ] High contrast mode
- [ ] Reduced motion setting (`prefers-reduced-motion`)
- [ ] Dark mode (`prefers-color-scheme: dark`)

### CI Integration
```yaml
# .github/workflows/a11y.yml
name: Accessibility
on: [pull_request]
jobs:
  a11y:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm run build
      - run: npx @axe-core/cli http://localhost:3000
```

## WCAG 2.2 AA Success Criteria Checklist

### A (Must support)
- [ ] 1.1.1 Non-text Content (alt text)
- [ ] 1.2.1 Audio-only and Video-only (transcripts)
- [ ] 1.3.1 Info and Relationships (semantic structure)
- [ ] 1.3.2 Meaningful Sequence (reading order)
- [ ] 1.3.3 Sensory Characteristics (not just shape/size/color)
- [ ] 1.4.1 Use of Color (not sole indicator)
- [ ] 2.1.1 Keyboard (all functionality)
- [ ] 2.1.2 No Keyboard Trap
- [ ] 2.2.1 Timing Adjustable
- [ ] 2.2.2 Pause, Stop, Hide
- [ ] 2.3.1 Three Flashes
- [ ] 2.4.1 Bypass Blocks (skip link)
- [ ] 2.4.2 Page Titled
- [ ] 2.4.3 Focus Order
- [ ] 2.4.4 Link Purpose (In Context)
- [ ] 2.5.1 Pointer Gestures
- [ ] 2.5.2 Pointer Cancellation
- [ ] 2.5.3 Label in Name
- [ ] 2.5.4 Motion Actuation
- [ ] 3.1.1 Language of Page
- [ ] 3.2.1 On Focus
- [ ] 3.2.2 On Input
- [ ] 3.3.1 Error Identification
- [ ] 3.3.2 Labels or Instructions
- [ ] 4.1.1 Parsing
- [ ] 4.1.2 Name, Role, Value
- [ ] 4.1.3 Status Messages

### AA (Should support)
- [ ] 1.2.4 Captions (Live)
- [ ] 1.2.5 Audio Description (Prerecorded)
- [ ] 1.3.4 Orientation
- [ ] 1.3.5 Identify Input Purpose
- [ ] 1.4.3 Contrast (Minimum) ← **most commonly failed**
- [ ] 1.4.4 Resize Text
- [ ] 1.4.5 Images of Text
- [ ] 1.4.10 Reflow
- [ ] 1.4.11 Non-text Contrast
- [ ] 1.4.12 Text Spacing
- [ ] 1.4.13 Content on Hover or Focus
- [ ] 2.4.5 Multiple Ways
- [ ] 2.4.6 Headings and Labels
- [ ] 2.4.7 Focus Visible
- [ ] 2.4.11 Focus Not Obscured (Minimum)
- [ ] 2.5.7 Dragging Movements
- [ ] 2.5.8 Target Size (Minimum)
- [ ] 3.1.2 Language of Parts
- [ ] 3.2.3 Consistent Navigation
- [ ] 3.2.4 Consistent Identification
- [ ] 3.3.3 Error Suggestion
- [ ] 3.3.4 Error Prevention (Legal, Financial, Data)

## Reduced Motion

### CSS Media Query
```css
/* Respect user preference */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

/* Opt-in to essential motion */
@media (prefers-reduced-motion: no-preference) {
  .fade-in {
    animation: fadeIn 0.5s ease-in;
  }
}
```

## Common Accessibility Issues

| Issue | Fix |
|-------|-----|
| Missing alt text | Add descriptive `alt` or `alt=""` |
| Low contrast text | Increase contrast to ≥ 4.5:1 |
| No focus indicator | Add visible `:focus-visible` styles |
| Non-semantic HTML | Use `<button>`, `<nav>`, `<main>` |
| Color-only indicators | Add icons, patterns, text labels |
| Missing form labels | Add `<label for="id">` |
| No skip link | Add "Skip to content" link |
| Keyboard trap | Fix focus management |
| No ARIA on custom widgets | Add appropriate roles and properties |
| Poor heading structure | Fix heading hierarchy (no skipping) |

## Usage
Reference this checklist when building UI components, testing for accessibility, and before shipping to production. Run automated tools in CI and perform manual keyboard + screen reader testing.
