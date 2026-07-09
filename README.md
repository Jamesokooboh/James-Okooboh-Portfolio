# James Okooboh — Portfolio

A single-file, dark-themed portfolio site for a Cloud & DevOps Engineer — built to look and feel like a modern SaaS product page (Vercel/Stripe-adjacent), not a template CV page. No framework, no build step, no dependencies beyond three Google Fonts loaded via CDN.

**Live:** deploy via GitHub Pages (see below) — once enabled, the site is served straight from this repo.

## What makes this different from a typical portfolio template

Every project card renders a small, animated SVG diagram tracing the **actual data flow** of that system — S3 → SQS → Lambda → DynamoDB → SNS for the serverless project, ALB → ECS Fargate → CloudWatch for the Java deployment, and so on. These aren't decorative icons; they're simplified versions of each project's real architecture, with a moving "pulse" animation along the connector lines to suggest live traffic.

## Structure

```
.
├── index.html   # Entire site: markup, styles, and script in one file
└── README.md
```

Everything — CSS custom properties, the SVG architecture diagrams, and the scroll-reveal script — lives inside `index.html`. There's nothing to install and nothing to build; open the file in a browser and it works.

## Sections

| Section | Content |
|---|---|
| **Hero** | Headline, summary, résumé/CTA buttons, and a live "request path" diagram (Client → ALB → EKS/ECS → CloudWatch) |
| **Work** (`#work`) | Five project cards, each with its own architecture diagram, tech-stack tags, and a link to the project's source repo |
| **Capabilities** (`#capabilities`) | Skills grouped by category (AWS, IaC, Containers, CI/CD, Monitoring, Application Development) rather than a flat badge wall |
| **Experience** (`#experience`) | Work history timeline |
| **Contact** (`#contact`) | Email, GitHub, LinkedIn, and résumé links |

## Design system

- **Palette:** near-black background (`#0B0F14`) with a signal-teal accent (`#4DE8C8`) and amber used sparingly for labels — CSS custom properties defined once in `:root`, not hardcoded per element
- **Type:** [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) for headings, [Inter](https://fonts.google.com/specimen/Inter) for body text, [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono) for technical labels, tags, and diagram text
- **Motion:** scroll-triggered fade-ins via `IntersectionObserver`, plus a continuous dash animation on the diagram connector lines

## Built-in resilience

A couple of things worth knowing if you're editing this:

- **Progressive enhancement, not JS-dependent visibility.** The `.reveal` / `.project-card` / `.cap-card` elements only start hidden once a `js-ready` class is added to `<html>` by an inline script. If JavaScript fails to load for any reason, content is visible by default rather than permanently hidden.
- **Timeout safety net.** Even with JS running, a `setTimeout` forces every animated element visible after 2.5s regardless of whether `IntersectionObserver` fired — so a slow-to-intersect element can never get stuck invisible.
- **`prefers-reduced-motion` is respected** — all animations and transitions collapse to near-zero duration for users who've requested reduced motion at the OS level.

## Deploying with GitHub Pages

1. Go to **Settings → Pages** in this repository.
2. Under **Source**, select **Deploy from a branch**.
3. Choose the `main` branch and `/ (root)` folder, then **Save**.
4. GitHub will publish the site at `https://jamesokooboh.github.io/James-Okooboh-Portfolio/` within a minute or two.

No further setup is needed — since the whole site is one static `index.html`, there's no build step for Pages to run.

## Editing content

All project data, links, and copy live directly in the HTML in `#work` and `#contact` — search for the relevant `<h3 class="project-title">` or link `href` to update text or point at a different repo. There's no CMS or data file; it's a static, hand-authored page by design.
