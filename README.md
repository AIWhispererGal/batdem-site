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

## Demos

`demos/` holds standalone single-file apps linked from the landing page. **Every folder in it is generated**: each app lives in its own repository, and a GitHub Action there builds the app and pushes the result here on every push to that repository's `main`. Edit the app in its repository, not here, or the next deploy overwrites your change.

| Demo | Source repository | App folder in that repository |
|---|---|---|
| `demos/queryquest` | `adaptive-sql-learning` | `adaptive-sql-trainer` |
| `demos/shellquest` | `adaptive-cli-learning` | `visual-cli-learning-platform` |
| `demos/lsat-dojo` | `adaptive-lsat-learning` | `adaptive-lsat-trainer` |
| `demos/neuron-evolution` | `neuron-evolution-game` | `neuron-evolution-game` |
| `demos/calcare` | `single-payer-game` | `health-plan-impact-simulator` |
| `demos/vote-atlas` | `congressional-voting-correlation-tool` | `.` |

The shared workflow is `.github/workflows/publish-demo.yml` here. Each source repository has a short caller workflow that names its demo folder and app folder, plus an Actions secret `BATDEM_SITE_TOKEN` (a fine-grained token with Contents: Read and write on this repository). To add a new demo: copy one of those caller workflows into the new repository, set `demo` and `app_dir`, add the secret, and link `demos/<name>/` from `index.html`.
