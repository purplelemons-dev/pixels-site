<script lang="ts">
	export let currentColor: string;

	const colorNames = ['black', 'red', 'green', 'blue', 'yellow', 'purple', 'cyan', 'white'];
</script>

<div class="color-selector">
	{#each colorNames as colorName, idx}
		<div
			class="color"
			style={`background-color: ${colorName}`}
			on:click={() => (currentColor = colorName)}
			tabindex="{idx}"
		></div>
	{/each}
</div>
