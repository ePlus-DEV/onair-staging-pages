# ePlus OnAir — Staging Pages

**Listen Beyond Borders.** This public repository holds the **generated static website** for ePlus OnAir staging. It is **not** the source-code repository.

| Property | Value |
| --- | --- |
| Website hostname | https://stg.radio.eplus.dev |
| Source repository | [ePlus-DEV/radio.eplus.dev](https://github.com/ePlus-DEV/radio.eplus.dev) |
| Source branch | `staging` |
| GitHub Environment | `staging` (legacy `development` fallback only during migration) |
| Published website branch | `main` (this repository) |

> [!IMPORTANT]
> **Generated output — do not manually edit HTML, CSS, JavaScript, radio catalogs, `CNAME` or artwork here.** The next trusted source deployment replaces generated files.

## How releases reach this repository

1. Maintainers merge verified feature PRs into the source `staging` branch. Production releases use a separate reviewed `staging` → `main` PR.
2. [Deploy ePlus OnAir to GitHub Pages](https://github.com/ePlus-DEV/radio.eplus.dev/actions/workflows/deploy-github-pages.yml) builds and tests the website, checks the exact target repository, configured hostname and token permissions, and audits output size.
3. The workflow publishes Nuxt static output to this repository's `main` branch. The root `CNAME` is restored and this `README.md` is preserved by the publishing workflow.
4. This repository's GitHub Pages settings serve branch `main` at `/(root)` for the configured custom domain.

Automatic Staging publishing uses source repository Actions Variable `PAGES_STAGING_READY=true` and Environment `staging`, with `NUXT_PUBLIC_SITE_URL=https://stg.radio.eplus.dev` and its scoped `PAGES_DEPLOY_TOKEN`. If the new flag is unset, the workflow temporarily retains the documented legacy `development`/`PAGES_DEV_READY` fallback; explicitly false disables Staging.

## Indexing and image policy

**Staging is deliberately `noindex`**: no production sitemap, canonical or GA4 is emitted from the `staging` deployment. The separate `main` production Pages build is indexable and includes a production sitemap, canonical links and GA4 (`G-ETDY41KBBJ`). A successful Pages push alone does not verify live DNS or TLS routing. The legacy `new-radio.eplus.dev` domain is no longer this repository's Pages custom hostname.

Regular website builds use `npm run generate:site`, retaining station logos but excluding the large per-station Open Graph JPEG collection so the published site stays under the GitHub Pages **1 GB site limit**.

The retired per-station image publishing workflow is no longer part of the release path; regular Pages builds use the shared brand social image unless a separately verified external manifest is configured.

## Maintainership

- Make application, station-data, player, SEO, or CI changes **in the source repository** through pull requests.
- Check source [README](https://github.com/ePlus-DEV/radio.eplus.dev/blob/main/README.md) and [deployment guide](https://github.com/ePlus-DEV/radio.eplus.dev/blob/main/docs/GITHUB_PAGES.md) for the branch map, configuration and release procedure.
- Never commit deployment tokens, private configuration or credentials into this public repository.
- If this README disappears after a redeploy, verify that the source publisher still excludes `/README.md` when syncing with `rsync --delete`.

Maintained by **ePlus.DEV** · ePlus OnAir — Listen Beyond Borders.
