# Essence of Childcare University — website

Static site. No build step, no dependencies, no server code.
Every file here ships as-is.

    index.html          the whole site (9 pages, hash routing)
    img/                28 photos + the transparent logo
    og-image.jpg        social share card
    favicon*, apple-touch-icon.png
    robots.txt, sitemap.xml
    vercel.json         clean URLs, cache headers, security headers

---

## 1. Deploy to Vercel

### If you use GitHub (recommended, gives you auto-deploy on every push)

1. Make a new repo, for example `essence-childcare`.
2. Copy everything in this folder into it, commit, push.
3. Go to vercel.com/new and import the repo.
4. Framework Preset: **Other**. Leave Build Command and Output Directory empty.
5. Click Deploy.

From then on, every push to `main` redeploys automatically.

### If you want it up in two minutes without GitHub

    npm i -g vercel
    cd path/to/this/folder
    vercel            # answer the prompts, take the defaults
    vercel --prod     # promote it to the live URL

---

## 2. Replace the domain placeholder

The first deploy gives you a URL like `essence-childcare.vercel.app`.
Search these three files for `REPLACE-WITH-YOUR-DOMAIN.vercel.app` and put your
real domain in its place:

    index.html      (canonical, og:url, og:image, twitter:image)
    robots.txt      (sitemap line)
    sitemap.xml     (loc)

The site works fine before you do this. It only affects link previews in
iMessage, Facebook and Instagram, plus what Google indexes.

Redeploy after editing.

---

## 3. Make the forms actually deliver

Until you do this, submitting a form shows the parent an amber panel saying
nothing was sent and asking them to call. That is deliberate. It never
pretends a message arrived.

1. Sign up at formspree.io (free tier is fine at this volume) or usebasin.com.
2. Create a form and point it at the ECU business email.
3. Copy the endpoint URL. It looks like `https://formspree.io/f/xxxxxxxx`.
4. Open `index.html`, find this block near the bottom:

        var ECU = {
          formEndpoint: "",            //  <-- paste the form endpoint URL here
          email:        "",            //  <-- ECU business email, once it exists

5. Paste the URL between the quotes on `formEndpoint`. Redeploy.

All three forms, enrollment, careers and contact, switch over at once. The
confirmation changes to a real green "we received your inquiry" panel.

---

## 4. Custom domain

In Vercel: Project → Settings → Domains → Add.
Vercel shows the exact DNS records. Add them at whoever sells the domain.
HTTPS is issued automatically, usually within a few minutes.

---

## 5. Tell Google it exists

1. search.google.com/search-console → add your domain → verify.
2. Submit `https://yourdomain.com/sitemap.xml`.
3. Separately, claim the Google Business Profile for
   5644 W. Appleton Ave. For a daycare, the Business Profile brings far more
   calls than the website does. Put the website URL on it.

---

## Editing content later

Everything is in `index.html`. Real text, no CMS, no templating.
Search for the words you see on the site and change them in place.

Photos live in `img/`. Replacing a file with the same name swaps it
everywhere it appears.

The page titles per section and the structured data block near the bottom
(`application/ld+json`) carry the business name, address, hours and phone
for search engines. Update those if the details change.
