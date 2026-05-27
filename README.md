# Agent Engineering Trilogy

This repository contains a single-page curriculum for the agent engineering trilogy:

1. Prompt Engineering Curriculum
2. Context Engineering Curriculum
3. Harness Engineering Curriculum
4. Capstone: From Harness to Agent

The central thesis is that these are not three independent courses. They are one argument about where AI engineering leverage has moved: from controlling individual model calls, to constructing the context around those calls, to designing the harnesses that turn model calls into reliable systems.

## Site

The production domain is:

- https://harnesscourse.com

The repo is public and configured for GitHub Pages from the root of `main`:

- `CNAME` declares the custom domain.
- `index.html` is the production curriculum page served at the site root.
- `harness-engineering-curriculum.html` is kept as a stable direct-file URL for local use and older links.

DNS status: Porkbun is configured with an apex `ALIAS` record and a `www` `CNAME` record pointing at GitHub Pages.

GitHub Pages status: Pages is enabled for `main` `/` with `harnesscourse.com` as the custom domain. HTTPS enforcement may remain unavailable immediately after DNS setup until GitHub issues the custom-domain certificate.

## Contents

- [index.html](./index.html) - the complete self-contained curriculum page served at the site root.
- [harness-engineering-curriculum.html](./harness-engineering-curriculum.html) - stable direct-file copy for local use and older links.
- [CNAME](./CNAME) - GitHub Pages custom-domain declaration.

## Viewing

Open the HTML file directly in a browser:

```sh
open index.html
```

There is no build step, package manager, or local server requirement.

## Deployment

Pushing to `main` is the deployment mechanism.

GitHub Pages settings:

- Source: deploy from branch
- Branch: `main`
- Folder: `/`
- Custom domain: `harnesscourse.com`

Porkbun DNS records:

```text
ALIAS  @    vivekhaldar.github.io
CNAME  www  vivekhaldar.github.io
```

If ALIAS flattening is unavailable, use GitHub Pages apex records instead:

```text
A  @  185.199.108.153
A  @  185.199.109.153
A  @  185.199.110.153
A  @  185.199.111.153
```

If HTTPS enforcement is still disabled after DNS changes, retry after GitHub has issued the Pages certificate:

```sh
gh api --method PUT repos/vivekhaldar/agent-engineering-trilogy/pages \
  -F cname=harnesscourse.com \
  -F https_enforced=true \
  -F 'source[branch]=main' \
  -F 'source[path]=/'
```

## Editing Notes

- Keep the page self-contained unless there is a strong reason to introduce a build system.
- Prefer stable primary-source links inline in the body text, not only in reading lists.
- Preserve the curriculum order: Prompt Engineering, Context Engineering, Harness Engineering, Capstone.
- Keep `index.html` and `harness-engineering-curriculum.html` in sync when changing curriculum content.
- Keep changes reviewable as small logical commits.
