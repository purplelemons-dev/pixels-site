<script lang="ts">
	import ColorSelector from '$lib/components/ColorSelector.svelte';
	import { collectionStore, getFirebaseContext } from 'sveltefire';
	import { doc, setDoc, type Firestore } from 'firebase/firestore';
	import type { Pixel } from '$lib';

	let currentColor = 'black';

	const cellClicked = async (me: MouseEvent) => {
		(me.currentTarget as HTMLTableCellElement).style.backgroundColor = currentColor;
		const [x, y] = (me.currentTarget as HTMLTableCellElement).id.split(',').map(Number);
		const pixelDoc = doc(firebase.firestore as Firestore, `pixels`, `${x},${y}`);
		const data = { color: currentColor, position: [x, y] };

		//if ((await getDoc(pixelDoc)).exists()) {
		await setDoc(pixelDoc, data);
		//} else {
		//	const newDoc = await addDoc(collection(firebase.firestore as Firestore, 'pixels'), data);
		//}
	};

	const firebase = getFirebaseContext();
	const pixels = collectionStore<Pixel>(firebase.firestore as Firestore, 'pixels');
	$: for (let pixel of $pixels) {
		const [x, y] = pixel.position;
		const cell = document.getElementById(`${x},${y}`) as HTMLTableCellElement;
		cell.style.backgroundColor = pixel.color;
	}
</script>

<div class="container">
	<table>
		<tbody>
			{#each Array(40) as _, y}
				<tr>
					{#each Array(118) as _, x}
						<td on:click={cellClicked} id="{x},{y}"></td>
					{/each}
				</tr>
			{/each}
		</tbody>
	</table>

	<ColorSelector bind:currentColor />
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 16px;
	}

	table {
		border-collapse: collapse;
		border: 2px solid black;
		background-color: white;
		box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
	}

	td {
		width: 12px;
		height: 12px;
		border: 1px solid #ccc;
		cursor: pointer;
		transition: background-color 0.2s ease;
	}

	td:hover {
		background-color: #f0f0f0;
	}
</style>
