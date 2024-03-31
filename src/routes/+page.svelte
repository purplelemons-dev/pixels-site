<script lang="ts">
	import ColorSelector from "$lib/components/ColorSelector.svelte"
	let currentColor = "black";
	const cellClicked = (me: MouseEvent) => {
		(me.currentTarget as HTMLTableCellElement).style.backgroundColor = currentColor;
	};
</script>

<table >
	<tbody>
		{#each Array(50) as _, i}
			<tr>
				{#each Array(118) as _, j}
					<td on:click={cellClicked}></td>
				{/each}
			</tr>
		{/each}
	</tbody>
</table>

<ColorSelector bind:currentColor />

<style>
	table {
		border-spacing: 0;
		width: calc(118 * 8px);
		height: calc(50 * 8px);
		table-layout: fixed;
	}
	td {
		width: 8px;
		height: 8px;
		border: 1px solid black;
		background-color: black;
	}
</style>
