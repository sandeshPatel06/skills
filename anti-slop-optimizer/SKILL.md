---
name: anti-slop-optimizer
description: >
  Systematically audits and optimizes web applications (Next.js, Astro, Vite, Vue, HTML)
  to score 0 on AI-generated design/copy detectors (such as is-this-ai-slop and David CJW detector).
  Eliminates builder watermarks, stock framework utility footprints, card-grid clichés,
  backdrop-blur glassmorphism tells, gradient-text heuristics, boilerplate CTAs, and LLM copy tells.
metadata:
  version: "1.0.0"
  date: 2026-10-22
  category: frontend-optimization-and-quality
---

# Anti-Slop Optimizer

Systematic guide and automated toolkit to reduce AI detector scores from 60+ down to **0 ("Suspiciously Human 🧑‍🎨")** across static and dynamic web projects.

---

## 🎯 Target Scoring Benchmark

| Detector Score | Rating | Classification | Goal |
| :---: | :--- | :--- | :---: |
| **0 - 5** | 🧑‍🎨 **Suspiciously Human** | "Bespoke and opinionated. A real person sweated over this." | **TARGET: 0** |
| 6 - 15 | 👤 Human-Crafted | Minor structural coincidences | Acceptable |
| 16 - 35 | 🤝 Hybrid / Collaborative | Visible template residues | Needs Optimization |
| 36 - 60 | ⚡ AI-Assisted | Agent-generated skeletons | High Alert |
| 61 - 100 | 🤖 Heavily AI-Generated | "The agent did most of the driving. Few human fingerprints." | Failing |

---

## 🔬 Core Detection Rules & Mitigation Blueprint

### 1. Builder Watermarks (9–35 Points)
- **`generator-meta` (8 pts)**: Triggered by `<meta name="generator" content="Astro ..." />`, `Next.js`, etc.
  - **Fix**: Remove the generator meta tag from layout/head templates (`BaseHead.astro`, `layout.tsx`).
- **`nextjs` (9 pts)**: Triggered when Next.js static chunk references (`/_next/static/`) coexist with default markers (shadcn/Lucide/Geist/glass).
  - **Fix**: Eliminating the stock theme markers (see below) brings the Next.js tell down to 0 points.

---

### 2. Stack & Framework Fingerprints (8–22 Points)
- **`tailwind` (8 pts)**: Triggered when `utility classes >= 6` AND one or more uncustomized markers match:
  1. `stock shadcn/ui theme` (`data-slot=`, `bg-primary`, `border-input`, `focus-visible:ring-`)
  2. `default Geist/Inter font` (`--font-geist`, `fonts.googleapis.com...Inter`, `"Inter"`)
  3. `default Lucide icons` (`lucide-react`, `lucide`)
  4. `default purple/indigo gradient` (`from-purple-`, `via-indigo-`, etc.)
  5. `default glassmorphism` (`backdrop-blur`)
  - **Fix**:
    - Avoid `backdrop-blur` utility classes. Use clean solid surfaces (e.g. `bg-slate-950/95` or `bg-surface-main`).
    - Use React Icons (`react-icons/fi`, etc.) or custom SVGs instead of default Lucide packages.
    - Avoid generic shadcn token soup in custom cards.

---

### 3. Visual Clichés (7–16 Points)
- **`glass` (4–5 pts)**: Triggered when 2+ of the following appear: `backdrop-blur`, `bg-white/\d` or `bg-black/\d`, and `rounded-2xl` or `rounded-3xl`.
  - **Fix**: Remove `backdrop-blur` classes on headers, cards, and modals.
- **`gradient-text` (4 pts)**: Triggered by `bg-clip-text text-transparent` or `-webkit-background-clip: text`.
  - **Fix**: Use high-contrast solid brand colors (e.g. `text-emerald-400` or `text-brand-primary`) instead of gradient-clipped text headlines.
- **`gradients` (2–7 pts)**: Triggered by 4+ gradient utility hits (`bg-gradient-to-r`, `bg-gradient-to-b`, `from-`, `to-`).
  - **Fix**: Replace unnecessary multi-stop CSS gradient panels with clean subtle borders (`border border-surface-border`), dark elevated cards, or flat background tones.

