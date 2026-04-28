# OpFix Site Update - Book Page Integration

## What's shipping

A new dedicated `book.html` page replaces the team page. Built to Break gets its own
home on opfix.io. Team page (with placeholder team members) is being removed entirely.

## Files in this drop

1. **book.html** - NEW page (drop in repo root)
2. **index.html** - patched (replace existing)
3. **how-it-works.html** - patched (replace existing)
4. **the-system.html** - patched (replace existing)

## Files Everett needs to manually patch

I didn't have access to these. Apply the same edits below.

### case-studies.html

**NAV LINKS (`<div class="nav-links">`):**
- Replace `<a href="case-studies.html"...>Case Studies</a>` with `<a href="book.html">Book</a>`
- The current page indicator (e.g., `style="color:var(--white)"`) on the Case Studies link
  should be REMOVED since this page no longer represents the Book section

**FOOTER LINKS:**
- DELETE `<a href="case-studies.html">Case Studies</a>` entirely
- Replace `<a href="opfix_team_page.html">The Team</a>` with `<a href="book.html">Book</a>`

**MOBILE NAV (`<div class="mobile-nav">`):**
- Replace `<a href="case-studies.html"...>Case Studies</a>` with
  `<a href="book.html" onclick="toggleMobileNav()">Book</a>`
- Replace `<a href="opfix_team_page.html"...>The Team</a>` (if present) with `<a href="book.html" onclick="toggleMobileNav()">Book</a>`
  - If this creates a duplicate Book link, remove one

### four-pillars.html

Same edits as case-studies.html above. Remove all references to:
- `case-studies.html`
- `opfix_team_page.html`

Replace with `book.html` where appropriate.

## Files to DELETE from repo

- **opfix_team_page.html** - kill entirely. No incoming links remain after the patch.

## Required asset to add

- **built_to_break_cover.jpg** - drop in repo root. 2x resolution minimum (target display
  is 280px wide, so ship 560×840 minimum). Pull from KDP or use the production cover file.
  Without this asset, book.html shows a broken image.

## Verification checklist after deploy

For each page (index, how-it-works, the-system, four-pillars, case-studies):

- [ ] Nav has: How It Works | Four Pillars | The System | **Book** | Free Diagnostic
- [ ] Footer has: ...standard links... | **Book** (and NO Case Studies, NO Team)
- [ ] Mobile nav has Book in the list, no Case Studies, no Team
- [ ] No broken `case-studies.html` or `opfix_team_page.html` references anywhere
  (run: `grep -r "case-studies.html\|opfix_team_page.html" .` in repo - should return nothing)

For book.html specifically:

- [ ] Renders book cover image (built_to_break_cover.jpg)
- [ ] Both Amazon CTAs (hero + final) link to https://www.amazon.com/dp/B0GXSRB5MQ
- [ ] Both open in new tab (target="_blank")
- [ ] Mobile QA at 375px - cover scales to 220px, layout is centered, no horizontal scroll

## Rollback

If anything breaks, the original opfix_team_page.html and the original index/how-it-works/the-system files are still in git history. `git revert` the commit.
