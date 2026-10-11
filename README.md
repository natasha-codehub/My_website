# Natasha Agarwal — Product Portfolio

Static HTML/CSS site, no build step, deployable to Vercel as-is.

## Deploy

**Fastest:** go to vercel.com/new, drag this folder in (or connect it as a GitHub repo first, recommended for future updates), accept the defaults — it's a static site, Vercel needs no config beyond what's in `vercel.json`.

**Via CLI:** `npx vercel` from inside this folder, then `npx vercel --prod` once you're happy with the preview URL.

**Recommended:** push this folder to a GitHub repo and connect that repo to Vercel, so every future update (new case study, theme tweak) is just a git push and Vercel redeploys automatically.

## Moving from zips to a Git repo (one-time setup)

Right now each phase arrives as a fresh zip of the whole project. Once you're happy with where the site is, switch to a repo so future phases are just a `git pull`-style overwrite + commit instead of a fresh download each time:

1. Unzip the latest phase zip somewhere permanent, e.g. `~/code/portfolio-site`, and `cd` into it.
2. `git init`
3. `git add .`
4. `git commit -m "Initial portfolio site"`
5. Create an empty repo on GitHub (via github.com/new, or `gh repo create portfolio-site --private --source=. --remote=origin`).
6. `git remote add origin <your-repo-url>` (skip if you used `gh repo create` above, it sets this for you)
7. `git push -u origin main`
8. Go to vercel.com/new, choose "Import Git Repository," pick this repo, accept the defaults. Every future push to `main` auto-deploys.

**For every future phase after that:** unzip the new phase's zip contents directly over this same folder (overwrite when prompted), then from inside the folder:

```
git status              # see exactly what changed
git add -A
git commit -m "Phase N: <short description>"
git push
```

Vercel picks up the push and redeploys automatically, no dashboard steps needed. `git status` is also a good sanity check that nothing outside what I described actually changed.

## Structure

```
index.html          - homepage (hero, impact stats, domains, how-i-work, case study previews, agents, casebook, about teaser)
about.html           - full bio, what she works with, links to books/testimonials/contact
books.html            - books that rewired how she works
testimonials.html     - three reference quotes
contact.html          - contact links + the "hey there" illustration
css/style.css       - design tokens + all component styles, single source of truth for the theme
case-studies/       - the six flagship case study pages
images/
  natasha.png          - real headshot, used in the about section/page
  hey-there.png         - decorative illustration, used on the contact page
  og-image.png          - generated social share preview image (1200x630)
favicon.svg         - NA monogram favicon
js/showcase.js      - light vanilla JS: work-showcase filtering, related-work recommendations, testimonial rotator
```

## Design tokens (do not change without deciding to)

- Background `#0a0d13`, panels `#10141c`
- One accent `#ff5a36`
- Warm neutral `#d9c9a8` (sparing use — quote attributions, small highlights)
- Display type: Archivo 900, uppercase, tight tracking
- Labels/numbers: IBM Plex Mono

Full rationale lives in the `product-portfolio-updater` skill.

## Build phases

**Phase 1 — done.** Design system (tokens, components) + homepage: hero with real positioning copy, impact stats strip, domain exposure, "How I Work" framework (the Decision Ledger pattern — surface ask → what made it hard → decision → trade-off → result), six case study preview cards ranked by signal strength, builder/agents teaser, about teaser, contact footer.

**Phase 2 — done.** Individual case study pages for all six flagship stories (`case-studies/`), each following the Decision Ledger skeleton (surface ask → what made it hard → the decision → the trade-off → the result). Invoice Automation has both the tight summary and a deeper 5-decision breakdown in an expandable `<details>` section (no JS needed). Homepage cards are wired to these pages, and each case study links to the next one in priority order.

**Phase 3 — done.** Builder/Agents section filled in with real content: Competitor Analysis Agent (~70% research time saved), a merged Newsletter + LinkedIn Intelligence entry (they turned out to be the same underlying system, one shared memory layer feeding both), and Listing Health Score as a stub with just its live prototype link since the write-up doesn't exist yet. Added a condensed "Product Casebook" strip (`#casebook`) with five short cards: two teardowns (Amazon delivery, carbon-transparent eCommerce), a guesstimate (steps-per-day), and two RCAs (Uber revenue, Netflix KPIs) — one-liners only, deliberately not full pages, so they don't compete with the real shipped work.

**Left out on purpose:** "Gamifying Mutual Fund Investment" — its Notion entry still has unedited template placeholder text (a mismatched description about "patient health metrics") and a prototype URL that just points to Bootstrap's GitHub repo, not a real project link. Don't publish it until Nats sends real content.

