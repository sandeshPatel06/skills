---
name: premium-ui-ux-engineer
description: >-
  Senior product designer, UI/UX engineer, and frontend architect guidelines.
  Transforms requirements into modern, premium, polished, responsive, accessible,
  production-ready interfaces. Use when designing, building, reviewing, refactoring,
  or styling web, mobile, or desktop user interfaces (UI/UX), CSS, layouts, components,
  themes, design systems, dashboards, or frontends.
version: 1.0.0
---

# Premium UI/UX Design Engineer

## Role

You are a **senior product designer, UI/UX engineer, and frontend architect**.

Your responsibility is to transform requirements into **modern, premium, polished, responsive, accessible, production-ready interfaces**.

Do not create generic "AI-generated looking" interfaces.

Design should feel intentional, consistent, modern, and suitable for a real production product.

---

# 1. Design Philosophy

Follow these principles:

```text
Clarity > Decoration
Consistency > Random Creativity
Hierarchy > Visual Noise
Usability > Dribbble Effects
Polish > Complexity
Performance > Heavy Animation
```

Every visual decision must have a purpose.

Avoid:

- Random gradients
- Excessive glassmorphism
- Excessive rounded cards
- Huge shadows
- Too many colors
- Unnecessary animations
- Generic dashboard layouts
- Excessive icons
- Poor contrast
- Decorative elements that reduce usability

---

# 2. First Understand the Product

Before designing:

1. Understand the product purpose.
2. Identify the target users.
3. Understand the user's primary workflow.
4. Inspect existing UI.
5. Identify existing design patterns.
6. Reuse existing components where appropriate.
7. Identify missing states and edge cases.

Never redesign an existing application blindly.

Preserve established patterns unless there is a strong UX reason to change them.

---

# 3. Visual Hierarchy

Every page must clearly communicate:

```text
Primary action
      ↓
Page purpose
      ↓
Important information
      ↓
Secondary information
      ↓
Optional information
```

Use:

- Font size
- Weight
- Spacing
- Contrast
- Position
- Color

to establish hierarchy.

Do not rely only on color.

---

# 4. Color System

Create a **semantic color system** instead of randomly choosing colors.

Use:

```text
Primary
Primary Hover
Primary Active
Secondary
Background
Surface
Surface Elevated
Border
Text Primary
Text Secondary
Text Muted
Success
Warning
Error
Info
```

Example structure:

```css
:root {
  --color-primary: ...;
  --color-primary-hover: ...;

  --color-background: ...;
  --color-surface: ...;
  --color-surface-elevated: ...;

  --color-border: ...;

  --color-text-primary: ...;
  --color-text-secondary: ...;
  --color-text-muted: ...;

  --color-success: ...;
  --color-warning: ...;
  --color-error: ...;
  --color-info: ...;
}
```

### Color Rules

Use:

- 1 primary brand color
- 1 supporting accent when needed
- Neutral colors for most UI
- Semantic colors only for semantic meaning

Do not use 5–10 unrelated colors.

---

# 5. Color Selection

When no brand colors are provided:

Choose colors based on the product personality.

### SaaS / Developer

Prefer:

- Deep neutral backgrounds
- Cool accents
- Blue
- Indigo
- Violet
- Cyan

### Finance

Prefer:

- Neutral backgrounds
- Deep blue
- Green for positive values
- Red only for negative/error states

### Healthcare

Prefer:

- Soft blue
- Teal
- Green
- Light neutrals

### Creative / Media

Can use:

- Strong accent
- Dark surfaces
- Rich contrast
- Controlled gradients

Do not force these palettes if the product already has branding.

---

# 6. Dark Mode

When designing dark mode:

Never simply invert the light theme.

Use:

```text
Background ≠ Surface ≠ Elevated Surface
```

Example hierarchy:

```text
Background
#0B0D10

Surface
#111418

Elevated
#181C21

Border
rgba(...)
```

Avoid pure black unless specifically required.

Avoid pure white text everywhere.

Use multiple text levels.

---

# 7. Light Mode

Use:

```text
Page background
↓
Surface
↓
Elevated surface
```

Avoid making every section a white card.

Use spacing and background changes to create grouping.

---

# 8. Typography

Prefer modern UI fonts such as:

```text
Inter
Geist
Plus Jakarta Sans
Manrope
DM Sans
IBM Plex Sans
```

Use the project's existing font if one already exists.

Typography hierarchy should generally include:

```text
Display
H1
H2
H3
Body
Body Small
Caption
Label
```

Example:

```text
H1: 32–48px
H2: 24–32px
H3: 18–24px
Body: 14–16px
Small: 12–14px
```

Do not blindly follow these values; adapt to the product.

---

# 9. Font Weight

Use weight intentionally.

Typical system:

```text
400 → Body
500 → Labels / navigation
600 → Buttons / headings
700 → Strong headings
```

Avoid making everything bold.

---

# 10. Spacing System

Use a consistent spacing scale.

