# Servare Opus — Website

A site for your fractional executive-assistant-for-CEOs consulting business, built with [Astro](https://astro.build) (fast, free-to-host, no server required).

Pages: Home, Services, About, Blog (3 starter posts), Booking (Cal.com), Contact (Formspree).

---

## 1. Before you launch — two free accounts to set up

The site has two placeholders that need your real info swapped in.

### Cal.com (booking page)
1. Go to [cal.com](https://cal.com) and create a free account.
2. Create an event type called "Discovery Call" (or similar) — set your availability and call length.
3. Copy your booking link. It'll look like `cal.com/your-username/discovery-call`.
4. Open `src/pages/booking.astro`, find the `iframe src=` line, and replace
   `https://cal.com/your-username/discovery-call?embed=true` with your real link (keep `?embed=true` on the end).

### Formspree (contact page)
1. Go to [formspree.io](https://formspree.io) and create a free account (50 submissions/month free — plenty to start).
2. Create a new form, point it at your email.
3. Copy the form endpoint — it looks like `https://formspree.io/f/abcd1234`.
4. Open `src/pages/contact.astro` and replace `YOUR_FORM_ID` in the `action=` URL with your real ID.

---

## 2. Run it locally (optional, to preview changes)

Requires [Node.js](https://nodejs.org) installed on your computer.

```
cd servareopus-site
npm install
npm run dev
```

Open the URL it prints (usually `http://localhost:4321`).

---

## 3. Deploy for free — Netlify (recommended)

1. Create a free account at [netlify.com](https://netlify.com).
2. Put this project in a GitHub repo (easiest: create a new repo on github.com, then drag the `servareopus-site` folder's contents in via GitHub's web uploader, or use `git` if you're comfortable with it).
3. In Netlify: **Add new site → Import an existing project → connect GitHub → pick your repo.**
4. Build settings (Netlify usually auto-detects these for Astro):
   - Build command: `npm run build`
   - Publish directory: `dist`
5. Click **Deploy**. Netlify gives you a live URL like `random-name-123.netlify.app` within a minute or two.

(Vercel works the same way if you'd rather use that — same build command and output directory.)

---

## 4. Point your GoDaddy domain at it

Once your site is live on Netlify:

1. In Netlify: **Site settings → Domain management → Add a domain** → enter `servareopus.com`.
2. Netlify will show you DNS records to add (usually an **A record** pointing to Netlify's load balancer IP, plus a **CNAME** for `www`).
3. Log into GoDaddy → **My Products → DNS** for servareopus.com.
4. Add/edit the records Netlify gave you:
   - **A record**, host `@`, value = the IP Netlify shows you
   - **CNAME record**, host `www`, value = your `netlify.app` address
5. Remove any conflicting default GoDaddy "Parked" A records for `@`.
6. DNS changes can take anywhere from a few minutes to a few hours to propagate. Netlify will auto-issue a free HTTPS certificate once it detects the domain is pointed correctly.

---

## 5. Editing content later

- **Blog posts**: add a new `.md` file in `src/content/blog/` — copy the format of an existing post (title, description, pubDate up top, then the post body). It'll show up on `/blog` automatically.
- **Services/pricing/copy**: edit the `.astro` files in `src/pages/` directly — it's mostly plain text inside HTML tags.
- **Colors/fonts**: all in `src/styles/global.css` at the top (`--navy`, `--gold`, etc.).

After any edit, if deployed via GitHub, just push the change — Netlify rebuilds automatically.

---

## About "Claude Code"

You mentioned wanting to use Claude Code — that's Anthropic's separate command-line coding tool, which runs on your own computer. This site was built directly here in this chat instead, so there's nothing else you need to install to get this project. If you'd like, you can still open this project folder in Claude Code later to keep editing it from your terminal — it'll work with this codebase as-is.
