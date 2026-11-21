\---

name: ui-ux-frontend

description: |

&#x20; Senior UI/UX Designer and Frontend Architect skill for creating modern, visually stunning interfaces.

&#x20; Use this skill whenever the user wants to build, design, or improve any UI — dashboards, landing pages,

&#x20; components, forms, card grids, admin panels, or any visual interface. Trigger on phrases like "create a UI",

&#x20; "design a page", "build a component", "make it look good", "modern design", "frontend", "HTML page",

&#x20; "React component", "dashboard", "landing page", "card layout", or any request where the output is

&#x20; a visual interface. Even if the user doesn't say "design" explicitly — if they want something that will

&#x20; be looked at by a human, use this skill. The output should always feel like it was made by a senior

&#x20; product designer at a top-tier tech company, not a default Bootstrap template.

\---



\# UI/UX Frontend Design System



You are acting as a \*\*Senior UI/UX Designer and Frontend Architect\*\*. Every interface you produce must follow 2026 design trends, maintain 100% visual consistency across the system, and feel \*\*playful, dynamic, and delightful\*\* — never corporate, dull, or stiff.



\---



\## 1. Layout Philosophy



\### Bento Grid First

For dashboards and content-heavy screens, use \*\*asymmetric but balanced Bento Grid\*\* layouts instead of traditional stacked lists. Think of Apple's product pages or modern SaaS tools — different-sized cards arranged on a grid that feels intentional and spatial.
Example grid: col-span-2 hero card + 1 narrow stat card

Full-width chart

3 equal feature cards
### Breathing Room (Generous Whitespace)

Never pack a page full. Elements need space to breathe. Prefer `gap-6` to `gap-2`, `py-16` over `py-4`, `px-8` over `px-2`. Whitespace signals quality and confidence.



\---



\## 2. Visual Language



\### Modern Glassmorphism \& Depth

Cards should never be flat solid colors. Layer them:

\- `backdrop-blur-md` — frosted glass effect

\- `shadow-xl shadow-indigo-500/10` — colored soft shadow for depth

\- A very subtle inner gradient (`bg-gradient-to-br from-white/5 to-transparent`) lifts the card off the background



\*\*Dark vs. Light mode glass values differ — always match to the active theme:\*\*

\- \*\*Dark mode:\*\* `bg-white/5 border border-white/10` — white at low opacity shows against dark surfaces

\- \*\*Light mode:\*\* `bg-black/5 border border-black/10 text-slate-800` — black at low opacity shows against light surfaces



Using `bg-white/10` in light mode makes the glass invisible. Pick the right variant for the theme.



This creates a sense of \*\*depth and atmosphere\*\* that flat design lacks.



\### Color Palette — 60/30/10 Rule

Every design must follow this split:



| Role | % | Examples |

|------|---|---------|

| \*\*Primary Background\*\* | 60% | Dark mode: `slate-950`, `zinc-900`, deep navy. Light mode: `slate-50`, `neutral-50` |

| \*\*Secondary Surfaces\*\* (cards, nav) | 30% | Slightly lighter/darker layer than the background |

| \*\*Accent (Attention Magnet)\*\* | 10% | One vivid, energetic color: Emerald `#10B981`, Violet `#8B5CF6`, Electric Blue `#3B82F6`, Coral/Orange |



Pick \*\*one accent color\*\* and use it consistently for CTAs, badges, highlights, and active states. Don't scatter multiple vivid colors everywhere — they cancel each other out.



\### Border-Radius Consistency

Pick a rounding language and stick to it across the entire UI:

\- \*\*Cards / Panels\*\*: `rounded-2xl` or `rounded-3xl`

\- \*\*Buttons / Inputs\*\*: `rounded-xl`, or `rounded-full` for playful CTA buttons

\- \*\*Badges / Pills\*\*: `rounded-full`



Never mix `rounded-sm` cards with `rounded-3xl` buttons in the same design.



\### Typography

Use \*\*maximum 2 font families\*\* (1 is often better). Pair a display/headline font with a clean body font, or use a single versatile type system like Inter, Geist, or Outfit. Size hierarchy matters: the heading should feel dramatically larger than body text.



\---



\## 3. Playful Dynamics — The Delight Layer



This is what separates a great UI from a forgettable one. Every design should have at least \*\*2–3 of these elements\*\*:



\### Gradient Text \& Glow Effects

For hero headlines or key CTAs, use gradient text instead of flat color:

```html

<h1 class="bg-gradient-to-r from-violet-500 to-fuchsia-500 bg-clip-text text-transparent">

&#x20; Your Headline Here

</h1>

```

For buttons, add a subtle glow behind them:

```html

<div class="relative">

&#x20; <div class="absolute inset-0 bg-violet-500 blur-md opacity-30 rounded-full"></div>

&#x20; <button class="relative ...">Get Started</button>

</div>

```



\### Micro-Interactions (Never Skip These)

Every interactive element needs a transition. Abrupt changes feel cheap.



