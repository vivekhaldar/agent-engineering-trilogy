# Agent Instructions

## Repository Purpose

This repo is a static curriculum artifact for the Agent Engineering Trilogy. The main source file is `harness-engineering-curriculum.html`.

## Production Site

- Intended production domain: `harnesscourse.com`
- Repository visibility: public
- Hosting target: GitHub Pages, deployed from the root of `main`
- Root entrypoint: `index.html`, which redirects to `harness-engineering-curriculum.html`
- GitHub Pages custom-domain file: `CNAME`

Porkbun DNS records: apex `ALIAS` to `vivekhaldar.github.io`; `www` `CNAME` to `vivekhaldar.github.io`. Do not put registrar order IDs, billing details, renewal dates, or account settings in this public repository.

GitHub Pages status as of 2026-05-27: Pages is enabled for `main` `/` with `harnesscourse.com` as the custom domain. HTTPS enforcement may remain unavailable immediately after DNS setup until GitHub issues the custom-domain certificate. If `https_enforced` is still false later, retry the Pages update after the certificate exists.

Expected Porkbun DNS records:

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

To enable HTTPS once the GitHub Pages certificate exists:

```sh
gh api --method PUT repos/vivekhaldar/agent-engineering-trilogy/pages \
  -F cname=harnesscourse.com \
  -F https_enforced=true \
  -F 'source[branch]=main' \
  -F 'source[path]=/'
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
