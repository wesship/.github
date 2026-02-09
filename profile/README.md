### Hi there, this is n8n 👋

n8n is a low-code automation tool. With over 220 pre-built integrations and a general connector for anything with an API, n8n enables you to connect anything to everything. With n8n you can move beyond simple one step integrations to build multi-step workflows that integrate your tools exactly the way you want, including adding AI functionality. Thanks to its <a href="https://faircode.io/">fair-code</a> distribution model, n8n will always have visible source code, be available to self-host, have a free community edition, and allow you to add your own custom functions, logic, and apps.

- Check out <a href="https://github.com/n8n-io/n8n">our main project here.</a>
- Interested in working for n8n? See our<a href="https://n8n.io/careers"> open positions</a>.
- Learn more how to <a href="https://docs.n8n.io/hosting/">self-host n8n in our docs</a>. 
- Want to quickly test out n8n? <a href="https://n8n.io/get-started/?utm_medium=referral&utm_source=github.com&utm_campaign=readme">Download our desktop app</a> to see what the fuss is all about. 
- Not interested in hosting n8n yourself? We also offer <a href="https://n8n.io/cloud/?utm_medium=referral&utm_source=github.com&utm_campaign=readme">n8n cloud</a> for a monthly fee. 
- Both our team and our users have been building a <a href="https://n8n.io/workflows/?utm_medium=referral&utm_source=github.com&utm_campaign=readme">workflow template library</a> to help others easily get started with n8n automations. 


![Image](https://n8niostorageaccount.blob.core.windows.net/n8nio-strapi-blobs-prod/assets/github_screen_2_86155234c3.png "Stripe to Hubspot to Slack")

 We launched in 2019 with a ton of interest, and things have accelerated since then:

- 📈 With 100m+ Docker pulls and a huge active user base/community - we're already building global traction
- ⭐️ With 40k stars, we are now in the top 600 of the 238m projects on GitHub
- 🌱 We were Sequoia's first seed investment in Germany, and recently raised a $12m Series A round, led by Felicis Ventures

We're on a mission to give technical superpowers to everyone with a computer. <a href="https://n8n.io/careers">Join us!</a>

## Supreme AI Deployment Hub: debug + deploy workflow

If your `wesship/supreme-ai-deployment-hub` app is failing in production, this repo now provides reusable workflows that your app repo can call.

Available workflows:
- `.github/workflows/supreme-ai-deploy.yml`: reusable CI/CD workflow for validate -> containerize -> SSH deploy.
- `.github/workflows/vercel-deploy.yml`: reusable Vercel workflow for `vercel pull`, `vercel build`, and `vercel deploy --prebuilt`.

For Supreme AI server deploy callers, provide these required secrets from the app repo:
- `DEPLOY_HOST`
- `DEPLOY_USER`
- `DEPLOY_SSH_KEY`
- `GHCR_USERNAME`
- `GHCR_TOKEN` (PAT with `read:packages`)

Recommended inputs when calling `supreme-ai-deploy.yml`:
- `healthcheck-url` (default: `http://localhost/health`)
- `bind-ip` (default: `127.0.0.1`; set `0.0.0.0` only when you intentionally expose publicly)
- `app-port` / `host-port` (defaults: `3000` / `80`)

Deployability checklist:
- Ensure your app repo includes a valid `package.json`, lockfile, and `Dockerfile`.
- Ensure target VM has Docker + curl installed and SSH key access configured.
- Ensure GHCR package visibility and token permissions allow pull from deploy host.

Security hardening included:
- Deployment binds service to `127.0.0.1` by default to reduce accidental public exposure.
- GHCR login on the server uses `--password-stdin` to avoid leaking tokens in process args.

Vercel deployment (for `https://vercel.com/wesships-projects`):
- Required app-repo secrets: `VERCEL_TOKEN`, `VERCEL_ORG_ID`, `VERCEL_PROJECT_ID`.
- Supports Lovable-generated apps too (example project: `https://lovable.dev/projects/b5eb8a4d-3709-4e3f-930c-ab5ab4b96560`) by deploying from a configurable `working-directory`.
- The reusable workflow exports `deployment_url` so callers can post the deployed URL to PR comments/check summaries.

Go-live quick start:
- 1) Add required secrets in your app repo.
- 2) Copy `.github/workflows/vercel-app-deploy-example.yml` into your app repo.
- 3) Add a second caller workflow in the app repo for `wesship/.github/.github/workflows/supreme-ai-deploy.yml@main`.
- 4) Run one manual `workflow_dispatch` in each workflow and confirm health checks / deployment URL output.

