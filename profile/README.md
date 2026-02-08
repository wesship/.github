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

If your `wesship/supreme-ai-deployment-hub` app is failing in production, this repo now includes a hardened GitHub Actions workflow at `.github/workflows/supreme-ai-deploy.yml`.

It performs:
- dependency installation and app validation (`npm ci`, lint, tests, build),
- container image publishing to GHCR,
- remote deployment via SSH,
- immediate health check retries with failure logs for faster debugging.

Required repository secrets:
- `DEPLOY_HOST`
- `DEPLOY_USER`
- `DEPLOY_SSH_KEY`
- `GHCR_USERNAME`
- `GHCR_TOKEN` (PAT with `read:packages`)

Optional repository secrets:
- `HEALTHCHECK_URL` (defaults to `http://localhost/health`)
- `DEPLOY_BIND_IP` (defaults to `127.0.0.1`; set to `0.0.0.0` only if you explicitly want public exposure)

Deployability checklist:
- Ensure your app image exposes port `3000` (or update `APP_PORT` in workflow).
- Ensure target VM has Docker + curl installed and SSH key access configured.
- Ensure GHCR package visibility and token permissions allow pull from deploy host.

Security hardening included:
- Deployment now binds service to `127.0.0.1` by default to reduce accidental public exposure (addresses common n8n exposure mistakes).
- GHCR login on the server uses `--password-stdin` to avoid leaking tokens in process args.

Vercel note:
- This repo only contains GitHub profile/workflow files and no Vercel project config, so Vercel-specific runtime errors must be fixed in the actual app repo (`wesship/supreme-ai-deployment-hub`).

Recommendations:
- Use environment protection rules for `production` (required reviewers + wait timer).
- Rotate deploy and GHCR credentials regularly and scope them minimally.
- Pin your app runtime with a tested Docker image base and keep lockfiles committed.
- Add smoke tests for your critical API routes after deploy.

This gives you a repeatable pipeline to debug failures earlier (in CI) and deploy only after checks pass.

Vercel deployment (for `https://vercel.com/wesships-projects`):
- A reusable workflow is available at `.github/workflows/vercel-deploy.yml` for app repos to call.
- Required repo secrets in the app repo: `VERCEL_TOKEN`, `VERCEL_ORG_ID`, `VERCEL_PROJECT_ID`.
- Supports Lovable-generated apps too (example project: `https://lovable.dev/projects/b5eb8a4d-3709-4e3f-930c-ab5ab4b96560`) by deploying from a configurable `working-directory`.
- Typical usage in the app repo:
  - `uses: wesship/.github/.github/workflows/vercel-deploy.yml@main`
  - `with.environment: production`
  - `with.production: true`
- The reusable workflow exports `deployment_url` so callers can post the deployed URL to PR comments/check summaries.
- If Vercel still errors, verify project linkage (`vercel pull`), build output (`vercel build`), and runtime env vars in the Vercel dashboard.

Go-live quick start:
- 1) Add the three Vercel secrets in your app repo: `VERCEL_TOKEN`, `VERCEL_ORG_ID`, `VERCEL_PROJECT_ID`.
- 2) Copy `.github/workflows/vercel-app-deploy-example.yml` into your app repo and adjust `working-directory` (for Lovable monorepos/subfolders).
- 3) Push to `main` and verify the workflow summary includes the `deployment_url` output.
- 4) In Vercel dashboard, set Production domain + environment variables, then run one manual `workflow_dispatch` smoke deploy.

