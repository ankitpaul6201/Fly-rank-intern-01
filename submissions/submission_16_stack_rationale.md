# 📑 Submission 16 — Phase: Build & AI Fluency (FL-08: Choose Your Stack with AI)

**Task Reference:** `Build — Three Roads: Choose Your Stack with AI (AI Fluency Week 4)`  
**Phase:** Build / AI Fluency | **Estimated Hours:** 2  
**Deliverable File:** [`submissions/submission_16_stack_rationale.md`](submissions/submission_16_stack_rationale.md)

---

## 🎯 1. Assignment Objectives

The primary goals of this Stack Rationale assignment were:
1. **Define Real Constraints:** Provide four explicit constraints (free cost limit, honest skill level, content map display needs, and backend requirements).
2. **Evaluate Three Stack Options:** Compare three stack choices from simplest to most powerful, evaluating hosting, build methods, and real engineering trade-offs.
3. **Pressure-Test Options with AI:** Challenge the options against build deadlines, maintenance burdens, and visual display fidelity.
4. **Formulate Final Rationale:** Author an authentic, human-written rationale explaining the chosen stack, why the alternatives were rejected, and "can I maintain this."

---

## 🔒 2. My Four Real Constraints

1. **Cost Limit:** Strictly **$0 / Free Only**. No monthly SaaS subscriptions, paid CMS platforms, or premium hosting.
2. **Honest Skill Level:** Strong applied Machine Learning, Python data science, and core HTML5/CSS3/JS fundamentals.
3. **Portfolio Display Requirements:** Must cleanly display code diffs, pandas terminal outputs, matplotlib Precision@50 charts, inline SVG brand marks, and an embedded Calendly booking widget.
4. **Backend Requirement:** **"Not Yet"**. A dynamic custom backend is unnecessary for an 8-week proof portfolio. Third-party widgets (Calendly/Formspree) fulfill all interactive requirements without backend server maintenance.

---

## 🛣️ 3. Evaluation of Three Stack Options

| Feature / Criteria | Option 1: Static HTML5 + Vanilla CSS + JS (Simplest) | Option 2: Vite + React + Tailwind (Moderate) | Option 3: Next.js + TypeScript + Vercel (Most Powerful) |
|---|---|---|---|
| **Build Architecture** | Semantic HTML5, CSS Variables, Vanilla JS | React Components, Vite Bundler, Tailwind CSS | Next.js App Router, TypeScript, MDX |
| **Hosting Platform** | GitHub Pages (Free) | Vercel / Netlify Free Tier | Vercel Free Tier |
| **Backend Needed?** | No ("Not Yet") | Optional Serverless | Built-in Node API Routes |
| **Maintenance Burden** | Zero build step, zero npm dependency drift | Requires npm audit & Vite updates | High maintenance, framework updates |
| **Primary Trade-off** | Bulletproof & instant load, but manual repetition if multi-page | Modular components, but build pipeline setup overhead | High capability, but high over-engineering risk for single page |

---

## 🧪 4. Pressure-Testing the Front-Runner

* **What breaks if I pick Option 1 (Simplest)?** Nothing breaks. The portfolio sitemap is designed as a single-page scroll layout (`/`). Semantic HTML5 handles code blocks, responsive charts, and SVG graphics natively without framework bloat.
* **What do I maintain if I pick Option 3 (Most Powerful)?** Next.js App Router requires managing TypeScript interfaces, server vs client component boundaries, hydration errors, and breaking framework updates.
* **Can I finish in two weeks?** Yes. Option 1 allows 100% of build time to be spent refining case study prose, visual layout, and Precision@50 proof charts rather than debugging build scripts.
* **Does it show my work well?** Exceptionally well. Lightweight HTML/CSS renders code blocks crisply, loads in under 300ms, and runs smoothly on all mobile viewports.

---

## ✍️ 5. Final Stack Rationale & Decision

### Chosen Stack: Option 1 — Static HTML5 + Vanilla CSS + GitHub Pages

> **Why I Chose It:**  
> I selected Option 1 because it perfectly satisfies the core proof requirement without introducing accidental complexity. The portfolio's sole job is to demonstrate applied engineering judgment and present empirical machine learning metrics (88.00% Precision@50). Static HTML5 with vanilla CSS variables provides zero-friction deployment on GitHub Pages, sub-second load times, and complete freedom to customize design tokens matching our Identity Kit (`#F8FAFC`, `#0F172A`, `#2563EB`).

> **Why I Rejected Option 2 & Option 3:**  
> Option 2 (Vite + React) and Option 3 (Next.js + TypeScript) introduce unnecessary framework overhead for a single-page scroll layout. Building a static single-page portfolio inside Next.js creates a classic over-engineering failure trap — spending critical internship build hours wrestling with Node dependencies and hydration warnings instead of polishing case study evidence.

> **Can I Maintain This?**  
> Absolutely. Static HTML and CSS carry zero maintenance debt. There are no npm packages to break, no security vulnerabilities to patch, and no build servers to configure. It will remain online and functional indefinitely.
