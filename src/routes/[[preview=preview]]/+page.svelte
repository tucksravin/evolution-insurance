<script lang='ts'>
  import DefaultButton from "$lib/components/Buttons/DefaultButton.svelte";
  import ContentWidth from "$lib/components/ContentWidth/ContentWidth.svelte";
  import SliderEvoInsurance from "$lib/components/FullWidth/SliderEvoInsurance.svelte";
  import ScreenWidthImage from "$lib/components/ScreenWidth/ScreenWidthImage.svelte";
  import { isFilled } from "@prismicio/client";
  import { PrismicImage, PrismicRichText } from "@prismicio/svelte";
  import { onMount } from "svelte";
  import { swipe } from "svelte-gestures";
  import { fade } from "svelte/transition";

  import type { SwipePointerEventDetail } from "svelte-gestures";



	let { data } = $props();

	let viewpoortWidth=$state(1024)

	let content = data.page.data;


	const SLIDER_INTERVAL_IN_MS = 5000;


let sliderIndex = $state(0);
	



	const slideRight = () => {
		sliderIndex--;
		clearInterval(sliderInterval);
		sliderInterval = setInterval(()=>slideRight(), SLIDER_INTERVAL_IN_MS);

		


  
	}
	const slideLeft = () => {
		sliderIndex++;
		clearInterval(sliderInterval);
		sliderInterval = setInterval(()=>slideLeft(), SLIDER_INTERVAL_IN_MS);
	 

	}

	const getPositiveIndex = (index: number, length: number): number => {
  return ((index % length) + length) % length;
};




	let sliderInterval:NodeJS.Timeout;

	const handleSwipe = (e:CustomEvent<SwipePointerEventDetail>) => {
	  if(e.detail.direction==="left") 
		slideLeft();

		if(e.detail.direction==="right") 
		slideRight();
	}
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
			<h4 class="md:w-1/4 md:pr-4 xl:pr-16">{content.s1_eyebrow}</h4>
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
			<h4 class="md:w-1/4 md:pr-4 xl:pr-16">{content.s2_eyebrow}</h4>
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

<ScreenWidthImage field={content.s5_background_image} class="flex items-center justify-end">
	<div class="bg-white aspect-[4/3] w-full lg:w-1/2 p-10 flex flex-col justify-between" use:swipe onswipe={handleSwipe}>
		<div class="w-full h-14 flex flex-row justify-between items-center">
			<h4 class="text-primary xl:pr-16">{content.s5_eyebrow}</h4>
			<div class="relative h-20 w-20">
			{#key sliderIndex}
			<div out:fade in:fade={{delay:500}} class="absolute w-full h-full left-0 top-0">
				<PrismicImage class="" field={content.s5_slider[getPositiveIndex(sliderIndex, content.s5_slider.length)].icon} />
			</div>
			{/key}
			</div>
		</div>
		<div class="flex flex-col text-dark gap-8">
			<div class="h-2/3 relative">
			{#key sliderIndex}
				<h3 out:fade in:fade={{delay:500}} class="w-4/5 absolute bottom-0 left-0">{content.s5_slider[getPositiveIndex(sliderIndex, content.s5_slider.length)].testimonial}</h3>
			{/key}
			</div>
			<div class="flex flex-row justify-between h-14 items-center">
				<div class="relative w-1/2 h-full">
					{#key sliderIndex}
						<h5 out:fade in:fade={{delay:500}} class="text-primary absolute left-0 top-1/2 -translate-y-1/2">{content.s5_slider[getPositiveIndex(sliderIndex, content.s5_slider.length)].attribution}</h5>
					{/key}
				</div>
				<div class="flex flex-row gap-4">
					<button aria-label="prev image" class="pointer-events-auto cursor-pointer" onclick={slideLeft}><i class="text-primary fa-sharp fa-solid fa-chevron-left" ></i></button>
					<button aria-label="next image" class="pointer-events-auto cursor-pointer" onclick={slideRight}><i class="text-primary fa-sharp fa-solid fa-chevron-right" ></i></button>
				
				</div>
			</div>
		</div>

	</div>
</ScreenWidthImage>

<section class="py-24 text-dark">
	<ContentWidth class="relative flex flex-col gap-20 md:gap-40">
		<div class="hidden lg:block absolute h-full w-[13px] bg-primary left-0 -translate-x-[400%]"></div>
		<div class="flex flex-col md:flex-row">
			<h4 class="md:w-1/4 md:pr-4 xl:pr-16">{content.s6_eyebrow}</h4>
			<div class="flex flex-col gap-3 md:w-1/4 md:pr-4">
				<PrismicRichText field={content.s6_body} />
				{#if isFilled.link(content.s6_button)}
					<DefaultButton class="w-fit" href={content.s6_button.url}>{content.s6_button.text}</DefaultButton>
				{/if}
			</div>

			<div class="md:w-1/2 flex flex-col gap-20 md:gap-40">
				<div class="w-full flex flex-row justify-center flex-wrap text-primary">
					{#each content.partners as partner}
						<div class="w-1/2 lg:w-1/3 pr-4 pb-4 aspect-square flex flex-col items-center justify-center gap-12">
							<PrismicImage field={partner.logo} class="w-2/3" />
							
						</div>
					{/each}
				</div>
			</div>
		</div>
		<div class="flex flex-col md:flex-row w-full text-dark">
			<h4 class="md:w-1/4 md:pr-4 xl:pr-16">{content.s7_eyebrow}</h4>
			<div class="flex flex-col gap-3 md:w-3/4 md:pr-4">
				<div class="w-1/3 flex flex-col gap-3">
					<PrismicRichText field={content.s7_body} />
					{#if isFilled.link(content.s7_button)}
						<DefaultButton class="w-fit" href={content.s7_button.url}>{content.s7_button.text}</DefaultButton>
					{/if}
				</div>
				<div class="w-full flex flex-col md:flex-row mt-8">
					{#each content.s7_cities as city}
					<div class="w-full md:w-1/3 md:pr-8 flex flex-col gap-3">
						<PrismicImage class="w-full aspect-[3/4]" field={city.image} />
						<span class="label text-primary">{city.label}</span>
					</div>
					{/each}

				</div>
			</div>
		</div>
		
		<div class="w-full aspect-video relative text-white">
			<PrismicImage class="absolute w-full h-full left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 object-cover -z-10" field={content.s8_background}/>
			<div class="w-full h-full p-20 flex flex-col items-start justify-end gap-12">
				<h2 class="w-1/2">{content.s8_title}</h2>
				{#if isFilled.link(content.s8_button)}
						<DefaultButton class="w-fit" href={content.s8_button.url}>{content.s8_button.text}</DefaultButton>
				{/if}
			</div>
		</div>
				
	</ContentWidth>
</section>