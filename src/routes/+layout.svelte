<script lang='ts'>
	import { PrismicPreview } from '@prismicio/svelte/kit';
	import { page } from '$app/state';
	import { repositoryName } from '$lib/prismicio';
	import "../app.css";
  import { isFilled } from '@prismicio/client';
  import { PrismicImage, PrismicRichText } from '@prismicio/svelte';
  import ContentWidth from '$lib/components/ContentWidth/ContentWidth.svelte';
  import ArrowButton from '$lib/components/Buttons/ArrowButton.svelte';

	let { children, data } = $props();

	const nav = data.nav.data

	let showMenu=false;
</script>

<svelte:head>
	<title>{page.data.title}</title>
	{#if page.data.meta_description}
		<meta name="description" content={page.data.meta_description} />
	{/if}
	{#if page.data.meta_title}
		<meta name="og:title" content={page.data.meta_title} />
	{/if}
	{#if page.data.meta_image}
		<meta name="og:image" content={page.data.meta_image.url} />
		<meta name="twitter:card" content="summary_large_image" />
	{/if}
	<meta name="viewport" content="width=device-width, initial-scale=1.0 user-scalable=no">
</svelte:head>
<main>
	<div class="fixed top-0 left-0 w-screen p-4 h-24 z-10">
	<nav class="h-full w-full bg-dark text-white flex items-center justify-end md:justify-between rounded relative p-4">
		{#if isFilled.link(nav.left_link)}
			<a class="hidden md:block bump " href={nav.left_link.url}><h5 class="hover:opacity-80 transition">{nav.left_link.text}</h5></a>
		{/if}
		<button onclick={()=>showMenu=!showMenu} class="flex flex-row items-center justify-end gap-4 hover:opacity-80 transition"><h5 class="bump hidden md:block">Menu</h5><i class="bump fa-sharp fa-solid fa-bars fa-xl -translate-y-[2px]" ></i> </button>
		<a href='/' class="absolute hover:opacity-80 transition left-4 md:left-1/2 top-1/2 md:-translate-x-1/2 -translate-y-1/2 h-4 md:h-6 w-fit"><PrismicImage class="bump w-fit h-full" field={nav.logo_full} /></a>
	</nav>
	</div>
	{@render children?.()}
	<footer class="w-full bg-primary text-white md: py-8 md:py-12 min-h-screen flex flex-col justify-between relative z-20">
		<ContentWidth class="flex flex-col md:flex-row">
			<div class="flex flex-col md:w-1/4 gap-16">
				<a href='/' class="hover:opacity-80 transition h-4 md:h-6 w-fit"><PrismicImage class="bump w-fit h-full" field={nav.logo_small} /></a>
				<div class="w-full flex flex-col gap-8">
					<h4>Visit Us</h4>
					{#each nav.visit_addresses as addy }
					<div>
						<PrismicRichText field={addy.address} />
					</div>
					{/each}
				</div>
				<div class="w-full flex flex-col gap-8">
					<h4>Contact Us</h4>
					{#each nav.contact_us as addy }
					<div>
						<PrismicRichText field={addy.bodies} />
					</div>
					{/each}
				</div>
	
			</div>
			<div class="flex flex-col md:w-3/4 items-start gap-8">
				<h4>Explore</h4>
				{#each nav.nav_links as link}
					{#if isFilled.link(link)}
					<div>
						<ArrowButton text={link.text} href={link.url} />
					</div>
					{/if}
				{/each}
			</div>
		</ContentWidth>
		<ContentWidth class="flex flex-col md:flex-row items-center">
			<div class="flex flex-col md:w-1/4 text-light">
				<div class="label">Copyright © {new Date().getFullYear()} <br/> Evolution Insurance Partners </div>
	
			</div>
			<div class="flex flex-col md:flex-row gap-16 md:w-3/4">
				{#each nav.partners as partner}
					<PrismicImage class="h-12 w-fit" field={partner.logo} />
				{/each}
			</div>
		</ContentWidth>
		

	</footer>
</main>
<PrismicPreview {repositoryName} />
