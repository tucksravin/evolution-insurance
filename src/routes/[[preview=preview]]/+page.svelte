<script lang='ts'>
  import DefaultButton from "$lib/components/Buttons/DefaultButton.svelte";
  import ContentWidth from "$lib/components/ContentWidth/ContentWidth.svelte";
  import SliderEvoInsurance from "$lib/components/FullWidth/SliderEvoInsurance.svelte";
  import ScreenWidthImage from "$lib/components/ScreenWidth/ScreenWidthImage.svelte";
  import { isFilled } from "@prismicio/client";
  import { PrismicImage, PrismicRichText } from "@prismicio/svelte";


	let { data } = $props();

	let viewpoortWidth=$state(1024)

	let content = data.page.data;
</script>


<svelte:window bind:innerWidth={viewpoortWidth} />

<ScreenWidthImage field={content.hero_image}>
	
	<div class="h-full w-full flex flex-col justify-between py-24">
		<div></div>
		<div>
			<h1 class="text-white text-left w-full">{content.title_line_one}</h1>
			<h1 class="text-white text-right w-full">{content.title_line_two}</h1>
		</div>
		<div class="flex flex-col w-80 text-[#554F45] gap-8">
			
				<PrismicRichText field={content.hero_subtitle} />
				{#if isFilled.link(content.hero_button)}
					<DefaultButton class="w-fit" href={content.hero_button.url}>{content.hero_button.text}</DefaultButton>
				{/if}
			
		</div>
	</div>
	
</ScreenWidthImage>
<section class="py-24 text-dark">
	<ContentWidth class="relative">
		<div class="absolute h-full w-[13px] bg-primary left-0 -translate-x-[400%]"></div>
		<div class="flex flex-col md:flex-row">
			<h4 class="md:w-1/4 md:pr-4">{content.s1_eyebrow}</h4>
			<div class="md:w-3/4 flex flex-col gap-20">
				<div class="w-64 flex flex-col gap-6">
					<PrismicRichText field={content.s1_body} />
				</div>
				<div class="flex flex-col md:flex-row w-full aspect-video">
					<div class="md:w-2/3 relative aspect-[4/3]">
						<SliderEvoInsurance contentArray={content.s1_slider}/>
					</div>
					<PrismicImage field={content.s1_static_image} class="md:w-1/3 md:pl-6 object-cover"/>
				</div>

			</div>

		</div>
	</ContentWidth>
</section>