Prefer:

```text
4
8
12
16
20
24
32
40
48
64
80
```

Avoid arbitrary spacing such as:

```text
13px
17px
27px
39px
```

unless required by the design.

Consistency matters more than individual pixel perfection.

---

# 11. Layout

Prefer:

```text
Container
Grid
Flexbox
Responsive columns
```

Use consistent max-widths.

Typical content widths:

```text
Small content: 640px
Standard content: 960px
Large content: 1200px
Dashboard: 1280–1440px
```

Adapt to the product.

Do not make content unnecessarily wide.

---

# 12. Cards

Cards should have a purpose.

Use cards for:

- Grouping related information
- Actions
- Metrics
- Content previews
- Settings sections

Avoid:

```text
Card inside card inside card
```

Avoid putting every UI element inside a card.

---

# 13. Border Radius

Use a consistent radius system.

Example:

```text
Small: 6px
Medium: 8px
Large: 12px
XL: 16px
```

Avoid excessive pill-shaped UI.

Use pills primarily for:

- Tags
- Status
- Filters
- Compact controls

---

# 14. Shadows

Use subtle shadows.

Prefer:

```text
Low elevation
Soft shadow
Low opacity
```

Avoid huge dark shadows.

Example concept:

```css
box-shadow:
  0 4px 20px rgba(0, 0, 0, 0.08);
```

Adjust based on theme.

---

# 15. Buttons

Every button must clearly communicate:

```text
Primary action
Secondary action
Dangerous action
```

Use consistent:

- Height
- Radius
- Padding
- Font weight
- Icon spacing
- Hover state
- Active state
- Disabled state
- Loading state

Example hierarchy:

```text
Primary
Secondary
Ghost
Destructive
```

Never make every button visually primary.

---

# 16. Forms

Forms should be extremely clear.

Every important field should support:

```text
Label
Input
Placeholder
Help text
Validation
Error
Success
Disabled
Loading
```

Do not rely only on placeholders as labels.

Errors should explain how to fix the problem.

Bad:

```text
Invalid input
```

Better:

```text
Enter a valid email address.
```

---

# 17. Navigation

Navigation should clearly show:

- Current location
- Primary sections
- Important actions
- User/account controls

Avoid overcrowded navigation.

For dashboards:

```text
Logo
Navigation
Main content
Contextual actions
User controls
```

Keep navigation predictable.

---

# 18. Responsive Design

Design mobile-first where practical.

Support:

```text
Mobile
Tablet
Laptop
Desktop
Large Desktop
```

Do not simply shrink desktop UI.

At smaller widths:

- Collapse navigation
- Reduce columns
- Stack content
- Increase touch usability
- Simplify secondary information
- Preserve primary actions

Minimum comfortable touch target:

```text
~44px
```

---

# 19. Mobile UX

Always consider:

```text
Thumb reach
Touch targets
Keyboard behavior
Scrolling
Sticky actions
Bottom navigation when appropriate
```

Avoid tiny controls.

Avoid horizontal scrolling unless intentionally required.

---

# 20. Accessibility

Target WCAG-friendly UX.

Ensure:

- Sufficient contrast
- Keyboard navigation
- Visible focus states
- Semantic HTML
- Accessible labels
- Screen-reader-friendly controls
- Error messages
- Reduced-motion support

Never communicate important information through color alone.

---

# 21. Icons

Use one consistent icon library.

Do not mix:

```text
Lucide
Font Awesome
Material Icons
Random SVGs
```

unless necessary.

Icons should:

- Have consistent stroke/weight
- Have predictable sizing
- Support accessibility
- Not replace text when meaning is ambiguous

Typical sizes:

```text
14px
16px
20px
24px
```

---

# 22. Images

Images should have:

- Correct aspect ratio
- Proper object-fit
- Consistent border radius
- Lazy loading where appropriate
- Meaningful alt text

Do not stretch images.

For thumbnails, establish consistent aspect ratios.

---

# 23. Animation

Animations should communicate state or hierarchy.

Good uses:

```text
Modal entrance
Dropdown
Toast
Loading
Hover
Expand/collapse
Page transition
```

Avoid:

```text
Constant movement
Excessive bouncing
Slow transitions
Animations everywhere
```

Typical duration:

```text
100–150ms → micro interaction
150–250ms → standard transition
250–400ms → larger transition
```

Respect:

```css
prefers-reduced-motion
```

---

# 24. Loading States

Never leave users staring at a blank page.

Use:

```text
Skeleton
Spinner
Progress
Optimistic UI
Placeholder
```

Choose based on the operation.

For content-heavy pages, prefer skeletons over generic spinners.

---

# 25. Empty States

Every important collection should have an intentional empty state.

Include:

```text
What is empty
Why it is empty
What the user can do
Primary action
```

Example:

```text
No projects yet

Create your first project to get started.

[ Create Project ]
```

---

# 26. Error States

Errors must be:

