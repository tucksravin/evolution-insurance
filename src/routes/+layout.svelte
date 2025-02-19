<script lang='ts'>
	import { PrismicPreview } from '@prismicio/svelte/kit';
	import { page } from '$app/state';
	import { repositoryName } from '$lib/prismicio';
	import "../app.css";
  import { isFilled } from '@prismicio/client';
  import { PrismicImage, PrismicRichText } from '@prismicio/svelte';
  import ContentWidth from '$lib/components/ContentWidth/ContentWidth.svelte';
  import ArrowButton from '$lib/components/Buttons/ArrowButton.svelte';
  import { fly} from 'svelte/transition';

	let { children, data } = $props();

	const nav = data.nav.data

	let showMenu=$state(false);
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
{#if showMenu}
<div class="h-screen w-screen fixed z-30 bg-primary text-white left-0 top-0" transition:fly={{x:'100%'}}>
	
	<ContentWidth class="h-full relative">
		<button aria-label="close nav" onclick={()=>showMenu=false} class="absolute top-12 right-0"><i class="fa-sharp fa-solid fa-close"></i></button>
		<div class="flex flex-col md:w-3/4 py-24 items-start justify-center gap-8">
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

</div>
{/if}
<main class={showMenu?"pointer-events-none":""}>
	<div class="fixed top-0 left-0 w-screen p-4 h-24 z-10">
	<nav class="h-full w-full bg-dark text-white flex items-center justify-end md:justify-between rounded relative p-4">
		{#if isFilled.link(nav.left_link)}
			<a class="hidden md:block bump " href={nav.left_link.url}><h5 class="hover:opacity-80 transition">{nav.left_link.text}</h5></a>
		{/if}
		<button onclick={()=>showMenu=true} class="flex flex-row items-center justify-end gap-4 hover:opacity-80 transition"><h5 class="bump hidden md:block">Menu</h5><i class="bump fa-sharp fa-solid fa-bars fa-xl -translate-y-[2px]" ></i> </button>
		<a href='/' class="absolute hover:opacity-80 transition left-4 md:left-1/2 top-1/2 md:-translate-x-1/2 -translate-y-1/2 h-4 md:h-6 w-fit"><PrismicImage class="bump w-fit h-full" field={nav.logo_full} /></a>
	</nav>
	</div>

	{@render children?.()}
	<footer class="w-full bg-primary text-white pt-36 pb-12  relative">
		<ContentWidth class="h-full relative min-h-[50vh] flex flex-col justify-between">
			<div class="hidden lg:block absolute h-full w-[13px] bg-dark left-0 -translate-x-[400%]"></div>
		<div class="flex flex-col md:flex-row relative w-full">
			
			<div class="flex flex-col md:w-1/4 gap-16">
				<a href='/' class="hover:opacity-80 transition h-4 md:h-6 w-fit"><PrismicImage class="bump w-fit h-full" field={nav.logo_small} /></a>
				<div class="w-full flex flex-col gap-4">
					<h5>Visit Us</h5>
					{#each nav.visit_addresses as addy }
					<div>
						<PrismicRichText field={addy.address} />
					</div>
					{/each}
				</div>
				<div class="w-full flex flex-col gap-4">
					<h5>Contact Us</h5>
					<p>{nav.telephone}</p>
				</div>
				<div class="w-full flex flex-col gap-4">
					<h5>Mailing Address</h5>
					<div>
						<PrismicRichText field={nav.mailingaddress} />
					</div>
				</div>
	
			</div>
			<div class="flex flex-col md:w-3/4 items-start gap-8 mt-16 md:mt-0">
				<h5>Explore</h5>
				{#each nav.nav_links as link}
					{#if isFilled.link(link)}
					<div>
						<ArrowButton text={link.text} href={link.url} />
					</div>
					{/if}
				{/each}
			</div>
		</div>
		<div class="flex flex-col-reverse items-start md:flex-row md:items-center relative w-full mt-16 md:mt-36">
	
			
			<div class="flex flex-col md:w-1/4 text-light mt-16 md:mt-0">
				<div class="label">Copyright © {new Date().getFullYear()} <br/> Evolution Insurance Partners </div>
	
			</div>
			<div class="flex flex-col md:flex-row gap-16 md:w-3/4 ">
				{#each nav.partners as partner}
					<PrismicImage class="h-16 md:h-12 w-fit" field={partner.logo} />
				{/each}
			</div>
		</div>
		</ContentWidth>
		

	</footer>
</main>
<PrismicPreview {repositoryName} />
