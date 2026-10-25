# Google Ads tag + moving the website to GitHub

Notes for setting up Google Ads conversion tracking on **faithandflour22.com**
and moving the website's code into this GitHub repo.

## Status

- [ ] Website code pushed to this repo (`bella0428/Faith-Flour`)
- [ ] Google Ads tag added to the site
- [ ] Vercel connected to this GitHub repo
- [ ] Google Ads "Test installation" passes

Google Ads currently says: *"Your Google tag wasn't detected on faithandflour22.com."*
That is expected — the tag hasn't been added to the site yet.

## Where the website lives today

| Place | What's there |
| --- | --- |
| **Vercel** (project `faith-and-flour`) | Hosts the live site at faithandflour22.com and www.faithandflour22.com. It's a Next.js site, deployed straight from the Mac (not from GitHub). |
| **The Mac** — `Faith and Flour/website` folder | The original, complete code. Secrets live in `Faith and Flour/.env` (one folder up), **not** in the website folder. |
| **GitHub** (this repo) | Only a banana bread photo and this note. The website code was never added. |

The site is **not** on Squarespace, so ignore the Squarespace "Code Injection" instructions.

Why the code can't be copied from Vercel: Vercel only returns small pieces of each
file, and some folders (Stripe checkout, admin orders, order success page) are
hidden entirely. Copying from there would produce a broken site, so the move has
to be done from the Mac.

## The Google tag

Google Ads tag ID: **`AW-18535603524`**

The snippet Google gives you (for reference — on a Next.js site it goes in
`app/layout.tsx` using `next/script`, not pasted as raw HTML):

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=AW-18535603524"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'AW-18535603524');
</script>
```

Only one Google tag per page. If a Google Analytics tag (`G-...`) is ever added,
reuse the same `gtag.js` script and just add another `gtag('config', ...)` line.

## Before you start

**Make this repo private.** Anyone can currently read it. The site's code includes
the Stripe checkout and admin login logic. Passwords and API keys stay in Vercel's
settings and `.env`, but a business site's code should still be private.

GitHub → **Faith-Flour** → **Settings** → bottom of the page → **Change visibility** → **Private**.

## Step 1 — Move the code and add the tag (on the Mac)

Open the **Claude desktop app** on the Mac (or run `claude` in a terminal inside the
`website` folder) and paste:

> In my Faith and Flour `website` folder (the Next.js site deployed to the Vercel project "faith-and-flour"):
> 1. Push this folder to my GitHub repo `bella0428/Faith-Flour` on the `main` branch. Do NOT include the `.env` file (it's one folder up), `node_modules`, `.next`, `.vercel`, or `tsconfig.tsbuildinfo`. Check that no API keys or passwords are in the files first.
> 2. Add the Google Ads tag `AW-18535603524` to `app/layout.tsx` using `next/script` (gtag.js with `strategy="afterInteractive"`), run `npm run build` to make sure it works, then commit and push.
> 3. Walk me through connecting the Vercel project "faith-and-flour" to that GitHub repo so pushes to `main` deploy automatically. Then help me confirm the tag shows on faithandflour22.com.

## Step 2 — Connect Vercel to GitHub

Vercel → **faith-and-flour** project → **Settings** → **Git** → **Connect Git Repository**
→ choose `bella0428/Faith-Flour`, production branch `main`.

After this, every push to `main` updates faithandflour22.com automatically.
Hosting stays on Vercel; nothing about the domain changes.

## Step 3 — Check the tag

1. Open https://faithandflour22.com, right-click → **View Page Source**, and search
   for `AW-18535603524`. If it's there, the tag is live.
2. In Google Ads, click **Retest**. If it still fails, wait 10–30 minutes and try
   again, or click **I'll do this later** — Google keeps checking on its own.

## Next

Once the tag is detected, set up a **conversion** in Google Ads (for example, a
completed order on `/order/success`) so Google can tell which ads bring in orders.