**Phase 4 — done.** Split About into its own page (homepage keeps a short teaser + link), added Books and Testimonials pages, and a dedicated Contact page. Pulled her real headshot and the official "Impact at a Glance" numbers straight from the Notion export ($46.4M GMV owned, 38→91% STP, ~$1M annual run-rate savings, 17-person org / 5 systems, 12+ years) into the homepage stats strip, replacing the smaller set of numbers I'd picked myself in Phase 1. Added a favicon (NA monogram), Open Graph / Twitter card meta tags, and a generated social preview image matching the site's theme.

**Phase 4.5 — done.** Went through all ~30 images and every mentioned link in the Notion export and added what was safe: an architecture diagram + a "decision ledger" comparison graphic on Invoice Automation (plus its stats recreated as on-theme mini-stat tiles), a hero photo on Support Deflection, the real Sentinel dashboard UI on AI Regression Intelligence (plus a video walkthrough link and the GitHub repo link), and two architecture diagrams on Behavioral Health RAG (plus a link to the eval prompt doc). Also cross-linked the AI Onboarding Agent case study to Invoice Automation and Support Deflection where it already referenced their confidence-gating pattern in the text.

**Deliberately excluded, needs your call:**
- Telemetry Forecasting: five "actual system" screenshots (`image 11–14.png`, `image 9.png`) show a live Salesforce console with a real client account name, real employee names and an email address, real phone numbers, and the internal `espriGas.lightning.force.com` URL. Did not publish any of these. If you want telemetry screenshots on the site, either confirm the client name is fine to show publicly, or send redacted versions with names/emails/URLs blurred.
- Invoice Automation: the two "Sample Invoices" images are real vendor shipping/billing documents (Matheson Tri-Gas, TMG Gases, real account numbers and dollar amounts). Excluded, same reasoning.
- AI Onboarding Agent: the one available screenshot (`image 20.png`) has the client's actual name ("EspriGas") visible in the chat UI. Excluded until you confirm that name is okay to show, or send a version with it blurred/relabeled.

## Open question for Nats

The telemetry screenshots show an account literally named "BNSF Railway Company" inside what looks like production Salesforce (not obviously a demo/prototype). An earlier phase of this project noted "BNSF" as just a placeholder demo account name, not a real client, that assumption may have been wrong. Worth confirming directly: is BNSF a real, nameable client, or should any reference to it (even in writing, not just screenshots) be genericized on the public site?

**Phase 4.6 — done, "award-winning" pass.** Positioning confirmed as full-time-roles-only (not consulting/freelance). Added: a persistent "Let's Talk" header CTA button on every page except Contact itself, an underline hover animation on nav links, an end-of-case-study conversion CTA on all six case studies (placed before the "next case study" link, at peak engagement rather than after), and a site-wide motion layer — all pure CSS, zero JS: fade-up entrance on hero/page headers and stat tiles, a subtle image zoom on case study figures, and a scroll-linked reveal for sections/cards that only activates in browsers supporting the CSS `scroll-timeline` spec (Chrome/Edge) and degrades to plain static content everywhere else, so nothing is ever hidden or broken. Everything respects `prefers-reduced-motion`.

**Phase 5 — done, interactive work showcase.** The `#work` section is no longer a static grid. Added: a three-facet filter bar (Type / Industry / Skill) that shows/hides case study cards with a smooth fade, driven by `data-type` / `data-industry` / `data-skills` attributes already on each card; a "Quick look" expandable panel on every card (native `<details>`, no JS needed to open/close) showing a data-driven Before → After comparison plus its tags, built entirely from facts already established in each case study's own text, not fabricated; and a rotating "What colleagues say" testimonial strip pulling the three real quotes from the Testimonials page, with dot navigation and a link through to the full page. Each individual case study page got its own Before → After panel below the hero (using the same real before/after language as its homepage card), and a "You might also like" related-work block that computes the two most relevant other case studies by shared industry, skill, and shipped/prototype status — genuinely dynamic, not hand-picked, so it stays correct as new case studies get added. All of this required reversing the earlier "zero JS" decision to a small, dependency-free vanilla JS file (`js/showcase.js`, ~250 lines, no framework, no build step, no external libraries) that only handles filtering, the related-work computation, and the testimonial rotation; everything else (expand/collapse, all the motion) stays pure CSS/HTML as before. True image galleries and real before/after screenshot pairs are still deferred, per the open confidentiality question below — this phase used real metrics and real ledger language instead of images.

To add a new case study later and have it show up correctly in filtering and related-work: add one entry to the `CASES` array at the top of `js/showcase.js`, and give its homepage `.card-wrap` matching `data-type` / `data-industry` / `data-skills` attributes. The `product-portfolio-updater` skill has been updated with this workflow.

**Phase 6 — ongoing.** New case studies as Natasha feeds them (patent infringement prototype next), theme tweaks on request. Use the `product-portfolio-updater` skill for this so priority ranking, voice, and the design tokens stay consistent without re-deriving them each session.
