---
name: ui-ux-pro-max-angular
description: "UI/UX design guidance for Angular apps (Angular Material, Angular CDK, Angular Router, signals). Use when designing, building, reviewing, or fixing Angular UI: pages, components, dialogs, sidenavs, tables, forms, design systems, theming, dark mode, accessibility, animation, responsive layout, typography, color, and charts. Uses the ui-ux-pro-max search engine with its --stack angular guidelines. Skip for backend, API, database, or infrastructure work."
---

# UI/UX Pro Max - Angular Design Intelligence

Design guide for Angular applications (current Angular: standalone components, signals, built-in control flow). It layers Angular, Angular Material and Angular CDK guidance on top of the [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) searchable database of styles, color palettes, font pairings, product reasoning rules, UX guidelines and chart types.

> **Requires the base `ui-ux-pro-max` skill.** This skill has no data or scripts of its own; every search command below runs the base skill's `search.py`. See [Requirements](#requirements).

## When to Apply

This Skill should be used when the task involves **UI structure, visual design decisions, interaction patterns, or user experience quality control** in Angular.

### Must Use

This Skill must be invoked in the following situations:

- Designing new pages (Landing Page, Dashboard, Admin, SaaS)
- Creating or refactoring Angular UI components (buttons, modals, forms, tables, charts, dialogs, sidenavs)
- Choosing color schemes, typography systems, spacing standards, or layout systems
- Reviewing Angular UI code for user experience, accessibility, or visual consistency
- Implementing navigation structures, animations, or responsive behavior with Angular Router
- Making product-level design decisions (style, information hierarchy, brand expression)
- Improving perceived quality, clarity, or usability of interfaces

### Recommended

This Skill is recommended in the following situations:

- Angular UI looks "not professional enough" but the reason is unclear
- Receiving feedback on usability or experience
- Pre-launch UI quality optimization
- Aligning cross-platform design (Web / iOS / Android)
- Building Angular design systems or reusable component libraries
- Working with Angular Material or custom SCSS theming

### Skip

This Skill is not needed in the following situations:

- Pure backend logic development (no UI involved)
- Only involving API or database design
- Performance optimization unrelated to the interface
- Infrastructure or DevOps work
- Non-visual scripts or automation tasks

**Decision criteria**: If the task will change how a feature **looks, feels, moves, or is interacted with** in an Angular application, this Skill should be used.

## Rule Categories by Priority

*For human/AI reference: follow priority 1→10 to decide which rule category to focus on first; use `--domain <Domain>` to query details when needed. Scripts do not read this table.*

| Priority | Category | Impact | Domain | Key Checks (Must Have) | Anti-Patterns (Avoid) |
|----------|----------|--------|--------|------------------------|------------------------|
| 1 | Accessibility | CRITICAL | `ux` | Contrast 4.5:1, Alt text, Keyboard nav, Aria-labels | Removing focus rings, Icon-only buttons without labels |
| 2 | Touch & Interaction | CRITICAL | `ux` | Min size 44×44px (Material default 48×48px), 8px+ spacing, Loading feedback | Reliance on hover only, Instant state changes (0ms) |
| 3 | Performance | HIGH | `ux` | WebP/AVIF, Lazy loading, Reserve space (CLS < 0.1) | Layout thrashing, Cumulative Layout Shift |
| 4 | Style Selection | HIGH | `style`, `product` | Match product type, Consistency, SVG icons (no emoji) | Mixing flat & skeuomorphic randomly, Emoji as icons |
| 5 | Layout & Responsive | HIGH | `ux` | Mobile-first breakpoints, Viewport meta, No horizontal scroll | Horizontal scroll, Fixed px container widths, Disable zoom |
| 6 | Typography & Color | MEDIUM | `typography`, `color` | Base 16px, Line-height 1.5, Semantic color tokens | Text < 12px body, Gray-on-gray, Raw hex in components |
| 7 | Animation | MEDIUM | `ux` | Duration 150–300ms, Motion conveys meaning, Spatial continuity | Decorative-only animation, Animating width/height, No reduced-motion |
| 8 | Forms & Feedback | MEDIUM | `ux` | Visible labels, Error near field, Helper text, Progressive disclosure | Placeholder-only label, Errors only at top, Overwhelm upfront |
| 9 | Navigation Patterns | HIGH | `ux` | Predictable back, Sidenav ≤5 items, Deep linking | Overloaded nav, Broken back behavior, No deep links |
| 10 | Charts & Data | LOW | `chart` | Legends, Tooltips, Accessible colors | Relying on color alone to convey meaning |

## Quick Reference

### 1. Accessibility (CRITICAL)

- `color-contrast` - Minimum 4.5:1 ratio for normal text (large text 3:1)
- `focus-states` - Visible focus rings on interactive elements (2–4px)
- `alt-text` - Descriptive alt text for meaningful images
- `aria-labels` - aria-label for icon-only buttons; use Angular attribute directives
- `keyboard-nav` - Tab order matches visual order; full keyboard support
- `form-labels` - Use label with for attribute; `<mat-label>` in Angular Material
- `skip-links` - Skip to main content for keyboard users
- `heading-hierarchy` - Sequential h1→h6, no level skip
- `color-not-only` - Don't convey info by color alone (add icon/text)
- `dynamic-type` - Support system text scaling; avoid truncation as text grows
- `reduced-motion` - Respect prefers-reduced-motion; reduce/disable animations when requested
- `cdk-a11y` - Use Angular CDK a11y module for focus trapping, live announcer, aria
- `escape-routes` - Provide cancel/back in modals and multi-step flows
- `keyboard-shortcuts` - Preserve system and a11y shortcuts; offer keyboard alternatives

### 2. Touch & Interaction (CRITICAL)

