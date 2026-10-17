# altivia.fi website

A static site with no build step, in the Altivia brand (logo and blue from `assets/altivia-mark.png`): the company landing page, the Stoke page, and Stoke's Terms of Use and Privacy Policy.

| Path              | Page                                                    |
| ----------------- | ------------------------------------------------------- |
| `/`               | Altivia Oy: software consultancy landing page           |
| `/stoke/`         | Stoke: app page, also the store **Support URL**         |
| `/stoke/terms/`   | Terms of Use, generated from `docs/terms-of-use.md`     |
| `/stoke/privacy/` | Privacy Policy, generated from `docs/privacy-policy.md` |

The two legal pages are generated: edit the Markdown in `docs/` and run `node scripts/build-legal.mjs`, which also updates the in-app copies. Everything else is plain HTML with one stylesheet, `assets/site.css`.

Preview locally with `python3 -m http.server 8090 --directory website` and open http://localhost:8090 (paths are root-relative, so opening the files directly won't load the styles).

## Publishing on GitHub Pages

`CNAME` (the domain) and `.nojekyll` (serve files as they are) are for GitHub Pages.

1. On github.com, create a **public** repository, for example `altivia-website` (GitHub Pages on a free account needs a public repository; this site contains nothing private).
2. **Add file › Upload files**, and drag in everything inside `website/` (not the folder itself), including `CNAME` and `.nojekyll`. Commit to `main`.
3. **Settings › Pages**: Source **Deploy from a branch**, branch `main`, folder `/ (root)`. The custom domain should read `altivia.fi`.
4. At Domainhotelli, in altivia.fi's DNS: delete the `A` record `20.82.13.59` and add four `A` records for `altivia.fi`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`. Point `www` with a `CNAME` to `<your-github-username>.github.io`. Don't touch the mail records.
5. When GitHub shows the certificate is ready (minutes to a day), tick **Enforce HTTPS**.

To update the site later, upload the changed files to the same repository.
