# Agent Engineering Trilogy

This repository contains a single-page curriculum for the agent engineering trilogy:

1. Prompt Engineering Curriculum
2. Context Engineering Curriculum
3. Harness Engineering Curriculum
4. Capstone: From Harness to Agent

The central thesis is that these are not three independent courses. They are one argument about where AI engineering leverage has moved: from controlling individual model calls, to constructing the context around those calls, to designing the harnesses that turn model calls into reliable systems.

## Site

The intended production domain is:

- https://harnesscourse.com

The repo is configured for GitHub Pages from the root of `main`:

- `CNAME` declares the custom domain.
- `index.html` redirects the site root to the curriculum page.
- `harness-engineering-curriculum.html` is the canonical curriculum artifact.

Operational note: the Porkbun API registration attempt for `harnesscourse.com` returned `INSUFFICIENT_FUNDS` because API purchases spend account credit. Add Porkbun account credit or complete web checkout, then configure DNS to GitHub Pages.

GitHub Pages note: enabling Pages for this private repository returned `422 Your current plan does not support GitHub Pages for this repository`. To publish from this repo on GitHub Pages, either make the repository public, use an account/plan that supports private-repo Pages, or move the static site to a public hosting repository.

## Contents

- [harness-engineering-curriculum.html](./harness-engineering-curriculum.html) - the complete self-contained curriculum page.
- [index.html](./index.html) - root redirect for GitHub Pages/custom-domain hosting.
- [CNAME](./CNAME) - GitHub Pages custom-domain declaration.

## Viewing

Open the HTML file directly in a browser:

```sh
open harness-engineering-curriculum.html
```

There is no build step, package manager, or local server requirement.

## Deployment

Pushing to `main` is the deployment mechanism once GitHub Pages is enabled for the repository.

Expected GitHub Pages settings:

- Source: deploy from branch
- Branch: `main`
- Folder: `/`
- Custom domain: `harnesscourse.com`

Expected Porkbun DNS records after the domain is registered:

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

## Editing Notes

- Keep the page self-contained unless there is a strong reason to introduce a build system.
- Prefer stable primary-source links inline in the body text, not only in reading lists.
- Preserve the curriculum order: Prompt Engineering, Context Engineering, Harness Engineering, Capstone.
- Keep changes reviewable as small logical commits.
