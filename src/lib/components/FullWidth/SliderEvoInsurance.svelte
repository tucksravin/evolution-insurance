<script lang='ts'>


  import { onMount } from "svelte";
  import { swipe } from "svelte-gestures";
  import { fade } from "svelte/transition";

  import type { SwipePointerEventDetail } from "svelte-gestures";
  import { PrismicImage } from "@prismicio/svelte";
  
  let innerWidth:number = $state(1024);

  
 let {
    contentArray,
} = $props();

  const SLIDER_INTERVAL_IN_MS = 5000;


  let sliderIndex = $state(0);
      


  
      const slideRight = () => {
          sliderIndex--;
          clearInterval(sliderInterval);
          sliderInterval = setInterval(()=>slideRight(), SLIDER_INTERVAL_IN_MS);

          


          
          console.log(sliderIndex)
      }
      const slideLeft = () => {
          sliderIndex++;
          clearInterval(sliderInterval);
          sliderInterval = setInterval(()=>slideLeft(), SLIDER_INTERVAL_IN_MS);
          console.log(sliderIndex)

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

  
      onMount(()=>{
         sliderInterval = setInterval(()=>slideLeft(), SLIDER_INTERVAL_IN_MS);
         return ()=>clearInterval(sliderInterval);
      });

</script>

<svelte:window bind:innerWidth />

<div class="hidden">
    {#each contentArray as content}
        <PrismicImage class="h-full w-full object-cover" field={content.image} />
    {/each}
</div>

<div use:swipe onswipe={handleSwipe} class="absolute w-full h-full left-0 top-0 text-primary">
    {#key sliderIndex}
        <div out:fade={{duration:300}} in:fade={{delay:500, duration:300}} class="absolute w-full h-full left-0 top-0">
          
            <PrismicImage class="h-full w-full object-cover" loading="eager" field={contentArray[getPositiveIndex(sliderIndex, contentArray.length)].image}/>
                
            <div class="absolute left-0 -bottom-12 label">
                {contentArray[getPositiveIndex(sliderIndex, contentArray.length)].label}
            </div>
            
        </div>
    {/key}
    <div class="absolute right-0 -bottom-12 w-fit flex flex-row gap-4">
        <button aria-label="prev image" class="pointer-events-auto cursor-pointer" onclick={slideLeft}><i class="text-primary fa-sharp fa-solid fa-chevron-left" ></i></button>
        <button aria-label="next image" class="pointer-events-auto cursor-pointer" onclick={slideRight}><i class="text-primary fa-sharp fa-solid fa-chevron-right" ></i></button>
    
    </div>
</div>


    

