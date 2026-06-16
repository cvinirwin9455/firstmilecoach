# FirstRunCoach.com → FirstMileCoach.com Redirect Setup

You have a few options depending on where your domains are hosted:

---

## Option 1: DNS-Level Redirect (Easiest — if your registrar supports it)

Most registrars (GoDaddy, Namecheap, Google Domains, Cloudflare) have a "URL Forwarding" or "Redirect" option:

1. Go to your registrar's DNS settings for **firstruncoach.com**
2. Look for "URL Forwarding" or "Redirect"
3. Set it to forward to: `https://firstmilecoach.com`
4. Choose **301 (Permanent)** redirect type
5. Enable "Forward path" if available (so firstruncoach.com/anything → firstmilecoach.com/anything)

**This is the recommended approach** — no hosting needed for firstruncoach.com.

---

## Option 2: HTML Meta Redirect (if you need to host a file)

Use the `redirect/index.html` file included in this repo. Upload it as the index page for firstruncoach.com.

This uses a `<meta http-equiv="refresh">` tag to instantly redirect visitors.

---

## Option 3: .htaccess (Apache hosting)

If you're hosting on Apache, add this to your `.htaccess` file for firstruncoach.com:

```apache
RewriteEngine On
RewriteCond %{HTTP_HOST} ^(www\.)?firstruncoach\.com [NC]
RewriteRule ^(.*)$ https://firstmilecoach.com/$1 [R=301,L]
```

---

## Option 4: Netlify (_redirects file)

If hosting on Netlify, create a `_redirects` file:

```
/* https://firstmilecoach.com/:splat 301!
```

---

## Option 5: Vercel (vercel.json)

If hosting on Vercel, add to `vercel.json`:

```json
{
  "redirects": [
    {
      "source": "/(.*)",
      "destination": "https://firstmilecoach.com/$1",
      "permanent": true
    }
  ]
}
```

---

## Which should I use?

| Hosting setup | Best option |
|---|---|
| Just registered the domain, not hosting anything | Option 1 (DNS forwarding) |
| Hosting both on same server | Option 3 or 4 or 5 |
| Want a fallback in case DNS forwarding doesn't work | Option 2 (HTML redirect) |

For most people, **Option 1 is all you need**. It takes 2 minutes in your registrar dashboard.
