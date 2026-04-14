# Premium Personal Portfolio — Product Requirements Document

> **Role Prompt:** You are a senior product-minded full-stack engineer and an award-winning portfolio designer with deep expertise in conversion-optimized personal brand sites, modern web performance, and recruiter psychology.

---

## 1. Vision & Objective

Build a **production-grade, recruiter-optimized personal portfolio website** that communicates engineering excellence, product taste, credibility, and personality — all within the first 5 seconds of a visit.

This is **not** a template. This is a handcrafted, high-end personal brand site for a serious professional. It should feel like the work of someone who ships polished, real-world products.

### Primary Success Metrics

| Metric | Target |
|---|---|
| Time to first meaningful impression | < 5 seconds |
| Lighthouse Performance score | ≥ 95 |
| Lighthouse Accessibility score | ≥ 95 |
| Lighthouse SEO score | 100 |
| Lighthouse Best Practices score | 100 |
| First Contentful Paint (FCP) | < 1.2s |
| Largest Contentful Paint (LCP) | < 2.5s |
| Cumulative Layout Shift (CLS) | < 0.1 |
| Total bundle size (gzipped) | < 200 KB |
| Mobile usability | Flawless on all breakpoints |
| Recruiter conversion (CTA click-through) | Maximized through design |

### Target Audience (Priority Order)

1. **Recruiters & hiring managers** — Scanning quickly; need instant credibility signals
2. **Engineering managers & tech leads** — Evaluating technical depth and judgment
3. **Potential clients & collaborators** — Assessing capability for product work
4. **Fellow engineers** — Evaluating code taste and technical interests

---

## 2. Design System & Visual Direction

### 2.1 Aesthetic Philosophy

- **Premium, agency-level quality** — Every pixel should feel intentional
- **Dark mode first** with a polished light mode toggle (persisted via `localStorage`)
- **Minimalist but not empty** — Confident use of whitespace, depth, and focus
- **Memorable, not noisy** — Restrained creativity that serves communication
- **Anti-template** — Must not resemble generic Bootstrap/Tailwind starter kits

### 2.2 Typography

- Use a **premium variable font pairing** (e.g., Inter/Satoshi for body, Clash Display/Cabinet Grotesk for headings — or similar modern geometric/humanist pair)
- **Strong typographic hierarchy:** minimum 4 distinct levels (display, heading, subheading, body)
- Font sizes: fluid/responsive using `clamp()` — e.g., hero heading from 2.5rem to 5rem
- Line heights: 1.2 for headings, 1.6–1.7 for body text
- Letter spacing: tighter on large headings (-0.02em to -0.04em), normal on body
- **No font loading flash** — use `font-display: swap` and preload critical fonts

### 2.3 Color System

