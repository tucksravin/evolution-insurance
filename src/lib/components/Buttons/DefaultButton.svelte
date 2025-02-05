
<script lang="ts">
    export let click = ()=>{};
    export let href="";
</script>

<style>
    button, a{
        border-bottom: 3px solid #554F45;
        font-size: 12px;
        font-style: normal;
        font-weight: 600;
        line-height: 24px; /* 200% */
        letter-spacing: 1px;
        text-transform: uppercase;

    }
    @media only screen and (max-width:1340px) {
        button, a{
            
        }
    }


</style>

{#if href}
    <a {href} on:click={click} 
            class="opacity-90 hover:opacity-100 hover:border-white transition active:-translate-y-[2px]  {$$props.class || ''}">
            <slot />
    </a>
{:else}
    <button on:click={click} 
            class="opacity-90 hover:opacity-100 hover:border-white transition active:-translate-y-[2px] {$$props.class || ''}">
            <slot />
    </button>
{/if}