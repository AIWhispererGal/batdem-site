# batdem-site

Single-page static site for BATDEM LLC, served at batdem.com via a Render Static Site.

## One-time setup (human steps, ~10 minutes)

1. **Create the GitHub repo.** New repo `batdem-site` (public or private), push this folder:
   ```
   git init
   git add .
   git commit -m "Initial BATDEM landing page"
   git branch -M main
   git remote add origin git@github.com:<you>/batdem-site.git
   git push -u origin main
   ```
2. **Create the Render Static Site.** Render dashboard → New → Static Site → connect the repo.
   - Branch: `main`
   - Build command: *(leave empty)*
   - Publish directory: `.`
   Render static sites are free and auto-deploy on every push to main.
3. **Attach the custom domain.** On the static site → Settings → Custom Domains → add `batdem.com` and `www.batdem.com`. Render shows the DNS records it wants.
4. **Update DNS at the registrar.** Remove the current forwarding/redirect to mgallagh.com. Add the A/ALIAS record for the apex and the CNAME for `www` exactly as Render displays them. TLS is automatic once DNS propagates (minutes to a few hours).
5. **Squarespace side.** If batdem.com is registered through Squarespace, the redirect lives in Domains → batdem.com → forwarding rules — delete the forward, then manage DNS records there per step 4.

## Ongoing updates (agent loop)

All content lives in `index.html`. To update the site: edit, commit, push to `main`. Render redeploys automatically — no dashboard interaction needed. See the `batdem-site-maintenance` skill for the rules agents should follow when editing.