- `touch-target-size` - Min 44×44 CSS px; Angular Material's default density gives 48×48px, so don't shrink density below that on touch screens
- `touch-spacing` - Minimum 8px gap between touch targets
- `hover-vs-tap` - Use click/tap for primary interactions; don't rely on hover alone
- `loading-buttons` - Disable button during async operations; show spinner or progress using Angular Material spinner
- `error-feedback` - Clear error messages near problem
- `cursor-pointer` - Add cursor-pointer to clickable elements (Web)
- `gesture-conflicts` - Avoid horizontal swipe on main content; prefer vertical scroll
- `tap-delay` - Use touch-action: manipulation to reduce 300ms delay (Web)
- `standard-gestures` - Use platform standard gestures consistently
- `system-gestures` - Don't block system gestures (Control Center, back swipe, etc.)
- `press-feedback` - Visual feedback on press (ripple/highlight) - use Angular Material ripple
- `haptic-feedback` - Use haptic for confirmations and important actions; avoid overuse
- `gesture-alternative` - Don't rely on gesture-only interactions; always provide visible controls
- `safe-area-awareness` - Keep primary touch targets away from notch, Dynamic Island, gesture bar
- `no-precision-required` - Avoid requiring pixel-perfect taps on small icons or thin edges
- `swipe-clarity` - Swipe actions must show clear affordance or hint
- `drag-threshold` - Use a movement threshold before starting drag
- `cdk-drag` - Use Angular CDK DragDrop for accessible drag interactions

### 3. Performance (HIGH)

- `image-optimization` - Use WebP/AVIF, responsive images (srcset/sizes), lazy load non-critical assets
- `image-dimension` - Declare width/height or use aspect-ratio to prevent layout shift
- `font-loading` - Use font-display: swap/optional to avoid invisible text (FOIT)
- `font-preload` - Preload only critical fonts; avoid overusing preload on every variant
- `critical-css` - Prioritize above-the-fold CSS (inline critical CSS or early-loaded stylesheet)
- `lazy-loading` - Lazy load Angular routes via `loadChildren` or `loadComponent`
- `bundle-splitting` - Split code by route/feature to reduce initial load and TTI
- `third-party-scripts` - Load third-party scripts async/defer; audit and remove unnecessary ones
- `reduce-reflows` - Avoid frequent layout reads/writes; batch DOM reads then writes
- `content-jumping` - Reserve space for async content to avoid layout jumps
- `lazy-load-below-fold` - Use loading="lazy" for below-the-fold images and heavy media
- `virtualize-lists` - Virtualize lists with 50+ items using Angular CDK ScrollingModule
- `main-thread-budget` - Keep per-frame work under ~16ms for 60fps
- `progressive-loading` - Use skeleton screens / shimmer instead of long blocking spinners for >1s operations
- `input-latency` - Keep input latency under ~100ms for taps/scrolls
- `tap-feedback-speed` - Visual feedback must start within 100ms of a tap (the animation itself then runs 150–300ms, see §7)
- `debounce-throttle` - Use RxJS debounceTime/throttleTime for high-frequency events
- `on-push` - Use OnPush for input-driven components where skipping subtree checks fits; prepare components for zoneless change detection
- `track-in-for` - Always give `@for` a stable `track` expression (e.g. `track item.id`, not `track $index` for dynamic data)
- `defer-below-fold` - Wrap heavy below-the-fold content in `@defer (on viewport)` with a `@placeholder` of the same size
- `ng-optimized-image` - Use `NgOptimizedImage` (`ngSrc`, `width`/`height`, `priority` for the LCP image)
- `signals` - Use Angular Signals (`signal`, `computed`, `linkedSignal`, `resource`) for fine-grained reactivity instead of observables where appropriate
- `offline-support` - Provide offline state messaging and basic fallback (PWA / service worker)
- `network-fallback` - Offer degraded modes for slow networks (lower-res images, fewer animations)

### 4. Style Selection (HIGH)

- `style-match` - Match style to product type
- `consistency` - Use same style across all components
- `no-emoji-icons` - Use SVG icons (Heroicons, Lucide, Material Icons), not emojis
- `color-palette-from-product` - Choose palette from product/industry
- `effects-match-style` - Shadows, blur, radius aligned with chosen style
- `angular-material-theme` - Build cohesive Angular Material themes with custom palettes
- `state-clarity` - Make hover/pressed/disabled states visually distinct while staying on-style
- `elevation-consistent` - Use a consistent elevation/shadow scale for cards, sheets, modals - Angular Material elevation tokens (`--mat-sys-level0`…`level5`)
- `dark-mode-pairing` - Design light/dark variants together
- `icon-style-consistent` - Use one icon set/visual language across the product (Material Icons, Heroicons, etc.)
- `system-controls` - Prefer native/system controls over fully custom ones
- `blur-purpose` - Use blur to indicate background dismissal (modals, sheets), not as decoration
- `primary-action` - Each screen should have only one primary CTA; secondary actions visually subordinate

### 5. Layout & Responsive (HIGH)

- `viewport-meta` - width=device-width initial-scale=1 (never disable zoom)
- `mobile-first` - Design mobile-first, then scale up to tablet and desktop
- `breakpoint-consistency` - Use systematic breakpoints (e.g. 375 / 768 / 1024 / 1440) with Angular CDK BreakpointObserver
- `readable-font-size` - Minimum 16px body text on mobile (avoids iOS auto-zoom)
- `line-length-control` - Mobile 35–60 chars per line; desktop 60–75 chars
- `horizontal-scroll` - No horizontal scroll on mobile; ensure content fits viewport width
- `spacing-scale` - Use a 4px/8px incremental spacing system
- `touch-density` - Keep component spacing comfortable for touch
- `container-width` - Consistent max-width on desktop (max-w-6xl / 7xl)
- `z-index-management` - Define layered z-index scale (e.g. 0 / 10 / 20 / 40 / 100 / 1000)
- `fixed-element-offset` - Fixed navbar/sidenav must reserve safe padding for underlying content
- `scroll-behavior` - Avoid nested scroll regions that interfere with the main scroll experience
- `viewport-units` - Prefer min-h-dvh over 100vh on mobile
- `orientation-support` - Keep layout readable and operable in landscape mode
- `content-priority` - Show core content first on mobile; fold or hide secondary content
- `visual-hierarchy` - Establish hierarchy via size, spacing, contrast — not color alone
- `css-layout` - Use CSS Grid/Flexbox (or Tailwind) for responsive layouts; Angular Flex Layout (`fxLayout`) is deprecated
- `rtl-support` - Use CSS logical properties (`margin-inline-start`, `inset-inline-end`) and the CDK `Directionality`/`dir` attribute so layouts mirror correctly for RTL languages

