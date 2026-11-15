# Writing With Pages CMS

Pages CMS provides a private editor for the blog. Markdown and media are saved to GitHub, and the existing Hugo workflow builds the published website.

## Open The Editor

Connect Tailscale on your iPhone or Mac, then open `https://cms.ts.autonate.dev`. Sign in using the `aut0nate` GitHub account and select `My-Blog`.

The self-hosted installation accepts only Nathan's GitHub account ID. Email sign-in is disabled. Its GitHub App should be installed on this repository only.

## Write A Post

1. Select **Blog posts** and create an entry.
2. Enter a title, publication date and short, lowercase tags.
3. Check that the proposed filename is `<Title Case Folder>/index.md`.
4. Write the article in Markdown. Source mode preserves code, HTML and Hugo gallery shortcodes exactly; visual editing is available for ordinary Markdown.
5. Add images using **Blog uploads** and insert the resulting `/uploads/...` URL. The source editor also supports normal Markdown image links.
6. Save to your writing branch while working. A branch in this public repository is publicly readable, even before publication.
7. Publish by merging the writing branch into `main`. The existing GitHub Actions workflow then rebuilds the blog.

Saving directly to `main` publishes the change after the build succeeds. The initial CMS setup does not introduce a separate draft flag or change existing posts.

## Add Media And Code

New CMS uploads live in `static/uploads` and are published at `/uploads`. Existing post folders and their relative image links remain supported.

Use useful alternative text for images:

```markdown
![A description of the screenshot](/uploads/example-screenshot.png)
```

Use fenced code blocks with a language name:

````markdown
```bash
docker compose ps
```
````

For audio and video, use an appropriate embed or HTML player in Source mode. Prefer a dedicated video host for large recordings rather than storing them in Git history. Media upload support does not automatically create a player in the article.

The CMS editor is not an exact preview of the Chirpy theme. Check the Hugo output before merging changes that affect galleries, embeds or layout. See [Blog Image Guidelines](image-guidelines.md) for existing gallery and screenshot conventions.

## Hosting And Access

The deployment definition belongs in the Docker Homelab repository under `stacks/pages-cms`. PostgreSQL stores login and cache data; article content stays in GitHub.

The existing `tools.autonate.dev` hostname also routes the signed GitHub webhook endpoint at `/api/webhook/github` to Pages CMS. Other paths continue serving IT Tools, and the editor is not exposed there. The editor and GitHub login callback use the private Tailscale address.
