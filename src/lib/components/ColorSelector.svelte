<script lang="ts">
	export let currentColor: string;

	const colorNames = ['black', 'red', 'green', 'blue', 'yellow', 'purple', 'cyan', 'white'];
</script>

<div class="color-selector">
	{#each colorNames as colorName, idx}
		<div
			class="color"
			style={`background-color: ${colorName}`}
			role="button"
			aria-label={colorName}
			on:click={() => (currentColor = colorName)}
			on:keydown={(e) => {
				if (e.key === 'Enter' || e.key === ' ') currentColor = colorName;
			}}
			tabindex={idx}
		></div>
	{/each}
</div>

<style>
	.color-selector {
		display: flex;
		gap: 8px;
		padding: 8px;
		background-color: white;
		border-radius: 4px;
		box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
	}

	.color {
		width: 24px;
		height: 24px;
		border-radius: 50%;
		border: 2px solid #ccc;
		cursor: pointer;
		transition: transform 0.2s ease;
	}

	.color:hover {
		transform: scale(1.1);
	}

	.color:focus {
		outline: none;
		box-shadow: 0 0 0 2px #333;
	}
</style>
