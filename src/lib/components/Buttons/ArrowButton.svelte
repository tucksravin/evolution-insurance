
<script lang="ts">
    import linkArrow from "$lib/assets/icons/arrow.svg"
    export let text = "";
    export let href ="#"


    let isLinkArrowActive=false;

</script>
<style>
    div{
font-size: 36px;
font-style: normal;
font-weight: 400;
line-height: 36px; /* 312.5% */
    }
</style>


<a 
onmouseenter={()=>isLinkArrowActive=true} 
onmouseleave={()=>isLinkArrowActive=false}
onclick= {()=>isLinkArrowActive=false}
class="flex flex-row items-center opacity-90 hover:opacity-100 no-underline justify-start transition-all duration-300 active:-translate-y-2 h-9 {$$props.class || ''}" 
{href}>
    <div>{text}</div>
    <img src={linkArrow} alt="link arrow" class=" ml-[10px]  duration-300 h-1/2 {isLinkArrowActive ? "":"opacity-0"}">
</a>