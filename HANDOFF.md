# Hand-off: getting the landing live

**Approach:** the landing stays a set of static pages. Sign-up, log-in and payment happen in the app. The landing only links to the app and makes a few small calls, so nothing here can break the app, and nothing in the app can break the landing.

Every form shows "Preview: … is switched off" until it's connected.

## Launch checklist

| # | Piece | What to do | Effort | Risk |
|---|---|---|---|---|
| 1 | Hosting | Serve `site/` as static files (DigitalOcean App Platform static site, or Spaces + CDN). Serve `404.html` for unknown addresses. | Small | None |
| 2 | Sign up / Log in | `signup.html` asks one question: "I run a business" or "I'm a creator". Each choice has its own page (`signup-business.html`, `signup-creator.html`; the creator page adds an Instagram handle, field `handle`). Point each at the app's matching sign-up (e.g. `https://app.ionkol.com/signup?as=business` / `?as=creator`), and Log in at `/login`. The app owns the forms, Google sign-in and verification codes. | Small | None to the landing |
| 3 | Plans and payment | "Start free" → business sign-up with `?plan=free`. Core "Sign up" → business sign-up with `?plan=core&billing=yearly` or `monthly`, taken from the Yearly/Monthly switch. Payment happens in the app (Stripe). | Small | None to the landing |
| 4 | Book a demo | Already a link to the booking page (the `BK` list in `contact.html`). Malay has no booking link yet; add one when it exists. | Done | None |
| 5 | Newsletter | Form `.nlf` (one email) → add the address to the Brevo list, with consent recorded. | Small | Low |
| 6 | Plus waitlist | Kept on purpose (owner's call, 25 Nov 2026). Form `#wl` (one email) → its own Brevo list. | Small | Low |
| 7 | Contact form | Form `#cf` (`fn` first name, `ln` last name, `e` email, `m` message) → one small endpoint that emails support@ionkol.com. The Malay demo request form `#df` works the same way. | Small | Low |
| 8 | Hero creator search | Form `#cs` → our own API returns the creator's public profile or "not found". Each lookup is a paid data request: cache results and set a daily budget agreed with the owner before switching it on. | Medium | Low |
| 9 | Jobs | `jobs.html` shows 14 sample jobs. Feed it real open job posts from the app (photo, type, kind, category, city, format, offer, apply-by, applicants, spots). `job.html#<id>` shows one job. **Apply** links to the app. If there are no real jobs at launch, hide the Jobs links. | Medium | Low |

Items 1–4 are enough to go live. Items 5–9 can follow one at a time.

## Free plan rule (owners' call, 25 Nov 2026)

**Free means see, not send.** A Free account must never reach a real creator.

- Free shows: the profile read, 3 campaign ideas, 5 matched creators (2 in full; 3 with the handle locked), and the brief, invite and Instagram message preview for one creator, with the Copy and Open chat buttons locked.
- Sending invites, posting a job and receiving applicants need Core, with a card on file.
- The send screen states how many real creators it reaches, and won't send until the offer and dates are filled in.
- For the first 50 campaigns, our team approves each business's first send.

The pricing table on the home page already says this. The app must enforce it on the server, not only by hiding buttons.

## Before going public

- **Text:** remove "Preview: forms are switched off on this page." from every footer.
- **Share image and icon:** every page now has a title, a description, a share image (`og.jpg`) and an icon (`favicon.svg`). Both are stand-ins made from the current logo; replace them when the final logo file arrives, and make the `og:image` address absolute once the real domain is known.
- **Sample jobs:** the 14 sample jobs carry dates in Nov–Dec 2026. They are samples; real jobs replace them (item 9).
- **Links:** add the LinkedIn link (missing) and confirm the Instagram link (instagram.com/ionkol).
- **Footer:** put in the real company address.
- **Legal:** Terms and Privacy still say "Draft for legal review" and have highlighted blanks.
- **Translated pages** (`-ko`, `-ms`, `-zh-hans`, `-zh-hant`): add `hreflang` links between the language versions. Keep them out of the menus until a native speaker has signed off each language. The job post, Terms and Privacy are English only for now.
- **Korean font:** load **Pretendard** before Noto Sans KR.
- **Cookie notice:** the choice is saved in the browser as `ck` = `y` (accept all) or `n` (only necessary). Load any analytics only when it's `y`. No third-party analytics is planned; we use our own.

## Field rules already checked in the page (repeat them on the server)

Sign up: names filled, the Instagram handle filled (creators only), a valid email, a password of 8+ characters with an uppercase letter, a number and a symbol, the passwords match, the Terms box ticked. The optional email-updates tick is marketing consent; store it separately.
