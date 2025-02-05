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
		<div class="hidden lg:block absolute h-full w-[13px] bg-primary left-0 -translate-x-[400%]"></div>
		<div class="flex flex-col md:flex-row">
			<h4 class="md:w-1/4 md:pr-4">{content.s1_eyebrow}</h4>
			<div class="md:w-3/4 flex flex-col gap-20">
				<div class="mt-6 md:mt-0 w-64 flex flex-col gap-6">
					<PrismicRichText field={content.s1_body} />
				</div>
				<div class="flex flex-col md:flex-row w-full aspect-video">
					<div class="w-full md:w-2/3 relative aspect-[4/3]">
						<SliderEvoInsurance contentArray={content.s1_slider}/>
					</div>
					<PrismicImage field={content.s1_static_image} class=" mt-24 md:mt-0 aspect-[3/4] md:aspect-auto w-full md:w-1/3 md:pl-6 object-cover"/>
				</div>

			</div>

		</div>
	</ContentWidth>
	<ContentWidth class="relative">
		<div class="hidden lg:block absolute h-full w-[13px] bg-primary left-0 -translate-x-[400%]"></div>
		<div class="h-52"></div>
		<div class="flex flex-col md:flex-row">
			<h4 class="md:w-1/4 md:pr-4">{content.s2_eyebrow}</h4>
			<div class="md:w-3/4 flex flex-col gap-20 md:gap-40">
				<div class="w-full flex flex-row justify-center flex-wrap text-primary">
					{#each content.s2_icons as value}
						<div class="w-1/2 lg:w-1/4 pr-4 pb-4 aspect-square flex flex-col items-center justify-center gap-12">
							<PrismicImage field={value.icon} class="w-2/3" />
							<span class="label">{value.label}</span>
						</div>
					{/each}
				</div>
				<div class="flex flex-col md:flex-row w-full text-dark">
					<div class="w-full md:w-1/3 relative aspect-[4/3] h-full flex flex-col items-start justify-between pr-8">
						<div>
							<PrismicImage field={content.s3_icon} class="w-14"/>
							<h3 class="mt-3">{content.s3_title}</h3>
						</div>
						<div class="flex flex-col gap-3">
							<PrismicRichText field={content.s3_body} />
							{#if isFilled.link(content.s3_button)}
								<DefaultButton class="w-fit" href={content.s3_button.url}>{content.s3_button.text}</DefaultButton>
							{/if}
						</div>
					</div>
					<PrismicImage field={content.s3_image} class=" mt-24 md:mt-0 aspect-video w-full md:w-2/3 md:pl-6 object-cover"/>
				</div>
				<div class="flex flex-col md:flex-row w-full text-dark">
					<div class="w-full md:w-1/3 relative aspect-[4/3] h-full flex flex-col items-start justify-between pr-8">
						<div>
							<PrismicImage field={content.s4_icon} class="w-14"/>
							<h3 class="mt-3">{content.s4_title}</h3>
						</div>
						<div class="flex flex-col gap-3">
							<PrismicRichText field={content.s4_body} />
							{#if isFilled.link(content.s4_button)}
								<DefaultButton class="w-fit" href={content.s4_button.url}>{content.s4_button.text}</DefaultButton>
							{/if}
						</div>
					</div>
					<PrismicImage field={content.s4_image} class=" mt-24 md:mt-0 aspect-video w-full md:w-2/3 md:pl-6 object-cover"/>
				</div>


			</div>

		</div>

	</ContentWidth>
</section>