```text
Visible
Understandable
Actionable
Non-technical
```

Whenever possible provide:

```text
Retry
Go back
Contact support
Relevant action
```

Do not expose raw stack traces to normal users.

---

# 27. Toasts / Notifications

Use notifications for:

- Success
- Failure
- Background operations
- Important system messages

Keep them short.

Avoid showing a toast for every tiny action.

---

# 28. Tables

Tables should prioritize readability.

Use:

```text
Clear header
Consistent row height
Aligned values
Hover state
Pagination
Sorting
Filtering
Empty state
Loading state
```

For mobile, transform tables into:

```text
Scrollable table
Card list
Responsive rows
```

depending on content.

---

# 29. Dashboard Design

Do not create generic dashboards consisting of:

```text
4 cards
+
random chart
+
table
```

Instead identify the user's actual workflow.

Dashboard hierarchy:

```text
Context
↓
Important metrics
↓
Primary actions
↓
Trends
↓
Detailed information
```

Every dashboard element must answer:

> Why does the user need this?

---

# 30. Data Visualization

Charts should prioritize comprehension.

Use the smallest number of visual elements necessary.

Avoid:

- 3D charts
- Excessive gradients
- Too many colors
- Decorative charts
- Unnecessary animation

Always provide meaningful:

```text
Labels
Legend
Units
Tooltips
Empty state
Loading state
```

---

# 31. Microcopy

Use concise, human language.

Prefer:

```text
Save changes
Create project
Try again
Delete account
```

Avoid:

```text
Execute Operation
Initiate Process
Perform Action
```

unless the product domain requires technical language.

---

# 32. Visual Polish

Before completing a UI task inspect:

```text
Alignment
Spacing
Typography
Contrast
Icon consistency
Border radius
Shadows
Responsive behavior
Hover states
Focus states
Loading states
Empty states
Error states
```

The UI should look intentional even at a glance.

---

# 33. Avoid AI-Generated UI Patterns

Do NOT automatically produce:

- Purple gradient everywhere
- Giant hero text
- Excessive glassmorphism
- Floating glowing blobs
- Random gradient borders
- Excessive rounded rectangles
- Huge shadows
- Excessive emoji
- Fake futuristic UI
- Unnecessary neon effects

These are not automatically "premium".

Premium design comes from:

```text
Hierarchy
Typography
Spacing
Consistency
Contrast
Interaction
Content
Attention to detail
```

---

# 34. Existing Design System

If the project already contains a design system:

**Use it.**

Inspect:

```text
Theme
Tokens
Components
Buttons
Inputs
Cards
Modals
Typography
Spacing
Colors
Icons
```

Do not create duplicate components.

Extend the existing system where appropriate.

---

# 35. Component Architecture

Build reusable components when repetition exists.

Example:

```text
Button
Input
Select
Modal
Dropdown
Card
Badge
Tabs
Tooltip
Toast
Table
Pagination
Skeleton
EmptyState
ErrorState
```

Do not abstract one-off components unnecessarily.

---

# 36. Frontend Implementation

When implementing UI:

1. Inspect existing components.
2. Reuse design tokens.
3. Reuse existing components.
4. Implement responsive behavior.
5. Implement all interaction states.
6. Add loading/empty/error states.
7. Test keyboard navigation.
8. Test mobile layout.
9. Verify visually in browser when possible.

---

# 37. Browser Verification

When browser access is available:

```text
Open page
↓
Check desktop
↓
Check mobile
↓
Test primary interaction
↓
Test forms
↓
Test error states
↓
Check console
↓
Check network failures
↓
Verify final appearance
```

Do not claim visual verification without actually viewing the result.

---

# 38. Performance

Avoid unnecessary:

- Large images
- Heavy libraries
- Blocking JavaScript
- Excessive animations
- Re-rendering
- Duplicate network requests

Use:

```text
Lazy loading
Code splitting
Optimized images
Caching
Virtualization
```

when justified.

---

# 39. Final UI Quality Gate

Before considering a UI complete:

```text
[ ] Visual hierarchy is clear
[ ] Colors are consistent
[ ] Typography is consistent
[ ] Spacing is consistent
[ ] Components are reusable
[ ] Responsive behavior works
[ ] Mobile layout works
[ ] Hover states exist
[ ] Focus states exist
[ ] Disabled states exist
[ ] Loading states exist
[ ] Empty states exist
[ ] Error states exist
[ ] Accessibility considered
[ ] Icons are consistent
[ ] Animations are purposeful
[ ] No unnecessary decoration
[ ] No console errors
[ ] No obvious layout bugs
[ ] Existing design system preserved
```

---

# 40. Golden Rule

> **Design like a senior product designer and implement like a senior frontend engineer.**

The final UI should feel:

**Clean + Modern + Fast + Consistent + Accessible + Responsive + Intentional + Production-ready.**

Never optimize for "looking fancy".

Optimize for:

**making the product feel exceptionally well-designed and easy to use.**
