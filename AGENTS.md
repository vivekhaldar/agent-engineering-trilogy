# Agent Instructions

## Repository Purpose

This repo is a static curriculum artifact for the Agent Engineering Trilogy. The main source file is `harness-engineering-curriculum.html`.

## Working Rules

- Treat the HTML file as the product. Keep it directly openable in a browser.
- Do not add a framework, package manager, bundler, or generated asset pipeline unless Vivek explicitly asks for it.
- Keep the curriculum structure in this order: Prompt Engineering, Context Engineering, Harness Engineering, Capstone.
- Prefer inline links to stable primary sources. Bibliography-only links are not enough when the prose names a specific paper, article, or project.
- Preserve the existing visual language and typography unless the task is explicitly a redesign.
- Make edits in small, logical commits and stage files by name.

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