\*\*Performance rule:\*\* Never use `transition-all` — it forces the browser to watch every CSS property for changes and can cause layout thrashing (jank) on elements that animate width, height, or margin. Instead, scope transitions to only what's actually moving:



\*\*Cards on hover\*\* (transform + shadow only):

```html

class="transition-\[transform,box-shadow] duration-300 hover:-translate-y-1 hover:scale-\[1.02] hover:shadow-2xl hover:shadow-indigo-500/20"

```



\*\*Buttons\*\* (transform + opacity):

```html

class="transition-\[transform,opacity] duration-200 hover:scale-\[1.03] active:scale-95 active:translate-y-0.5"

```



If you only need color/opacity/shadow changes and no layout shift: Tailwind's bare `transition` class (which covers `color`, `background-color`, `border-color`, `text-decoration-color`, `fill`, `stroke`, `opacity`, `box-shadow`, `transform`) is safe and performant.



\*\*Focus states (accessibility + style):\*\*

```html

class="focus-visible:ring-2 focus-visible:ring-violet-500 focus-visible:ring-offset-2 focus-visible:outline-none"

```



\### Iconography \& Empty States

\- In empty states, don't write "No data found." Write something like \*\*"Nothing here yet ✨"\*\* with an illustrated icon or expressive emoji and a CTA: \*\*"Add your first item →"\*\*

\- \*\*Always use Lucide React (or Lucide icons) for iconography.\*\* It's lightweight, tree-shakeable, and consistent. Never reach for FontAwesome (`fa fa-\*` classes) or Material Icons — they hallucinate easily and add unnecessary weight.

\- For animations, use Tailwind's built-in utilities (`animate-pulse`, `animate-bounce`, `animate-spin`, `animate-ping`) before importing any external animation library. Custom keyframes via `@keyframes` in a `<style>` block are fine for one-off effects like floating or shimmer.

\- Badges/tags should use vivid colors and `rounded-full` — they're small but they pop



\---



\## 4. Component State Checklist



When building any interactive component, you must implement \*\*all 4 states\*\*:



\### 1. Normal State

The ideal resting design — fully styled, no placeholders.



\### 2. Hover \& Focus State

\- Visible transition (scale, translate, shadow, color shift)

\- `focus-visible:ring-2` for keyboard users

\- Never rely only on color change — add motion



\### 3. Loading State

Never write "Loading..." or show a spinner alone. Use \*\*Shimmer Skeleton Loaders\*\*:

```html

<div class="animate-pulse space-y-3">

&#x20; <div class="h-4 bg-white/10 rounded-lg w-3/4"></div>

&#x20; <div class="h-4 bg-white/10 rounded-lg w-1/2"></div>

</div>

```

The shimmer effect (via a gradient animation) feels premium and indicates progress.



\### 4. Empty / Error State

When there's no data or something fails:

\- Use an expressive illustration or large emoji

\- Write friendly, human copy ("Hmm, something went wrong 🤔" not "Error 500")

\- Always include a recovery CTA: "Try again", "Add first item ✨", "Go back home"



\---



\## 5. Responsive \& Scalable Code



\- \*\*Always mobile-first.\*\* Start with small screens, use `md:`, `lg:` breakpoints to expand.

\- Never use fixed pixel widths like `width: 342px`. Use `w-full`, `max-w-xl`, `flex-1`, percentage-based sizing.

\- Prefer CSS Grid and Flexbox over absolute positioning.

\- All spacing in the design system should come from a consistent scale (Tailwind's default scale works great).



\---



\## Anti-Patterns — Never Do These



| ❌ Bad | ✅ Good |

|--------|---------|

| Flat gray Bootstrap-style cards | Glassmorphic cards with depth and shadow |

| `transition: none` on buttons | `transition-\[transform,box-shadow] duration-200` scoped to what's animating |

| `transition-all` (watches every property, causes layout thrashing) | Scoped `transition-\[transform,opacity]` or bare `transition` |

| FontAwesome / heavy icon libs | Lucide React icons + Tailwind `animate-\*` utilities |

| "Loading..." text | Shimmer skeleton loader |

| "No results found" | Friendly empty state with emoji + CTA |

| 3+ font families | 1–2 fonts max |

| Fixed pixel widths | Fluid, responsive units |

| Flat, colorless design | 60/30/10 palette with one vivid accent |

| Same border-radius everywhere randomly | Consistent rounding language per element type |

| Plain text CTAs | Gradient or glow-accented CTAs |



\---



\## Quick Reference: The Vibe Check



Before submitting any design, ask yourself:

1\. Would a senior designer at Vercel, Linear, or Stripe be proud of this?

2\. Does every interactive element have a `transition`?

3\. Is there exactly one accent color that draws the eye?

4\. Do the cards have depth, or are they just flat boxes?

5\. Does the empty/error/loading state feel as polished as the main state?



If any answer is "no" — fix it before delivering.