### 6. Typography & Color (MEDIUM)

- `line-height` - Use 1.5-1.75 for body text
- `line-length` - Limit body text to 60–75 characters per line on desktop and 35–60 on mobile (same as `line-length-control`)
- `font-pairing` - Match heading/body font personalities
- `font-scale` - Consistent type scale (e.g. 12 14 16 18 24 32)
- `contrast-readability` - Darker text on light backgrounds (e.g. slate-900 on white)
- `text-styles-system` - Use platform type system: Angular Material type roles
- `weight-hierarchy` - Use font-weight to reinforce hierarchy: Bold headings (600–700), Regular body (400), Medium labels (500)
- `color-semantic` - Define semantic color tokens (primary, secondary, error, surface, on-surface) not raw hex in components
- `angular-material-colors` - Use Angular Material theming with semantic color roles
- `color-dark-mode` - Dark mode uses desaturated / lighter tonal variants, not inverted colors
- `color-accessible-pairs` - Foreground/background pairs must meet 4.5:1 (AA) or 7:1 (AAA)
- `color-not-decorative-only` - Functional color (error red, success green) must include icon/text
- `truncation-strategy` - Prefer wrapping over truncation; when truncating use ellipsis and provide full text via tooltip/expand
- `letter-spacing` - Respect default letter-spacing per platform; avoid tight tracking on body text
- `number-tabular` - Use tabular/monospaced figures for data columns, prices, and timers
- `whitespace-balance` - Use whitespace intentionally to group related items and separate sections

### 7. Animation (MEDIUM)

- `duration-timing` - Use 150–300ms for micro-interactions; complex transitions ≤400ms; avoid >500ms
- `transform-performance` - Use transform/opacity only; avoid animating width/height/top/left
- `angular-animations` - Use native CSS transitions/keyframes with Angular's `animate.enter` / `animate.leave`; the `@angular/animations` package is deprecated, so don't add it to new code
- `loading-states` - Show skeleton or progress indicator when loading exceeds 300ms
- `excessive-motion` - Animate 1-2 key elements per view max
- `easing` - Use ease-out for entering, ease-in for exiting; avoid linear for UI transitions
- `motion-meaning` - Every animation must express a cause-effect relationship, not just be decorative
- `state-transition` - State changes should animate smoothly, not snap
- `continuity` - Page/screen transitions should maintain spatial continuity (shared element, directional slide)
- `parallax-subtle` - Use parallax sparingly; must respect reduced-motion and not cause disorientation
- `spring-physics` - Prefer spring/physics-based curves over linear or cubic-bezier for natural feel
- `exit-faster-than-enter` - Exit animations shorter than enter (~60–70% of enter duration) to feel responsive
- `stagger-sequence` - Stagger list/grid item entrance by 30–50ms per item
- `shared-element-transition` - Use shared element / hero transitions for visual continuity between screens
- `interruptible` - Animations must be interruptible; user tap/gesture cancels in-progress animation immediately
- `no-blocking-animation` - Never block user input during an animation; UI must stay interactive
- `fade-crossfade` - Use crossfade for content replacement within the same container
- `scale-feedback` - Subtle scale (0.95–1.05) on press for tappable cards/buttons
- `gesture-feedback` - Drag, swipe, and pinch must provide real-time visual response tracking the finger
- `hierarchy-motion` - Use translate/scale direction to express hierarchy
- `motion-consistency` - Unify duration/easing tokens globally
- `opacity-threshold` - Fading elements should not linger below opacity 0.2
- `modal-motion` - Modals/sheets should animate from their trigger source for spatial context
- `navigation-direction` - Forward navigation animates left/up; backward animates right/down
- `layout-shift-avoid` - Animations must not cause layout reflow or CLS; use transform for position changes

### 8. Forms & Feedback (MEDIUM)

