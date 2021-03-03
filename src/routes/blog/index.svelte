<script context="module">
	export function preload() {
		return this.fetch(`blog.json`).then(r => r.json()).then(posts => {
			return { posts };
		});
	}
</script>

<script>
	export let posts;
</script>

<style>
	ul {
		margin: 0 0 1em 0;
		line-height: 1.5;
	}
</style>

<svelte:head>
	<title>Blog</title>
</svelte:head>

<h1>Recent posts</h1>

<ul>
	{#each posts as post}
		<!-- we're using the non-standard `rel=prefetch` attribute to
				tell Sapper to load the data for the page as soon as
				the user hovers over the link or taps it, instead of
				waiting for the 'click' event -->
		<li><a rel="prefetch" href="blog/{post.slug}">{post.title}</a></li>
	{/each}
</ul>

<div class="sr-only">
	<!--You can iterate over the links from your preload fetch of posts-->
		{#each posts as { slug, title }}
			<a rel="prefetch" href="blog/{ slug }">{title}</a>
		{/each}
	<!--And manually put any links that are breaking as well (it means Sapper doesn't think you're using them)-->
	<a rel="prefetch" href="/someotherpage">Some page name for screen readers (nobody else sees it)</a>
</div>