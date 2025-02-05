
<script lang="ts">
    import linkArrow from "$lib/assets/icons/arrow.svg"
    export let text = "";
    export let href ="#"


    let isLinkArrowActive=false;

</script>
<style>
    div{
font-size: 48px;
font-style: normal;
font-weight: 400;
line-height: 1em; 
    }
    @media only screen and (max-width:1340px) {
        div{
            font-size: 36px;
        }
    }

    @media only screen and (max-width:1024px) {
        div{
            font-size: 28px;
        }
    }

    @media only screen and (max-width:768px) {
        div{
            font-size: 16px;
        }
    }
</style>


<a 
onmouseenter={()=>isLinkArrowActive=true} 
onmouseleave={()=>isLinkArrowActive=false}
onclick= {()=>isLinkArrowActive=false}
class="flex flex-row items-center opacity-90 hover:opacity-100 no-underline justify-start transition-all duration-300 h-4 md:h-7 lg:h-9 xl:h-14 active:-translate-y-2 relative {$$props.class || ''}" 
{href}>
    <div>{text}</div>
    <img src={linkArrow} alt="link arrow" class=" ml-[10px]  duration-300 h-1/2 -translate-y-[8%] {isLinkArrowActive ? "":"opacity-0"}">
</a>