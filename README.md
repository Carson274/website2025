# acm@osu 2025 website


## Writing Posts
First create a folder chain in the `/src/routes/talks/` representing the day of
the publish. e.g. `/src/routes/talks/2025/Oct/2/`
Next make a `+page.md` file.
Copy the following post boilerplate into the markdown file:
```markdown
---
title: Display Title
author: Benny Beaver
desc: This is what will be used for the page description on google search
date: 2025/10/2
# Optional: render media above the post body
video: https://www.youtube.com/watch?v=VIDEO_ID
slides: /slides/2025-10-02-display-title.pdf
slidesTitle: Display Title slides
---
# Hello Internet!
```

Be sure to update the arguments in the `---` front matter section. Now you can
write the blog post content in markdown format after the second `---` section.

### Adding slides
To render slides directly on a talk page, export/download the deck as a PDF and
place it in `static/slides/`, for example:

```text
static/slides/2025-10-02-display-title.pdf
```

Then add this to the talk front matter to render one deck at the top of the page:

```yaml
slides: /slides/2025-10-02-display-title.pdf
slidesTitle: Display Title slides
```

For pages with multiple decks, such as lightning talks, import and use the
slides component in the markdown body:

```md
<script>
	import Slides from "$lib/Slides.svelte";
</script>

<Slides src="/slides/lightning-talk-1.pdf" title="Lightning Talk 1" />
<Slides src="/slides/lightning-talk-2.pdf" title="Lightning Talk 2" />
```

Files in `static/` are served from the site root, so
`static/slides/example.pdf` is available at `/slides/example.pdf`.

## Updating Projects
The projects page is generated from `src/routes/projects/projects.json`. To add
or edit a project, update that JSON file with these fields:

```json
{
	"author": "Project Author",
	"title": "Project Title",
	"link": "https://example.com/project",
	"description": "A short description of the project."
}
```

The projects page imports this JSON at build time and the site is prerendered,
so project content is statically rendered into the generated page. There is no
client-side fetch or loading loop for project data.

## Deployment
This website is deployed with GitHub Pages.

Deployments are automatic: once code lands in the `main` branch, GitHub Pages
will build and publish the site. (The `./ship.sh` script is left over from when
the site was hosted with OSU's www engineering servers)

You can still run `npm run build` locally before merging to verify that the site
builds successfully.
