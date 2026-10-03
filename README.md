# remm.dev

A small custom Hugo site. Posts are Markdown; project cards are TOML.

## Preview and build

Use Hugo Extended v0.167.0 or later (the installed version used for validation).

```powershell
hugo server -D
```

Open http://localhost:1313. Draft posts are visible with `-D`.

```powershell
hugo --minify
```

This builds the publishable site in `public/`. Drafts are excluded.

## Write a post

```powershell
hugo new content posts/my-new-post/index.md
```

Using `index.md` creates a page bundle: keep images beside the article.
Set a description and tags, then change `draft = true` to `false` when ready.
The `archetypes/posts.md` file controls the starter content.

The table of contents appears automatically on posts with at least 600 words
and level 2 or 3 headings. Add `toc = true` to force it on a short post or
`toc = false` to hide it.

## Add images

```text
content/posts/my-new-post/
  index.md
  benchmark.png
```

In Markdown:

```markdown
![Describe what the chart shows](benchmark.png "Optional caption")
```

Hugo creates WebP versions up to 1440 pixels wide with a responsive `srcset`.
Images include intrinsic dimensions, lazy loading, and asynchronous decoding.
Small originals are never enlarged. GIF animation and SVG files are preserved.

Shared images can go in `assets/images/`; reference them as
`/images/filename.jpg`. Images in `static/` and remote URLs display as supplied
and scale with CSS, but are not resized during the build.

Use descriptive alt text. A title on a standalone image becomes its caption.

## Update project cards

Edit `data/projects.toml`. Cards appear in file order.

```toml
[[projects]]
title = 'My Project'
description = 'A short description.'
technologies = ['C++', 'CUDA']
page = '/posts/my-new-post' # optional internal article
# url = 'https://github.com/your-name/project' # optional external link
# image = '/images/project.jpg' # optional image in assets/images
# image_alt = 'Describe the project image'
```

Cards without a link still display their description and technologies.
The original CUDA, camera, and game engine descriptions are the starting cards.

## Topics, feeds, and sharing

Use `tags = ['CUDA', 'C++']` in a post. Hugo builds the topic pages.
`content/tags/c++/_index.md` gives the C++ topic the readable `/tags/cpp/` URL.
Templates use Hugo's term URLs so the links stay consistent.

- All writing: `/posts/`
- Topics: `/tags/`
- Writing feed: `/posts/index.xml`
- Home feed, containing posts only: `/index.xml`
- Sitemap: `/sitemap.xml`

The favicon is `static/favicon.svg`. The default social image is
`static/images/social.png`. To override it for a post, add
`images = ['cover.jpg']` and put that image beside its `index.md`, or use
a path to an image under `static/`.

Dark mode follows the reader's system preference. Syntax highlighting adapts
to the same preference. No JavaScript is required.

Before deployment, check `baseURL`, your name, description, and GitHub link in
`hugo.toml`, and review the sample posts. GitHub deployment is the next step.