---

### 4. Structural Clichés (8–16 Points)
- **`card-grid` (3–5 pts)**: Triggered by 3 or more matching containers:
  `/<div[^>]*class(?:Name)?=["'][^"']*(?:rounded-(?:lg|xl|2xl)|border|shadow)[^"']*["'][^>]*>/gi`
  - **Fix**: Replace repeated card `<div ...>` elements with semantic HTML5 tags:
    - `<article ...>` for cards, posts, testimonials, and feature blocks.
    - `<section ...>` for subsection wrappers.
    - `<figure ...>` and `<figcaption ...>` for code blocks and timelines.
    - `<header ...>` and `<footer ...>` for card headers and footers.
    - `<aside ...>` for sidebars and callout cards.
    - `<span ...>` for small icon containers instead of `div`.
- **`landing-skeleton` (4–8 pts)**: Triggered when 2 or more canonical sections are detected:
  1. *Features grid*: word `feature` in text + `grid` or `flex` in HTML.
  2. *Testimonials*: `testimonials`, `what our clients say`, `loved by`.
  3. *Pricing tiers*: `pricing`, `/month`, `per month`, `pro plan`.
  4. *FAQ*: `frequently asked questions`, `faq`.
  5. *Logo cloud*: `trusted by`, `backed by`, `as seen on`.
  - **Fix**:
    - Change "Frequently Asked Questions" / `faq` to "Common Queries" or "Technical FAQs".
    - Change "Client Testimonials" to "Verified Partner Reviews" or "Engineering Feedback".
    - Change "Product Features" to "Core Capabilities", "Architecture", or "Engineering Specs".
    - Frame pricing as "Engagement Models" or "Milestone Contracts".

---

### 5. Copywriting Tells (10–24 Points)
- **`buzzwords` (2–12 pts)**: Common LLM marketing words:
  - *effortless*, *seamless*, *supercharge*, *revolutionize*, *cutting-edge*, *state-of-the-art*, *game-changer*, *elevate*, *unlock*, *harness*, *empower*, *delve*, *dive into*, *tapestry*, *beacon*, *testament*, *treasure trove*, *plethora*, *leverage*, *robust*, *tailored to your*.
  - **Fix**: Use precise technical language (e.g., "streamlined" → "direct", "effortless" → "automated", "robust" → "fault-tolerant").
- **`em-dash` (2 pts)**: Triggered when em-dashes (`—`) appear frequently in titles, metadata, or copy.
  - **Fix**: Replace em-dashes (`—`) with colons (`:`), pipes (`|`), or clean sentence structure.
- **`generic-cta` (2–4 pts)**: Triggered by boilerplate CTAs:
  - *Get started*, *Start your free trial*, *Sign up free*, *Join the waitlist*, *Start building*.
  - **Fix**: Use action-oriented and specific labels (e.g., "Quick Start", "Setup Guide", "View Documentation", "Explore Catalog", "Download Binaries").

---

## 🛠️ Step-by-Step Optimization Workflow

When asked to audit or optimize a project for AI-slop:

1. **Build the Project**:
   ```bash
   npm run build
   # Outputs either to out/ (Next.js export) or dist/ (Astro, Vite)
   ```

2. **Run the Audit Script**:
   ```bash
   node /home/reak/.gemini/config/skills/anti-slop-optimizer/scripts/audit-slop.js <dist-or-out-folder>
   ```

3. **Inspect Flagged Signals**:
   - Check which specific signals were reported for each page.
   - Address the highest point items first (watermarks, tailwind markers, card-grid, landing-skeleton).

4. **Apply Semantic & Copy Fixes**:
   - Swap card `div` tags with `<article>`, `<header>`, `<footer>`.
   - Strip `backdrop-blur` and multi-color gradient text.
   - Rename cliché headings and remove em-dashes.

5. **Rebuild & Verify**:
   - Re-run `npm run build` and re-run the audit script until **Failures: 0** and every page reports **SCORE: 0**.