- `input-labels` - Visible label per input (not placeholder-only)
- `error-placement` - Show error below the related field
- `submit-feedback` - Loading then success/error state on submit
- `required-indicators` - Mark required fields (e.g. asterisk)
- `empty-states` - Helpful message and action when no content
- `toast-dismiss` - Auto-dismiss toasts in 3-5s
- `confirmation-dialogs` - Confirm before destructive actions using Angular Material Dialog
- `input-helper-text` - Provide persistent helper text below complex inputs, not just placeholder
- `disabled-states` - Disabled elements use reduced opacity (0.38–0.5) + cursor change + semantic attribute
- `progressive-disclosure` - Reveal complex options progressively; don't overwhelm users upfront
- `inline-validation` - Validate on blur (not keystroke); show error only after user finishes input
- `input-type-keyboard` - Use semantic input types (email, tel, number) to trigger the correct mobile keyboard
- `password-toggle` - Provide show/hide toggle for password fields
- `autofill-support` - Use autocomplete attributes so the system can autofill
- `undo-support` - Allow undo for destructive or bulk actions (e.g. "Undo delete" toast)
- `success-feedback` - Confirm completed actions with brief visual feedback (checkmark, toast, color flash)
- `error-recovery` - Error messages must include a clear recovery path (retry, edit, help link)
- `multi-step-progress` - Multi-step flows show step indicator or progress bar; allow back navigation
- `form-autosave` - Long forms should auto-save drafts to prevent data loss on accidental dismissal
- `sheet-dismiss-confirm` - Confirm before dismissing a sheet/modal with unsaved changes
- `error-clarity` - Error messages must state cause + how to fix (not just "Invalid input")
- `field-grouping` - Group related fields logically using native `<fieldset>`/`<legend>` (Angular Material has no fieldset component) or visual grouping
- `read-only-distinction` - Read-only state should be visually and semantically different from disabled
- `focus-management` - After submit error, auto-focus the first invalid field (query it with `viewChildren()` or `.ng-invalid` inside the form element)
- `error-summary` - For multiple errors, show summary at top with anchor links to each field
- `touch-friendly-input` - Mobile input height ≥44px to meet touch target requirements
- `destructive-emphasis` - Destructive actions use semantic danger color (red) and are visually separated from primary actions
- `toast-accessibility` - Toasts must not steal focus; use aria-live="polite" for screen reader announcement
- `aria-live-errors` - Form errors use aria-live region or role="alert" to notify screen readers
- `contrast-feedback` - Error and success state colors must meet 4.5:1 contrast ratio
- `timeout-feedback` - Request timeout must show clear feedback with retry option
- `reactive-forms` - Use typed Angular Reactive Forms for complex form validation and dynamic form arrays
- `custom-controls` - Implement `ControlValueAccessor` for custom inputs so they work with forms, validation and `<mat-form-field>`
- `form-state` - Use Angular form state (pristine, dirty, touched, untouched) for styling and validation UX

### 9. Navigation Patterns (HIGH)

- `sidenav-limit` - Sidenav/navigation max 5 primary items; use labels with icons
- `drawer-usage` - Use drawer/sidenav for secondary navigation, not primary actions
- `back-behavior` - Back navigation must be predictable and consistent; preserve scroll/state with Angular Router
- `deep-linking` - All key screens must be reachable via deep link / URL for sharing and notifications
- `tab-bar-ios` - iOS: use bottom Tab Bar for top-level navigation with Angular Router
- `top-app-bar-android` - Android: use Top App Bar with navigation icon for primary structure
- `nav-label-icon` - Navigation items must have both icon and text label
- `nav-state-active` - Current location must be visually highlighted in navigation using routerLinkActive
- `nav-hierarchy` - Primary nav vs secondary nav must be clearly separated
- `modal-escape` - Modals and sheets must offer a clear close/dismiss affordance
- `search-accessible` - Search must be easily reachable (top bar or tab)
- `breadcrumb-web` - Web: use breadcrumbs for 3+ level deep hierarchies using Angular Router
- `state-preservation` - Navigating back must restore previous scroll position, filter state, and input
- `gesture-nav-support` - Support system gesture navigation (iOS swipe-back, Android predictive back) without conflict
- `tab-badge` - Use badges on nav items sparingly to indicate unread/pending; clear after user visits
- `overflow-menu` - When actions exceed available space, use overflow/more menu
- `bottom-nav-top-level` - Bottom nav is for top-level screens only; never nest sub-navigation inside it
- `adaptive-navigation` - Large screens (≥1024px) prefer sidenav; small screens use top nav
- `back-stack-integrity` - Never silently reset the navigation stack or unexpectedly jump to home
- `navigation-consistency` - Navigation placement must stay the same across all pages
- `avoid-mixed-patterns` - Don't mix Tab + Sidenav + Bottom Nav at the same hierarchy level
- `modal-vs-navigation` - Modals must not be used for primary navigation flows
- `focus-on-route-change` - After page transition, move focus to main content region
- `persistent-nav` - Core navigation must remain reachable from deep pages
- `destructive-nav-separation` - Dangerous actions must be visually and spatially separated from normal nav items
- `empty-nav-state` - When a nav destination is unavailable, explain why instead of silently hiding it
- `lazy-routes` - Use lazy loading for routes to improve initial load time

### 10. Charts & Data (LOW)

- `chart-type` - Match chart type to data type (trend → line, comparison → bar, proportion → pie/donut)
- `color-guidance` - Use accessible color palettes; avoid red/green only pairs for colorblind users
- `data-table` - Provide table alternative for accessibility - use Angular Material Table
- `pattern-texture` - Supplement color with patterns, textures, or shapes
- `legend-visible` - Always show legend; position near the chart
- `tooltip-on-interact` - Provide tooltips/data labels on hover (Web) or tap (mobile) showing exact values
- `axis-labels` - Label axes with units and readable scale; avoid truncated or rotated labels on mobile
- `responsive-chart` - Charts must reflow or simplify on small screens
- `empty-data-state` - Show meaningful empty state when no data exists
- `loading-chart` - Use skeleton or shimmer placeholder while chart data loads
- `animation-optional` - Chart entrance animations must respect prefers-reduced-motion
- `large-dataset` - For 1000+ data points, aggregate or sample; provide drill-down for detail
- `number-formatting` - Use locale-aware formatting for numbers, dates, currencies on axes and labels
- `touch-target-chart` - Interactive chart elements must have ≥44×44px tap area or expand on touch
- `no-pie-overuse` - Avoid pie/donut for >5 categories; switch to bar chart for clarity
- `contrast-data` - Data lines/bars vs background ≥3:1; data text labels ≥4.5:1
- `legend-interactive` - Legends should be clickable to toggle series visibility
- `direct-labeling` - For small datasets, label values directly on the chart
- `tooltip-keyboard` - Tooltip content must be keyboard-reachable and not rely on hover alone
- `sortable-table` - Data tables must support sorting with aria-sort indicating current sort state - Angular Material Table sorting
- `axis-readability` - Axis ticks must not be cramped; maintain readable spacing, auto-skip on small screens
- `data-density` - Limit information density per chart to avoid cognitive overload
- `trend-emphasis` - Emphasize data trends over decoration
- `gridline-subtle` - Grid lines should be low-contrast (e.g. gray-200)
- `focusable-elements` - Interactive chart elements must be keyboard-navigable
- `screen-reader-summary` - Provide a text summary or aria-label describing the chart's key insight
- `error-state-chart` - Data load failure must show error message with retry action
- `export-option` - For data-heavy products, offer CSV/image export of chart data
- `drill-down-consistency` - Drill-down interactions must maintain a clear back-path and hierarchy breadcrumb
- `time-scale-clarity` - Time series charts must clearly label time granularity

