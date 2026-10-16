# GitHub Profile README — Install & Troubleshoot

This package is for https://github.com/MohammedNasr51/MohammedNasr51.

## What changed

- Replaced the Capsule Render header that showed an XML error. The new banner is a validated, self-hosted SVG at `assets/header.svg`. No dynamically generated SVG text or external rendering service.
- Replaced the Capsule Render footer with `assets/footer.svg`.
- Kept a locally hosted animated typing introduction at `assets/typing-intro.gif`.
- Replaced external Vercel-based activity/stats endpoints with real-data cards generated through GitHub Actions and saved in `output/tokyonight/`.
- Preserved the colorful badges, icon rows, team-project cards, and truthful personal contributions.

## Upload

1. Download and unzip the package.
2. Copy **README.md**, **assets/**, **output/**, and **.github/workflows/profile-metrics.yml** into the root of your `MohammedNasr51/MohammedNasr51` repository. Preserve the directories and file names.
3. Commit the files to `main`.
4. In GitHub, open **Actions** → **Generate profile metrics** → **Run workflow**.
5. Wait for the workflow to succeed and commit the generated SVG cards to `output/tokyonight/`.
6. Refresh your GitHub profile (GitHub may cache image previews temporarily).

**Important:** The three images under `output/tokyonight/` are transparent about being setup placeholders until the workflow runs successfully. Their displayed values are *not* fabricated stats. The Action replaces them with your real public data.

## Permissions and metrics

- The workflow uses GitHub's built-in `${{ github.token }}` and explicitly requests `contents: write` so it can update generated SVG assets; you do not need a PAT to start with public data.
- Some repository/org settings restrict Actions write permissions. If GitHub refuses the push, check **Settings** → **Actions** → **General** → **Workflow permissions** and allow **Read and write permissions** if available (or adjust repository/organization policy).
- The current configuration uses **only public contribution data** and `include_private: false`. Private activity may appear on your native GitHub profile but not in these cards. Including private contributions requires additional account permissions and a personal access token; do not place any token in the README or committed files.
- Public GitHub contribution counts can differ from raw git commit counts due to GitHub's attribution rules, time windows, and repository visibility.
- The workflow runs once each day and can also be triggered manually.

## If the metrics workflow fails

- Go to **Actions** → **Generate profile metrics**, open the failing run, and read its logs.
- Confirm the profile repo is named exactly `MohammedNasr51/MohammedNasr51` and the default branch is `main`.
- Check whether GitHub Actions are enabled and permitted to push commits to your branch.
- If the action reports that a user query needs additional privileges, create a narrowly scoped personal access token and save it as a repository secret (never paste it in a file), then adjust `token:` to reference the secret.
- If GitHub limits access to organization contributions or private work, the default workflow still aims to display whatever public data it can retrieve.

## Why the old banner broke

The previous third-party banner generated an SVG error (`xmlParseEntityRef: no name`), consistent with unescaped ampersands in text such as `React & TypeScript`. The local SVG encodes the ampersand correctly as `&amp;` and is validated as XML.

## Why the old graph broke

The chart service itself displayed "This deployment is temporarily paused." The fix is to **generate SVGs during your own GitHub Action and commit them**, rather than depending on that chart service at viewing time.

## Credits

Contribution SVG generation uses `tiennm99/ghstats@v1`:
https://github.com/tiennm99/ghstats

GitHub profile: https://github.com/MohammedNasr51
