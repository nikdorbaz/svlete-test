<script>
	import Block from "./Block.svelte";
	
	let blocks = [{
		id: 1,
		text: "Some text",
		keyboards: [
			{
				id: 1,
				text: "First button"
			},
			{
				id: 2,
				text: "Second button"
			}
		],
		position: {
			left: 0,
			top: 0
		}
	}];

	$: console.table(blocks);

</script>

<main>
	{#each blocks as block, index}
		<Block bind:block={block} bind:blocks={blocks} {index} />
	{/each}
</main>

<style>
	main {
		width: calc(100vw - 20px);
		height: calc(100vh - 20px);
		background: radial-gradient(rgba(195, 199, 203, 0.412) 25%,transparent 25%);
		background-size: 13.33333333px 13.33333333px;
    	background-color: #fafafd;
		background-position: center;
		position: relative;
	}
</style>