## How to Use

Search specific domains using the CLI tool below.

---

## Requirements

### 1. The base `ui-ux-pro-max` skill

All commands in this file run the base skill's search script. Install it once in the project (recommended):

```bash
npm install -g ui-ux-pro-max-cli
uipro init --ai claude        # creates .claude/skills/ui-ux-pro-max/
```

Or install it as a Claude Code plugin:

```
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
```

The commands below assume the project install, run from the project root:
`.claude/skills/ui-ux-pro-max/scripts/search.py`.
If it was installed elsewhere, use that path instead: `~/.claude/skills/ui-ux-pro-max/scripts/search.py` for a user-level install, or `${CLAUDE_PLUGIN_ROOT}/.claude/skills/ui-ux-pro-max/scripts/search.py` for the plugin.
If none of these exist, tell the user the base skill is missing and give the install commands above. Meanwhile, use the Quick Reference and the rules in this file without running searches.

### 2. Python 3

The script needs only the Python standard library. Check that Python is installed:

```bash
python3 --version || python --version
```

On Windows, the command is usually `python`, so use `python` instead of `python3` in every command below.

If Python is not installed, install it based on user's OS:

**macOS:**
```bash
brew install python3
```

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt install python3
```

**Windows:**
```powershell
winget install Python.Python.3.12
```

---

## How to Use This Skill

Use this skill when the user requests any of the following:

| Scenario | Trigger Examples | Start From |
|----------|-----------------|------------|
| **New project / page** | "Build a landing page", "Build a dashboard" | Step 1 → Step 2 (design system) |
| **New component** | "Create a pricing card", "Add a modal dialog" | Step 3 (domain search: style, ux) |
| **Choose style / color / font** | "What style fits a fintech app?", "Recommend a color palette" | Step 2 (design system) |
| **Review existing UI** | "Review this page for UX issues", "Check accessibility" | Quick Reference checklist above |
| **Fix a UI bug** | "Button hover is broken", "Layout shifts on load" | Quick Reference → relevant section |
| **Improve / optimize** | "Make this faster", "Improve mobile experience" | Step 3 (domain: ux) → Step 4 (`--stack angular`) |
| **Implement dark mode** | "Add dark mode support" | Step 3 (domain: style "dark mode") |
| **Add charts / data viz** | "Add an analytics dashboard chart" | Step 3 (domain: chart) |
| **Stack best practices** | "Angular performance tips", "Angular CDK navigation" | Step 4 (stack search) |

Follow this workflow:

### Step 1: Analyze User Requirements

Extract key information from user request:
- **Product type**: Entertainment (social, video, music, gaming), Tool (scanner, editor, converter), Productivity (task manager, notes, calendar), or hybrid
- **Target audience**: C-end consumer users; consider age group, usage context (commute, leisure, work)
- **Style keywords**: playful, vibrant, minimal, dark mode, content-first, immersive, etc.
- **Stack**: Angular (this project's tech stack)

### Step 2: Generate Design System (REQUIRED)

**Always start with `--design-system`** to get comprehensive recommendations with reasoning:

```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<product_type> <industry> <keywords>" --design-system [-p "Project Name"]
```

This command:
1. Searches domains in parallel (product, style, color, landing, typography)
2. Applies reasoning rules from `ui-reasoning.csv` to select best matches
3. Returns complete design system: pattern, style, colors, typography, effects
4. Includes anti-patterns to avoid

**Example:**
```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "beauty spa wellness service" --design-system -p "Serenity Spa"
```

### Step 2b: Persist Design System (Master + Overrides Pattern)

To save the design system for **hierarchical retrieval across sessions**, add `--persist`:

```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --design-system --persist -p "Project Name" --output-dir .
```

Always pass `--output-dir` pointing at the Angular project root (`.` when you run from it). An existing `MASTER.md` is not overwritten unless you add `--force`.

This creates (`<project-slug>` is the project name in lowercase with hyphens):
- `design-system/<project-slug>/MASTER.md` — Global Source of Truth with all design rules
- `design-system/<project-slug>/pages/` — Folder for page-specific overrides

**With page-specific override:**
```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --design-system --persist -p "Project Name" --page "dashboard" --output-dir .
```

This also creates:
- `design-system/<project-slug>/pages/dashboard.md` — Page-specific deviations from Master

Optional: add `--tokens css` (or `--tokens dtcg`) to also get design tokens you can map onto Angular Material theme CSS variables. Add `--preview` to write a `preview.html` of the generated system.

**How hierarchical retrieval works:**
1. When building a specific page (e.g., "Checkout"), first check `design-system/<project-slug>/pages/checkout.md`
2. If the page file exists, its rules **override** the Master file
3. If not, use `design-system/<project-slug>/MASTER.md` exclusively

**Context-aware retrieval prompt:**
```
I am building the [Page Name] page in Angular. Please read design-system/<project-slug>/MASTER.md.
Also check if design-system/<project-slug>/pages/[page-name].md exists.
If the page file exists, prioritize its rules.
If not, use the Master rules exclusively.
Now, generate the Angular code...
```

### Step 3: Supplement with Detailed Searches (as needed)

After getting the design system, use domain searches to get additional details:

```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<keyword>" --domain <domain> [-n <max_results>]
```

**When to use detailed searches:**

| Need | Domain | Example |
|------|--------|---------|
| Product type patterns | `product` | `--domain product "entertainment social"` |
| More style options | `style` | `--domain style "glassmorphism dark"` |
| Color palettes | `color` | `--domain color "entertainment vibrant"` |
| Font pairings | `typography` | `--domain typography "playful modern"` |
| Chart recommendations | `chart` | `--domain chart "real-time dashboard"` |
| UX best practices | `ux` | `--domain ux "animation accessibility"` |
| Alternative fonts | `typography` | `--domain typography "elegant luxury"` |
| Individual Google Fonts | `google-fonts` | `--domain google-fonts "sans serif popular variable"` |
| Landing structure | `landing` | `--domain landing "hero social-proof"` |
| Icons with import code | `icons` | `--domain icons "settings navigation outline"` |
| Animation presets | `gsap` | `--domain gsap "scroll reveal stagger"` |

There is no `angular` domain. Angular guidance comes from the `angular` **stack** (Step 4).

### Step 4: Stack Guidelines (Angular)

Get Angular implementation-specific best practices:

```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<keyword>" --stack angular
```

| Need | Example |
|------|---------|
| Performance | `--stack angular "performance zoneless defer signals"` |
| Angular CDK | `--stack angular "cdk harness virtual scroll"` |
| Angular Material | `--stack angular "material theming tokens"` |
| Angular Router | `--stack angular "lazy loading guards resolvers"` |
| Angular Forms | `--stack angular "typed reactive forms validation"` |
| Styling | `--stack angular "host encapsulation tailwind custom properties"` |

---

## Search Reference

### Available Domains

| Domain | Use For | Example Keywords |
|--------|---------|------------------|
| `product` | Product type recommendations | SaaS, e-commerce, portfolio, healthcare, beauty, service |
| `style` | UI styles, colors, effects | glassmorphism, minimalism, dark mode, brutalism |
| `typography` | Font pairings, Google Fonts | elegant, playful, professional, modern |
| `color` | Color palettes by product type | saas, ecommerce, healthcare, beauty, fintech, service |
| `landing` | Page structure, CTA strategies | hero, hero-centric, testimonial, pricing, social-proof |
| `chart` | Chart types, library recommendations | trend, comparison, timeline, funnel, pie |
| `ux` | Best practices, anti-patterns | animation, accessibility, z-index, loading |
| `google-fonts` | Individual Google Fonts lookup | sans serif, monospace, japanese, variable font, popular |
| `icons` | Icon recommendations with import code | settings, navigation, outline, filled |
| `gsap` | Animation skeletons by intensity tier | hover, scroll reveal, stagger, page transition |
`style` and `product` also accept `--rtl` (or `--rtl=full|partial|caveats`) to keep only layouts that work for Arabic, Hebrew, Persian or Urdu interfaces. Example: `--domain style "dashboard" --rtl`.

### Available Stacks

| Stack | Focus |
|-------|-------|
| `angular` | Components, Routing, State (signals, NgRx Signal Store), Forms, Performance, Testing, Styling, Architecture |

---

## Example Workflow

**User request:** "Make an AI search homepage in Angular."

### Step 1: Analyze Requirements
- Product type: Tool (AI search engine)
- Target audience: C-end users looking for fast, intelligent search
- Style keywords: modern, minimal, content-first, dark mode
- Stack: Angular

### Step 2: Generate Design System (REQUIRED)

```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "AI search tool modern minimal" --design-system -p "AI Search"
```

**Output:** Complete design system with pattern, style, colors, typography, effects, and anti-patterns.

### Step 3: Supplement with Detailed Searches (as needed)

```bash
# Get style options for a modern tool product
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "minimalism dark mode" --domain style

