<script lang="ts">
	import projectsData from './projects.json';
	import {
		GithubIcon,
		GlobeIcon,
		PlayIcon,
		ImageIcon,
		ExternalLinkIcon,
	} from '@lucide/svelte';
	import DevpostIcon from '$lib/DevpostIcon.svelte';

	type ProjectLink = { type: string; url: string };
	type Project = {
		author: string;
		title: string;
		description: string;
		// Optional cover image (path under /static). Omit to show a placeholder.
		image?: string;
		links?: ProjectLink[];
	};

	const projects = projectsData as Project[];

	// Maps a link "type" to the icon component + accessible label shown on
	// each project card. Unknown types fall back to a generic external link.
	const linkMeta: Record<string, { icon: any; label: string }> = {
		github: { icon: GithubIcon, label: 'GitHub' },
		website: { icon: GlobeIcon, label: 'Live site' },
		devpost: { icon: DevpostIcon, label: 'Devpost' },
		demo: { icon: PlayIcon, label: 'Demo' },
	};

	function metaFor(type: string) {
		return linkMeta[type] ?? { icon: ExternalLinkIcon, label: type };
	}

	// A project's cover can be a still image or a short video clip; videos
	// autoplay as a silent loop, like an animated GIF but far smaller.
	function isVideo(src: string) {
		return /\.(mp4|webm|mov)$/i.test(src);
	}
</script>

<svelte:head>
	<title>Projects: acm@osu</title>
	<meta name="description" content="" />
	<meta property="og:title" content="" />
	<meta property="og:type" content="article" />
	<meta property="og:description" content="" />
</svelte:head>
<article class="w-full flex flex-col items-center">
	<header class="bg-acm-yellow px-8 py-16 text-white md:px-12 w-full">
		<div class="mx-auto max-w-6xl">
			<p class="mb-3 font-mono text-xl">
				member work / tools / experiments
			</p>
			<h1
				class="whitespace-nowrap font-heading text-[clamp(2.25rem,12vw,4.5rem)] font-extrabold leading-none md:text-8xl"
			>
				{"{projects}"}
			</h1>
			<p class="mt-6 max-w-3xl font-mono text-2xl">
				Explore what acm@osu members are building and find projects to
				learn from or contribute to.
			</p>
		</div>
	</header>

	<div class="w-full max-w-6xl px-5 py-8 lg:px-8 lg:py-12">
		<p class="prose prose-xl max-w-[50em] font-mono">
			Many acm@osu members are always working on projects. In an effort to
			promote what they are working on this is a list of we're up to. If
			any of these projects peak your interest, reach out to see how you
			can contribute.
		</p>

		<div class="mt-10 grid gap-8 sm:grid-cols-2">
			{#each projects as project}
				<article
					class="flex flex-col overflow-hidden rounded-xl border border-gray-200 bg-white shadow-sm transition-shadow hover:shadow-md"
				>
					{#if project.image && isVideo(project.image)}
						<video
							src={project.image}
							class="aspect-video w-full object-cover"
							autoplay
							loop
							muted
							playsinline
							aria-label={project.title}
						></video>
					{:else if project.image}
						<img
							src={project.image}
							alt={project.title}
							class="aspect-video w-full object-cover"
						/>
					{:else}
						<div
							class="flex aspect-video w-full items-center justify-center bg-gradient-to-br from-acm-yellow to-acm-orange text-white"
						>
							<ImageIcon size="56" class="opacity-80" />
						</div>
					{/if}

					<div class="flex flex-1 flex-col p-6">
						<h3 class="font-heading text-2xl font-extrabold leading-tight">
							{project.title}
						</h3>
						<p class="mt-1 font-mono text-sm text-gray-500">
							{project.author}
						</p>
						<p class="mt-3 flex-1 text-gray-700">
							{project.description}
						</p>

						{#if project.links?.length}
							<div class="mt-5 flex flex-wrap gap-3">
								{#each project.links as link}
									{@const meta = metaFor(link.type)}
									<a
										href={link.url}
										target="_blank"
										rel="noopener noreferrer"
										title={meta.label}
										aria-label={meta.label}
										class="flex h-10 w-10 items-center justify-center rounded-full bg-gray-100 text-gray-700 transition-colors hover:bg-acm-orange hover:text-white"
									>
										<meta.icon size="20" />
									</a>
								{/each}
							</div>
						{/if}
					</div>
				</article>
			{/each}
		</div>
	</div>
</article>
