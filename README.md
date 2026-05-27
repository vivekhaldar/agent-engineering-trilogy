# Agent Engineering Trilogy

This repository contains a single-page curriculum for the agent engineering trilogy:

1. Prompt Engineering Curriculum
2. Context Engineering Curriculum
3. Harness Engineering Curriculum
4. Capstone: From Harness to Agent

The central thesis is that these are not three independent courses. They are one argument about where AI engineering leverage has moved: from controlling individual model calls, to constructing the context around those calls, to designing the harnesses that turn model calls into reliable systems.

## Contents

- [harness-engineering-curriculum.html](./harness-engineering-curriculum.html) - the complete self-contained curriculum page.

## Viewing

Open the HTML file directly in a browser:

```sh
open harness-engineering-curriculum.html
```

There is no build step, package manager, or local server requirement.

## Editing Notes

- Keep the page self-contained unless there is a strong reason to introduce a build system.
- Prefer stable primary-source links inline in the body text, not only in reading lists.
- Preserve the curriculum order: Prompt Engineering, Context Engineering, Harness Engineering, Capstone.
- Keep changes reviewable as small logical commits.