# Get UX best practices for search interaction and loading
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "search loading animation" --domain ux

# Get icons for the search UI
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "search filter history" --domain icons
```

### Step 4: Stack Guidelines

```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "component design material theme" --stack angular

# Angular performance for a results list
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "performance signals defer" --stack angular
```

**Then:** Synthesize design system + detailed searches and implement the Angular design.

---

## Output Formats

The `--design-system` flag supports two output formats:

```bash
# ASCII box (default) - best for terminal display
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "fintech crypto" --design-system

# Markdown - best for documentation
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "fintech crypto" --design-system -f markdown
```

---

## Tips for Better Results

### Query Strategy

- Use **multi-dimensional keywords** — combine product + industry + tone + density: `"entertainment social vibrant content-dense"` not just `"app"`
- Try different keywords for the same need: `"playful neon"` → `"vibrant dark"` → `"content-first minimal"`
- Use `--design-system` first for full recommendations, then `--domain` to deep-dive any dimension you're unsure about
- Always finish with `--stack angular` for Angular-specific implementation guidance

### Common Sticking Points

| Problem | What to Do |
|---------|------------|
| Can't decide on style/color | Re-run `--design-system` with different keywords |
| Dark mode contrast issues | Quick Reference §6: `color-dark-mode` + `color-accessible-pairs` |
| Animations feel unnatural | Quick Reference §7: `spring-physics` + `easing` + `exit-faster-than-enter` |
| Form UX is poor | Quick Reference §8: `inline-validation` + `error-clarity` + `focus-management` |
| Navigation feels confusing | Quick Reference §9: `nav-hierarchy` + `sidenav-limit` + `back-behavior` |
| Layout breaks on small screens | Quick Reference §5: `mobile-first` + `breakpoint-consistency` |
| Performance / jank | Quick Reference §3: `virtualize-lists` + `on-push` + `track-in-for` + `defer-below-fold` + `signals` |
| Angular change detection issues | Quick Reference §3: `on-push` + `signals` + `debounce-throttle` |
| Angular Material theming | Quick Reference §4: `angular-material-theme` + `elevation-consistent` |

### Review Process

- Run `--domain ux "animation accessibility z-index loading"` as a UX validation pass before implementation
- Run through Quick Reference **§1–§3** (CRITICAL + HIGH) as a final review
- Test on 375px (small phone) and landscape orientation
- Verify behavior with **reduced-motion** enabled and browser text zoom at 200%
- Check dark mode contrast independently (don't assume light mode values work)
- Confirm all touch targets ≥44×44px and no content hidden behind safe areas
- Finish with the [Pre-Delivery Checklist](#pre-delivery-checklist) at the end of this file

---

## Common Rules for Professional Angular UI

These are frequently overlooked issues that make Angular UI look unprofessional:

### Icons & Visual Elements

| Rule | Standard | Avoid | Why It Matters |
|------|----------|--------|----------------|
| **No Emoji as Structural Icons** | Use vector-based icons (e.g., Material Icons, Lucide, Heroicons via icon components). | Using emojis (🎨 🚀 ⚙️) for navigation, settings, or system controls. | Emojis are font-dependent, inconsistent across platforms, and cannot be controlled via design tokens. |
| **Vector-Only Assets** | Use SVG or platform vector icons that scale cleanly and support theming via Angular Material Icon | Raster PNG icons that blur or pixelate. | Ensures scalability, crisp rendering, and dark/light mode adaptability. |
| **Stable Interaction States** | Use color, opacity, or elevation transitions for press states without changing layout bounds. | Layout-shifting transforms that move surrounding content or trigger visual jitter. | Prevents unstable interactions and preserves smooth motion/perceived quality on mobile. |
| **Correct Brand Logos** | Use official brand assets and follow their usage guidelines (spacing, color, clear space). | Guessing logo paths, recoloring unofficially, or modifying proportions. | Prevents brand misuse and ensures legal/platform compliance. |
| **Consistent Icon Sizing** | Define icon sizes as design tokens (e.g., icon-sm = 16px, icon-md = 24px, icon-lg = 32px). | Picking sizes ad hoc per component (20px here, 22px there, 28px elsewhere). | Maintains rhythm and visual hierarchy across the interface. |
| **Stroke Consistency** | Use a consistent stroke width within the same visual layer (e.g., 1.5px or 2px). | Mixing thick and thin stroke styles arbitrarily. | Inconsistent strokes reduce perceived polish and cohesion. |
| **Filled vs Outline Discipline** | Use one icon style per hierarchy level. | Mixing filled and outline icons at the same hierarchy level. | Maintains semantic clarity and stylistic coherence. |
| **Touch Target Minimum** | Minimum 44×44px interactive area (expand with padding or a `::before` hit area; `mat-icon-button` already gives 48×48px). | Small icons without expanded tap area. | Meets accessibility and platform usability standards. |
| **Icon Alignment** | Align icons to text baseline and maintain consistent padding. | Misaligned icons or inconsistent spacing around them. | Prevents subtle visual imbalance that reduces perceived quality. |
| **Icon Contrast** | Follow WCAG contrast standards: 4.5:1 for small elements, 3:1 minimum for larger UI glyphs. | Low-contrast icons that blend into the background. | Ensures accessibility in both light and dark modes. |

### Interaction (Angular)

| Rule | Do | Don't |
|------|----|----- |
| **Tap feedback** | Start pressed feedback (ripple/opacity/elevation) within 100ms using Angular Material ripple (`matRipple`) | No visual response on tap |
| **Animation timing** | Keep micro-interactions around 150-300ms using CSS transitions with `animate.enter`/`animate.leave` and native easing | Instant transitions or slow animations (>500ms) |
| **Accessibility focus** | Ensure screen reader focus order matches visual order, use Angular CDK a11y, labels are descriptive | Unlabeled controls or confusing focus traversal |
| **Disabled state clarity** | Use `disabled` attribute, `aria-disabled`, reduced emphasis, and no tap action | Controls that look tappable but do nothing |
| **Touch target minimum** | Keep tap areas >=44x44px, expand hit area when icon is smaller using padding | Tiny tap targets or icon-only hit areas without padding |
| **Gesture conflict prevention** | Keep one primary gesture per region and avoid nested tap/drag conflicts | Overlapping gestures causing accidental actions |
| **Angular Material Primitives** | Prefer Angular Material components (`<button mat-button>`, `<input matInput>`) with proper accessibility roles | Generic HTML elements used as primary controls without Angular Material wrappers |
| **Change Detection** | Drive frequently updating UI with Signals; use OnPush where input-driven subtrees can be skipped | Mutable class fields and manual `detectChanges()` calls to force updates |

### Light/Dark Mode Contrast

| Rule | Do | Don't |
|------|----|-----|
| **Surface readability (light)** | Keep cards/surfaces clearly separated from background with sufficient opacity/elevation | Overly transparent surfaces that blur hierarchy |
| **Text contrast (light)** | Maintain body text contrast >=4.5:1 against light surfaces | Low-contrast gray body text |
| **Text contrast (dark)** | Maintain >=4.5:1 for all body-size text, primary and secondary (3:1 only for large text ≥24px, or ≥18.66px bold) on dark surfaces | Dark mode text that blends into background |
| **Border and divider visibility** | Ensure separators are visible in both themes (not just light mode) | Theme-specific borders disappearing in one mode |
| **State contrast parity** | Keep pressed/focused/disabled states equally distinguishable in light and dark themes | Defining interaction states for one theme only |
| **Token-driven theming** | Use Angular Material theming with semantic color tokens mapped per theme across app surfaces/text/icons | Hardcoded per-screen hex values |
| **Scrim and modal legibility** | Use a modal scrim strong enough to isolate foreground content (typically 40-60% black) | Weak scrim that leaves background visually competing |

### Layout & Spacing

| Rule | Do | Don't |
|------|----|----- |
| **Safe-area compliance** | Respect top/bottom safe areas for all fixed headers, tab bars, and CTA bars using CSS env() | Placing fixed UI under notch, status bar, or gesture area |
| **System bar clearance** | Add spacing for status/navigation bars and gesture home indicator | Let tappable content collide with OS chrome |
| **Consistent content width** | Keep predictable content width per device class (phone/tablet) | Mixing arbitrary widths between screens |
| **8px spacing rhythm** | Use a consistent 4/8px spacing system for padding/gaps/section spacing | Random spacing increments with no rhythm |
| **Readable text measure** | Keep long-form text readable on large devices (avoid edge-to-edge paragraphs on tablets) | Full-width long text that hurts readability |
| **Section spacing hierarchy** | Define clear vertical rhythm tiers (e.g., 16/24/32/48) by hierarchy | Similar UI levels with inconsistent spacing |
| **Adaptive gutters by breakpoint** | Increase horizontal insets on larger widths and in landscape using Angular CDK BreakpointObserver | Same narrow gutter on all device sizes/orientations |
| **Scroll and fixed element coexistence** | Add bottom/top content insets so lists are not hidden behind fixed bars | Scroll content obscured by sticky headers/footers |
| **Responsive Grid** | Use CSS Grid/Flexbox (or Tailwind) for responsive layouts | Fixed pixel widths that don't adapt, or the deprecated Angular Flex Layout (`fxLayout`) |
| **RTL mirroring** | Use logical properties (`padding-inline-start`) and set `dir` so CDK/Material components mirror | Hardcoded `left`/`right` margins and icons that don't flip in RTL |

### Angular-Specific Patterns

| Rule | Do | Don't |
|------|----|----- |
| **Standalone Components** | Use standalone components (the default; no `standalone: true` needed) | New `NgModule` declarations |
| **Component APIs** | Use `input()`, `output()` and `model()` | `@Input()` / `@Output()` with `EventEmitter` in new components |
| **Lazy Loading** | Use `loadChildren` or `loadComponent` for lazy loaded routes | Eagerly loading all routes upfront |
| **OnPush Change Detection** | Use OnPush where input-driven subtrees can be skipped; keep components zoneless-ready | Relying on Zone.js to catch mutations of plain class fields |
| **Track in @for** | Always give `@for` a stable key: `@for (item of items(); track item.id)` | `track $index` for lists that reorder, insert or delete |
| **Signals for State** | Use Angular Signals for component-level reactive state | Overusing observables where signals suffice |
| **ControlValueAccessor** | Implement CVA for custom form controls | Bypassing Angular form architecture |
| **Semantic Templates** | Use built-in control flow (`@if`, `@for`, `@switch`) with semantic HTML and `<ng-container>` | `*ngIf` / `*ngFor` in new code, or div soup |
| **Deferred Content** | Use `@defer (on viewport)` with a same-size `@placeholder` for heavy below-the-fold widgets | Loading charts and editors in the initial bundle |
| **Optimized Images** | Use `NgOptimizedImage` (`ngSrc`, `width`/`height`, `priority` on the LCP image) | Plain `<img>` with no dimensions, causing layout shift |
| **Animations** | Use CSS with `animate.enter` / `animate.leave` | Adding the deprecated `@angular/animations` package to new code |

---

## Pre-Delivery Checklist

Before delivering Angular UI code, verify these items:

### Visual Quality
- [ ] No emojis used as icons (use SVG/Material Icons instead)
- [ ] All icons come from a consistent icon family and style
- [ ] Official brand assets are used with correct proportions and clear space
- [ ] Pressed-state visuals do not shift layout bounds or cause jitter
- [ ] Semantic theme tokens are used consistently (no ad-hoc per-screen hardcoded colors)
- [ ] Angular Material theme is cohesive across components

### Interaction
- [ ] All tappable elements provide clear pressed feedback (ripple/opacity/elevation)
- [ ] Touch targets meet minimum size (>=44x44px)
- [ ] Micro-interaction timing stays in the 150-300ms range with native-feeling easing
- [ ] Disabled states are visually clear and non-interactive
- [ ] Screen reader focus order matches visual order, and interactive labels are descriptive
- [ ] Gesture regions avoid nested/conflicting interactions (tap/drag/back-swipe conflicts)
- [ ] Angular Material ripple effect is applied to interactive elements

### Light/Dark Mode
- [ ] Primary and secondary body text contrast >=4.5:1 in both light and dark mode (3:1 only for large text)
- [ ] Dividers/borders and interaction states are distinguishable in both modes
- [ ] Modal/drawer scrim opacity is strong enough to preserve foreground legibility (typically 40-60% black)
- [ ] Both themes are tested before delivery (not inferred from a single theme)
- [ ] Angular Material dark theme is properly configured

### Layout
- [ ] Safe areas are respected for headers, tab bars, and bottom CTA bars
- [ ] Scroll content is not hidden behind fixed/sticky bars
- [ ] Verified on small phone, large phone, and tablet (portrait + landscape)
- [ ] Horizontal insets/gutters adapt correctly by device size and orientation
- [ ] 4/8px spacing rhythm is maintained across component, section, and page levels
- [ ] Long-form text measure remains readable on larger devices (no edge-to-edge paragraphs)
- [ ] CSS Grid/Flexbox (not the deprecated Angular Flex Layout) is used for responsive behavior
- [ ] Layout mirrors correctly with `dir="rtl"` if the app supports RTL languages

### Angular Performance
- [ ] OnPush change detection is used where appropriate
- [ ] Every `@for` has a stable `track` expression
- [ ] Heavy below-the-fold content uses `@defer`, and images use `NgOptimizedImage`
- [ ] Lazy loading is implemented for feature routes
- [ ] Signals are used for fine-grained reactivity
- [ ] Virtual scrolling is used for lists with 50+ items
- [ ] No unnecessary re-renders detected

### Accessibility
- [ ] All meaningful images/icons have accessibility labels
- [ ] Form fields have labels, hints, and clear error messages
- [ ] Color is not the only indicator
- [ ] Reduced motion and 200% browser text zoom are supported without layout breakage
- [ ] Angular CDK a11y is used for focus trapping, live announcer, etc.
- [ ] Accessibility traits/roles/states (selected, disabled, expanded) are announced correctly
