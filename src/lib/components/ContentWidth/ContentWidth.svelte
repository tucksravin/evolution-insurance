<!-- @migration-task Error while migrating Svelte code: $$props is used together with named props in a way that cannot be automatically migrated. -->
<!-- @migration-task Error while migrating Svelte code: $$props is used together with named props in a way that cannot be automatically migrated. -->
<script lang='ts'>
    import AnimateIn from "../Animation/AnimateIn.svelte";

    export let animateIn = false;
</script>

{#if animateIn}
<AnimateIn><div class="max-w-[1220px] xl:max-w-[1440px] xl:mx-auto mx-[4%] w-[92%] {$$props.class || 'flex flex-col items-center justify-center relative'}"><slot /></div></AnimateIn>
{:else}
<div class="max-w-[1220px] xl:max-w-[1440px] xl:mx-auto mx-[4%] w-[92%] {$$props.class || 'flex flex-col items-center justify-center relative'}"><slot /></div>
{/if}