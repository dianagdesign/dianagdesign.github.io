# Portfolio site

Static site, no build step. Everything in this folder is served as-is.

## Layout

```
index.html          home page (shell). Routes by hash: #case-rsm, #case-adcm, #case-mips, #case-qd,
                    #full-prototype, #article, #sandbox
case-*.html         full case studies, loaded into the case overlay
reel-*.html         the same case pages in "reel mode" for the home page screen strips
demo.html           the interactive prototype
article.html        the article
sandbox.html        chart and motion studies
assets/img/         images (named by source page, numbered, with a short content hash)
assets/fonts/       Funnel Display, Funnel Sans, Geist Mono (woff2), shared by every page
.nojekyll           tells GitHub Pages to serve files starting with an underscore and skip Jekyll
```

Pages are loaded into iframes by the shell, so they must stay on the same origin as index.html.
Keep the file names stable: the chat's link list will depend on them.

## Deploy to GitHub Pages

1. Put the contents of this folder at the root of the repo (index.html at top level).
2. Settings > Pages > Build and deployment: Source "Deploy from a branch", branch `main`, folder `/ (root)`.
3. Wait for the first deploy, then open the `*.github.io/<repo>` URL to check it.
4. Custom domain: Settings > Pages > Custom domain. Enter the domain, tick "Enforce HTTPS" once
   the certificate is issued. GitHub writes a `CNAME` file into the repo for you.
   At your DNS provider, add the records GitHub's "Managing a custom domain" page lists for an
   apex domain (four A records plus optionally AAAA) and a `www` CNAME to `<user>.github.io`.

## Local preview

Any static server works. From this folder:

```
python3 -m http.server 8000
```

then open http://localhost:8000. Opening index.html directly from the file system will not work,
because the iframes need a real origin.

## Adding the contact form and the chat

- `contact.html`: a plain form page. Posts to the backend endpoint, never to an email address in the page.
- `ask.html`: the chat page. Same shell styles, calls the backend endpoint.
- Both pages should include `<meta name="robots" content="noindex">`.
- The backend (bot check, rate limit, API key, email forwarding) lives on a separate host, not in this repo.
  The pages reference it by URL; nothing secret goes in here.

## Before going public

- This repo's history will be public. Start the public repo from a clean copy, one first commit.
- Set the commit author name and email you want shown before the first commit.
- Nothing here should name internal tools, colleagues, or partners.
