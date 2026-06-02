<script lang="ts">
	import projects from './projects.json';
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
	<div
		class="prose prose-xl max-w-[50em] prose-headings:mt-0 p-5 lg:p-0 lg:py-8"
	>
		<p>
			Many acm@osu members are always working on projects. In an effort to
			promote what they are working on this is a list of we're up to. If
			any of these projects peak your interest, reach out to see how you
			can contribute.
		</p>

		<hr />

		{#each projects as project}
			<h3><a href={project.link}>{project.title}</a></h3>
			<h4>{project.author}</h4>
			<p>{project.description}</p>
		{/each}
	</div>
</article>
