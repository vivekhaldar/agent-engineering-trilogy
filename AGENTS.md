# Agent Instructions

## Repository Purpose

This repo is a static curriculum artifact for the Agent Engineering Trilogy. The main source file is `harness-engineering-curriculum.html`.

## Production Site

- Intended production domain: `harnesscourse.com`
- Hosting target: GitHub Pages, deployed from the root of `main`
- Root entrypoint: `index.html`, which redirects to `harness-engineering-curriculum.html`
- GitHub Pages custom-domain file: `CNAME`

Porkbun registration status as of 2026-05-27: `harnesscourse.com` was registered via the Porkbun API.

- Order ID: `10483845`
- Registration cost: `$11.08`
- Expiration: `2027-05-27 21:16:00`
- Auto-renew: enabled
- WHOIS privacy: enabled
- API access: enabled
- DNS records: none configured yet

Do not configure DNS while GitHub Pages is unavailable for this repository; pointing the domain at Pages before the custom domain is claimed creates an avoidable dangling-DNS risk.

GitHub Pages status as of 2026-05-27: enabling Pages for this private repository failed with `422 Your current plan does not support GitHub Pages for this repository`. Do not claim the site is live until one of these is done: make the repo public, use a plan/account that supports private-repo Pages, or deploy the static files to another public hosting target.

Expected Porkbun DNS records after GitHub Pages is enabled and configured with the custom domain:

```text
ALIAS  @    vivekhaldar.github.io
CNAME  www  vivekhaldar.github.io
```

If ALIAS flattening cannot be used, configure the GitHub Pages apex A records:

```text
A  @  185.199.108.153
A  @  185.199.109.153
A  @  185.199.110.153
A  @  185.199.111.153
```

## Working Rules

- Treat the HTML file as the product. Keep it directly openable in a browser.
- Do not add a framework, package manager, bundler, or generated asset pipeline unless Vivek explicitly asks for it.
- Keep the curriculum structure in this order: Prompt Engineering, Context Engineering, Harness Engineering, Capstone.
- Prefer inline links to stable primary sources. Bibliography-only links are not enough when the prose names a specific paper, article, or project.
- Preserve the existing visual language and typography unless the task is explicitly a redesign.
- Make edits in small, logical commits and stage files by name.
- After deployment-related edits, verify that `CNAME` still contains exactly `harnesscourse.com`.

## Verification

For content-only edits:

```sh
git diff --check
if rg -n "TODO|FIXME|Google search|Graduate Curriculum" harness-engineering-curriculum.html; then
  echo "Review the matches above before committing."
  exit 1
else
  echo "content scan ok"
fi
test "$(cat CNAME)" = "harnesscourse.com"
```

For JavaScript or table-of-contents behavior edits, also validate the inline script syntax:

```sh
node - <<'NODE'
const fs = require('fs');
const html = fs.readFileSync('harness-engineering-curriculum.html', 'utf8');
const match = html.match(/<script>([\s\S]*?)<\/script>/);
if (!match) throw new Error('No inline script found');
new Function(match[1]);
console.log('inline script syntax ok');
NODE
```

When possible, open the page locally after edits and skim the affected section in the browser.
