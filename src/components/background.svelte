<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	let starInterval: number;

	// Array to hold our stars
	let stars = $state<Array<{ id: number; x: number; y: number }>>([]);
	let nextId = $state(0);

	function addStar() {
		const star = {
			id: nextId++,
			x: Math.random() * 100,
			y: Math.pow(Math.random(), 3) * 100
		};
		stars = [...stars, star];

		setTimeout(() => {
			stars = stars.filter((s) => s.id !== star.id);
		}, 1500);
	}

	onMount(() => {
		// Create new stars every 150ms
		starInterval = setInterval(() => {
			for (let i = 0; i < 6; i++) {
				addStar();
			}
		}, 150);
	});

	onDestroy(() => {
		clearInterval(starInterval);
	});
</script>

<div
	class="absolute inset-0 -z-20 bg-black bg-gradient-to-t from-[#08060e] to-black"
	id="Background"
>
	<div class="absolute inset-0 -z-10 overflow-hidden">
		{#each stars as star (star.id)}
			<div class="star absolute" style="left: {star.x}%; top: {star.y}%;"></div>
		{/each}
	</div>
</div>

<style>
	.star {
		position: absolute;
		width: 2px;
		height: 2px;
		background: white;
		border-radius: 50%;
		animation: starAnimation 1.5s ease-out forwards;
		pointer-events: none;
	}

	@keyframes starAnimation {
		0% {
			opacity: 0;
			transform: scale(0);
		}
		50% {
			opacity: 1;
			transform: scale(1);
		}
		100% {
			opacity: 0;
			transform: scale(0);
		}
	}

	/* Varying star sizes */
	.star:nth-child(3n) {
		width: 3px;
		height: 3px;
		box-shadow: 0 0 3px rgba(255, 255, 255, 0.5);
	}

	.star:nth-child(5n) {
		width: 1px;
		height: 1px;
	}

	.star:nth-child(7n) {
		width: 4px;
		height: 4px;
		box-shadow: 0 0 4px rgba(255, 255, 255, 0.7);
	}
</style>