- **Dark mode primary:** Rich dark background (#0a0a0f or similar deep navy/charcoal), not pure black
- **Accent color:** A single signature accent (electric blue, violet, or emerald — choose one that conveys sophistication)
- **Accent gradient:** Subtle gradient on key CTAs and highlights (accent → shifted hue)
- Full palette: background, surface, surface-elevated, border, text-primary, text-secondary, text-muted, accent, accent-hover, success, error
- All color pairs must meet **WCAG 2.1 AA contrast ratios** (4.5:1 for text, 3:1 for large text/UI)
- Colors defined as CSS custom properties for easy theming

### 2.4 Spacing & Layout

- **8px base grid system** — All spacing in multiples of 8 (8, 16, 24, 32, 48, 64, 80, 96, 128)
- **Max content width:** 1200px for text-heavy sections, 1400px for visual sections
- **Section vertical padding:** 96px–128px on desktop, 64px–80px on mobile
- Container breathing room: minimum 24px horizontal padding on mobile
- **Golden ratio awareness** in key compositional decisions

### 2.5 Motion & Interaction Design

- **Scroll-triggered reveal animations** — Elements fade/slide in as they enter viewport (use Intersection Observer, not scroll listeners)
- **Staggered entrance timing** — Sequential elements animate 50–100ms apart
- **Micro-interactions:** Button hover lifts (translateY -2px + shadow), link underline animations, card hover depth changes
- **Smooth page scroll** with `scroll-behavior: smooth` and offset for fixed nav
- **Cursor interactions** (optional): Subtle magnetic buttons or custom cursor on desktop
- **No animation on `prefers-reduced-motion: reduce`** — Respect accessibility
- Easing: Use cubic-bezier curves (ease-out for entrances, ease-in-out for state changes)
- Duration: 200–400ms for micro-interactions, 500–800ms for scroll reveals
- **No animation libraries** unless they add clear value over CSS + Intersection Observer

### 2.6 Visual Effects (Use Sparingly)

- **Glassmorphism:** Only on floating nav bar or modal overlays — `backdrop-filter: blur()` with semi-transparent background
- **Gradients:** On accent elements, hero decorative shapes, or text highlights — never on backgrounds of full sections
- **Shadows:** Layered box-shadows for depth (surface: subtle, cards: medium, modals: dramatic)
- **Noise/grain texture:** Optional subtle SVG noise overlay on hero background for tactile depth
- **Dot grid / geometric patterns:** Optional background accent — must be very subtle (opacity < 0.05)
- **Glow effects:** Subtle accent-colored glow on hover states of primary CTAs

---

## 3. Site Architecture & Content Structure

### 3.0 Navigation

- **Fixed/sticky top nav** with glassmorphism background on scroll
- Logo/name on the left, section links on the right
- **Active section highlighting** as user scrolls (Intersection Observer–based)
- Mobile: Hamburger menu with smooth slide-in panel (animated, not jarring)
- Dark/light mode toggle in nav (icon-based, with smooth transition)
- **CTA button in nav:** "Let's Talk" or "Hire Me" — always visible
- Nav hides on scroll-down, shows on scroll-up (smart hide pattern)

### 3.1 Hero Section

**Goal:** Instantly establish who you are, what you do, and why someone should care.

- **Headline:** Bold, specific, confident — e.g., *"I build software that people love to use."* or *"Full-Stack Engineer. Product Thinker. Builder."* (craft something with personality)
- **Subheadline:** One sentence of proof — e.g., *"I design and ship performant, user-centric applications used by thousands."*
- **Animated role/title rotation** — Cycle through 3–4 descriptors: "Full-Stack Engineer", "System Architect", "Open Source Contributor", "Product Builder" (typewriter or fade effect)
- **Two CTA buttons:** Primary ("View My Work" → scrolls to projects) + Secondary ("Get in Touch" → scrolls to contact)
- **Visual accent:** Abstract geometric shapes, particle field, gradient orb, or a tasteful code-inspired pattern — no stock photos, no clichéd hero images
- **Availability badge:** Small pill/tag — "Available for opportunities" (green dot + text) — high-conversion pattern for recruiters
- **Scroll indicator:** Subtle animated chevron/mouse icon at bottom of hero
- Hero should be full viewport height (`100dvh`) with content vertically centered

### 3.2 About Section

**Goal:** Build trust and human connection in 15 seconds of reading.

- **Professional photo area** (placeholder with clear instructions for replacement) — circular or rounded-rectangle crop, subtle border/shadow
- **2–3 paragraphs maximum** — Concise, outcome-oriented, written in first person
- Tone: Confident but approachable, specific but not arrogant
- Cover: What you do → What you care about → What sets you apart
- **Key stats/metrics strip** (animated count-up on scroll):
  - Years of experience: `X+`
  - Projects delivered: `X+`
  - Technologies mastered: `X+`
  - Clients/companies served: `X+`
- Optional: A short list of 3–4 personal values or engineering principles (e.g., "Ship fast, iterate faster", "Code is communication", "UX is not optional")
- **Resume download button** — PDF link, secondary style

### 3.3 Skills & Tech Stack

**Goal:** Demonstrate breadth and depth without looking like a keyword dump.

**Presentation approach:** Categorized grid with icon + label for each technology. Use real SVG icons (from Simple Icons / Devicons). Group clearly with category headers.

**Categories:**

| Category | Example Technologies |
|---|---|
| Frontend | React, Next.js, TypeScript, Tailwind CSS, HTML5, CSS3 |
| Backend | Node.js, Python, Express, FastAPI, REST, GraphQL |
| Database | PostgreSQL, MongoDB, Redis, Prisma, Supabase |
| Cloud & DevOps | AWS, Docker, Kubernetes, CI/CD, GitHub Actions, Terraform |
| Tools & Workflow | Git, VS Code, Figma, Jira, Linux, Agile/Scrum |
| Currently Exploring | Rust, WebAssembly, AI/ML, Edge Computing |

- **Do NOT use progress bars or percentage ratings** — These are meaningless and look amateur
- Each tech should have a subtle hover effect revealing a tooltip or brief context
- Optionally highlight "core" vs. "familiar" via visual weight or badge
- Add a "Currently Exploring" category to show growth mindset
- **Animated entrance:** Icons stagger-in as section scrolls into view

### 3.4 Featured Projects

**Goal:** Prove you build real things that create real value. This is the most conversion-critical section.

- Showcase **4–6 projects** — Quality over quantity
- **Card-based layout** — 2-column grid on desktop, single column on mobile
- Each project card must include:

| Field | Description |
|---|---|
| **Project Name** | Clear, memorable |
| **One-Line Description** | What it does, for whom |
| **Problem Statement** | What challenge it solved (1 sentence) |
| **My Role & Contribution** | What you specifically did |
| **Key Impact / Outcome** | Metrics, scale, or qualitative outcomes (e.g., "Reduced load time by 60%", "Served 10K+ users") |
| **Tech Stack** | Inline pills/badges for each technology |
| **Links** | Live demo button + GitHub repo button (if available) |
| **Visual** | Screenshot, mockup, or project logo (placeholder image with clear replacement instructions) |

- **Storytelling order:** Problem → Solution → Impact → Tech (not tech-first)
- Featured/hero project should be larger and more prominent than others
- Card hover: Slight lift + shadow increase + subtle border glow
- **Filter/tab system** (optional): Filter by category (Full-Stack, Frontend, Backend, Open Source)
- Each card links to either a detail page/modal or external links

### 3.5 Professional Experience / Timeline

**Goal:** Show career trajectory, growth, and credibility through concrete achievements.

- **Vertical timeline layout** — Alternating left/right on desktop, single-column on mobile
- Each entry includes:
  - **Company name** and optional logo
  - **Role/title**
  - **Date range** (formatted as "Mon YYYY – Mon YYYY" or "Present")
  - **2–4 bullet points** of achievements — Use XYZ format: *"Accomplished [X] by doing [Y], resulting in [Z]"*
  - **Tech stack used** — small inline pills
- Timeline line with animated dot markers
- Scroll-triggered progressive reveal (entries animate in as user scrolls)
- **Most recent position first** (reverse chronological)
- Optional: Education entry at the bottom of timeline

### 3.6 Testimonials & Social Proof

**Goal:** Third-party validation that multiplies credibility.

- **Carousel or grid of 3–4 testimonials**
- Each testimonial includes:
  - Quote text (2–3 sentences max)
  - Name, title, and company of the recommender
  - Photo (circular avatar, placeholder provided)
  - Optional: LinkedIn profile link for verification
- **Tasteful quotation mark design element** — Large decorative quote icon
- Auto-rotating carousel with pause-on-hover, or static grid
- Star ratings are optional — only include if genuine
- If no real testimonials yet, include the section skeleton with placeholder content and a note to replace

### 3.7 Blog / Insights (Optional but Recommended)

**Goal:** Demonstrate thought leadership and communication skills.

- Show **3 latest posts** in a card grid
- Each card: Title, excerpt (2 lines), date, reading time, category tag
- Link to external blog (Medium, Dev.to, Hashnode) or future integrated blog
- If no blog exists, label this section "Coming Soon" or omit entirely

### 3.8 Contact Section

**Goal:** Convert interest into conversation with zero friction.

- **Strong headline:** "Let's Build Something Great Together" or "Ready to Talk?"
- **Subtext:** Brief, warm, low-pressure — "Whether you have a project, a question, or just want to connect — I'd love to hear from you."
- **Contact form** with fields:
  - Name (required)
  - Email (required, validated)
  - Subject (optional)
  - Message (required, textarea)
  - Submit button with loading state and success/error feedback
- **Form validation:** Client-side with clear inline error messages
- **Alternative contact links** alongside the form:
  - Email (mailto link, with copy-to-clipboard)
  - LinkedIn
  - GitHub
  - Twitter/X (if relevant)
  - Calendly/scheduling link (if available)
- Social links with branded SVG icons and hover color transitions
- Optional: Small embedded map or timezone indicator

### 3.9 Footer

- **Minimal and elegant** — Do not overload
- Site name / logo
- Quick nav links (repeat main sections)
- Social icon links
- Copyright line: `© 2026 [Name]. Crafted with care.`
- Optional: "Built with Next.js & Tailwind" credit line (shows tech confidence)
- Back-to-top button (smooth scroll)

---

## 4. Technical Specification

### 4.1 Recommended Stack

| Layer | Technology | Rationale |
|---|---|---|
| Framework | **Next.js 14+ (App Router)** | Best-in-class SSG, SSR, image optimization, SEO, routing |
| Language | **TypeScript** | Type safety, better DX, signals engineering rigor |
| Styling | **Tailwind CSS 3.4+** | Utility-first, fast iteration, built-in responsive/dark mode |
| Animations | **Framer Motion** | Production-quality React animations, gesture support |
| Icons | **Lucide React** or **React Icons** | Consistent, tree-shakable icon system |
| Font hosting | **Next.js `next/font`** | Zero-layout-shift font loading, auto-optimization |
| Deployment | **Vercel** | Zero-config, edge CDN, analytics, perfect Next.js integration |
| Form backend | **Formspree, Resend, or EmailJS** | Serverless form submission without building an API |
| Analytics | **Vercel Analytics** or **Plausible** | Privacy-friendly, lightweight |
| Linting | **ESLint + Prettier** | Consistent code formatting |

### 4.2 Project Structure

```
my-premium-portfolio/
├── public/
│   ├── images/              # Optimized static images, project screenshots, avatar
│   ├── fonts/               # Self-hosted font files (if not using next/font Google)
│   ├── resume.pdf           # Downloadable resume
│   ├── favicon.ico
│   ├── og-image.png         # Open Graph preview image (1200x630)
│   └── robots.txt
├── src/
│   ├── app/
│   │   ├── layout.tsx       # Root layout with metadata, fonts, theme provider
│   │   ├── page.tsx         # Home page composing all sections
│   │   ├── globals.css      # Tailwind directives, CSS custom properties, base styles
│   │   └── sitemap.ts       # Dynamic sitemap generation
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Navbar.tsx
│   │   │   ├── Footer.tsx
│   │   │   └── Section.tsx          # Reusable section wrapper (id, padding, max-width)
│   │   ├── sections/
│   │   │   ├── Hero.tsx
│   │   │   ├── About.tsx
│   │   │   ├── Skills.tsx
│   │   │   ├── Projects.tsx
│   │   │   ├── Experience.tsx
│   │   │   ├── Testimonials.tsx
│   │   │   ├── Contact.tsx
│   │   │   └── Blog.tsx             # Optional
│   │   ├── ui/
│   │   │   ├── Button.tsx
│   │   │   ├── Card.tsx
│   │   │   ├── Badge.tsx
│   │   │   ├── ThemeToggle.tsx
│   │   │   ├── AnimatedCounter.tsx
│   │   │   ├── TypeWriter.tsx
│   │   │   ├── ScrollReveal.tsx     # Reusable scroll animation wrapper
│   │   │   └── SocialLinks.tsx
│   │   └── icons/                   # Custom SVG icon components if needed
│   ├── data/
│   │   ├── profile.ts              # Personal info, bio, stats
│   │   ├── projects.ts             # Project entries
│   │   ├── experience.ts           # Work history entries
│   │   ├── skills.ts               # Tech stack data
│   │   ├── testimonials.ts         # Testimonial entries
│   │   └── navigation.ts           # Nav links config
│   ├── hooks/
│   │   ├── useScrollReveal.ts      # Intersection Observer hook
│   │   ├── useActiveSection.ts     # Active nav section tracking
│   │   └── useTheme.ts             # Dark/light mode hook
│   ├── lib/
│   │   └── utils.ts                # Utility functions (cn, formatDate, etc.)
│   └── types/
│       └── index.ts                # Shared TypeScript interfaces
├── .eslintrc.json
├── .prettierrc
├── tailwind.config.ts
├── tsconfig.json
├── next.config.js
├── package.json
└── README.md
```

### 4.3 Data Architecture

All content must live in the `src/data/` directory as typed TypeScript objects. This ensures:
- **Single source of truth** for all content
- Easy editing without touching component code
- Type safety prevents broken content
- Clean separation of data and presentation

Example type:
```typescript
interface Project {
  id: string;
  title: string;
  description: string;
  problem: string;
  role: string;
  impact: string;
  techStack: string[];
  liveUrl?: string;
  githubUrl?: string;
  image: string;
  featured: boolean;
  category: 'fullstack' | 'frontend' | 'backend' | 'opensource';
}
```

All placeholder content must be clearly marked with `// TODO: Replace with your actual content` comments.

### 4.4 SEO & Metadata

- **Dynamic metadata** via Next.js Metadata API in `layout.tsx`
- **Open Graph tags:** `og:title`, `og:description`, `og:image` (1200x630 preview), `og:url`, `og:type`
- **Twitter Card tags:** `twitter:card` (summary_large_image), `twitter:title`, `twitter:description`, `twitter:image`
- **JSON-LD structured data:** `Person` schema with name, job title, URL, social links
- **Canonical URL** set correctly
- **Sitemap** auto-generated via `sitemap.ts`
- **robots.txt** allowing all crawlers
- Semantic HTML: proper heading hierarchy (single `h1`, structured `h2`–`h4`), `main`, `section`, `article`, `nav`, `footer`
- All images: descriptive `alt` text, `next/image` for automatic optimization

### 4.5 Performance Requirements

- **Static site generation (SSG)** — All pages pre-rendered at build time
- **Image optimization:** `next/image` with responsive `srcset`, WebP/AVIF auto-format, lazy loading below fold
- **Font optimization:** `next/font` with subsetting, preload, and `font-display: swap`
- **Code splitting:** Automatic via Next.js App Router
- **No unused CSS/JS** — Tailwind purges unused styles
- **Minimize third-party scripts** — No jQuery, no heavy animation libraries unless justified
- **Preload critical assets** — Hero images, fonts
- **Defer non-critical scripts** — Analytics, form handlers

### 4.6 Accessibility Requirements

- **WCAG 2.1 Level AA compliance** minimum
- All interactive elements focusable and operable via keyboard
- Visible focus indicators (custom-styled, not browser default)
- Skip-to-content link (visually hidden until focused)
- `aria-label` on icon-only buttons and links
- `aria-current="page"` on active nav link
- `aria-expanded` on mobile menu toggle
- Form inputs with associated `<label>` elements
- Error messages linked via `aria-describedby`
- Color is never the sole means of conveying information
- `prefers-reduced-motion` respected — disable all animations
- `prefers-color-scheme` used as initial theme fallback
- Minimum touch target size: 44x44px on mobile

### 4.7 Responsive Breakpoints

| Breakpoint | Width | Layout Adjustments |
|---|---|---|
| Mobile | < 640px | Single column, stacked sections, hamburger nav, condensed spacing |
| Tablet | 640px–1024px | Partial grid (2-col projects), side nav or hamburger |
| Laptop | 1024px–1440px | Full layout, all grid columns active |
| Large screen | > 1440px | Max-width container centered, increased whitespace |

---

## 5. Interaction & Animation Specification

### 5.1 Page Load Sequence

1. **Navbar** — Fades in immediately (0ms)
2. **Hero headline** — Slides up + fades in (200ms delay)
3. **Hero subheadline** — Slides up + fades in (400ms delay)
4. **CTA buttons** — Scale up + fade in (600ms delay)
5. **Role rotation** — Starts cycling after 1s
6. **Background accent/visual** — Gentle fade-in (300ms delay)
7. **Scroll indicator** — Fades in after 1.5s

### 5.2 Scroll Behavior

- **Scroll reveal:** Elements fade-in + translateY(20px→0) as they enter viewport (threshold: 0.15)
- **Stagger:** Sequential elements within a section delay 75ms apart
- **Trigger once:** Animations fire only on first scroll-in (no re-animation on scroll-up)
- **Counter animation:** Stats count up from 0 to target over 2 seconds when section is visible
- **Timeline dots:** Light up sequentially as user scrolls through experience section
- **Parallax:** None — avoid. It creates more problems than value on a portfolio.

### 5.3 Hover & Focus States

- **Buttons:** translateY(-2px), shadow increase, slight background shift — 200ms ease-out
- **Project cards:** translateY(-4px), shadow elevation, optional border glow — 300ms ease-out
- **Nav links:** Animated underline (width 0→100%, left-to-right) — 200ms
- **Social icons:** Color transition to brand color + scale(1.1) — 150ms
- **Tech icons:** Subtle glow or tooltip reveal — 200ms
- **Focus rings:** 2px offset outline in accent color, visible on keyboard navigation only (`:focus-visible`)

---

## 6. Content Tone & Copy Guidelines

### Voice

- **First person** ("I build...", "I believe...", "I shipped...")
- **Confident, not arrogant** — Show, don't tell
- **Specific, not vague** — Numbers, outcomes, technologies — not "passionate team player"
- **Concise** — Every word earns its place
- **Human** — A real person wrote this, not a corporate template

### Recruiter Optimization

- **Above the fold:** Title + specialization + availability signal + primary CTA
- **Within 10 seconds:** Clear understanding of what you do, how well you do it, and how to hire you
- **Within 30 seconds:** Evidence (projects, metrics, experience)
- **Exit intent:** Strong footer CTA as final conversion opportunity

### Placeholder Content Notes

All placeholder content should:
- Be realistic and professional (not "Lorem ipsum")
- Be clearly marked with `{REPLACE}` tags or `// TODO` comments
- Include guidance on what kind of content should replace it
- Demonstrate the intended tone and length

---

## 7. Quality Checklist (Pre-Delivery)

### Design
- [ ] Looks premium and polished at every breakpoint
- [ ] Dark mode and light mode both look excellent
- [ ] Typography hierarchy is clear and consistent
- [ ] Spacing follows the 8px grid consistently
- [ ] No orphaned text, widows, or awkward line breaks on common screen sizes
- [ ] All placeholder images have clear replacement instructions

### Performance
- [ ] Lighthouse Performance ≥ 95
- [ ] Lighthouse Accessibility ≥ 95
- [ ] Lighthouse Best Practices = 100
- [ ] Lighthouse SEO = 100
- [ ] No layout shift on load (CLS < 0.1)
- [ ] All images lazy-loaded and optimized

### Accessibility
- [ ] Full keyboard navigation works
- [ ] Screen reader tested (logical reading order)
- [ ] Color contrast meets WCAG AA
- [ ] `prefers-reduced-motion` disables animations
- [ ] Skip link present and functional
- [ ] All form inputs labeled

### Code
- [ ] No TypeScript errors
- [ ] No ESLint warnings
- [ ] Components are small, focused, and reusable
- [ ] Data is separated from presentation
- [ ] No hardcoded strings in components (all in `data/`)
- [ ] Clean git-ready state (no test artifacts, no console.logs)

### SEO
- [ ] Open Graph preview renders correctly
- [ ] JSON-LD structured data validates
- [ ] Sitemap generates correctly
- [ ] Semantic heading hierarchy (single h1)
- [ ] All images have alt text

---

## 8. Deliverables

1. **Complete source code** — Clean, typed, linted, production-ready
2. **README.md** — Setup instructions, content customization guide, deployment steps
3. **All placeholder content clearly marked** — Ready for personalization
4. **Project runs locally** with `npm install && npm run dev` — zero additional setup
5. **Build succeeds** with `npm run build` — no errors, no warnings

---

## 9. Decision-Making Principles

When making design or implementation choices not explicitly covered above:

1. **Favor clarity over cleverness** — If a user can't understand what they're looking at in 3 seconds, simplify
2. **Favor performance over visual flair** — A fast, clean site beats a slow, flashy one
3. **Favor recruiter conversion** — Every section should move the visitor closer to clicking "Contact"
4. **Favor maintainability** — Clean code that's easy to update beats clever abstractions
5. **Favor industry-standard patterns** — Use proven UX patterns; innovate in execution quality, not layout conventions
6. **Fill gaps with the best solution** — If something is ambiguous or missing, implement the highest-quality standard approach

---

*This document defines the complete specification for a premium, modern, recruiter-optimized portfolio website. The final result should feel handcrafted, intentional, and unforgettable — the kind of site that makes someone think "I need to hire this person."*