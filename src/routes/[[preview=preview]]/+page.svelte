<script lang='ts'>

	let { data } = $props();

	let viewpoortWidth=$state(1024)

	let content = data.page.data;
</script>


<svelte:window bind:innerWidth={viewpoortWidth} />

<div class="h-screen w-screen bg-white"></div>
{#if viewpoortWidth>768}

{:else}
{/if}