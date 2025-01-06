<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	let myThing = ['Weeb', 'Programmer', 'Gamer', 'ML Engineer', 'PC Builder', 'Leader'];
	let currentThing = $state('');
	let currentIndex = $state(0);
	let charIndex = $state(0);
	let typingInterval: number;
	let starInterval: number;
	let isTyping = $state(true);

	// Array to hold our stars
	let stars = $state<Array<{ id: number; x: number; y: number }>>([]);
	let nextId = $state(0);

	function type() {
		if (isTyping) {
			if (charIndex < myThing[currentIndex].length) {
				currentThing += myThing[currentIndex].charAt(charIndex);
				charIndex++;
			} else {
				isTyping = false;
				setTimeout(() => {
					isTyping = true;
					currentThing = '';
					charIndex = 0;
					currentIndex = (currentIndex + 1) % myThing.length;
				}, 1000);
			}
		}
	}

	function addStar() {
		const star = {
			id: nextId++,
			x: Math.random() * 100,
			y: Math.random() * 100
		};
		stars = [...stars, star];

		setTimeout(() => {
			stars = stars.filter((s) => s.id !== star.id);
		}, 1500);
	}

	onMount(() => {
		typingInterval = setInterval(type, 100);
		// Create new stars every 150ms
		starInterval = setInterval(() => {
			for (let i = 0; i < 6; i++) {
				addStar();
			}
		}, 150);
	});

	onDestroy(() => {
		clearInterval(typingInterval);
		clearInterval(starInterval);
	});
</script>

<div class="flex h-screen items-center justify-center text-white">
	<div
		class="absolute inset-0 -z-20 bg-black bg-gradient-to-t from-[#01112b] to-black"
		id="Background"
	>
		<div class="absolute inset-0 -z-10 overflow-hidden">
			{#each stars as star (star.id)}
				<div class="star absolute" style="left: {star.x}%; top: {star.y}%;"></div>
			{/each}
		</div>
	</div>
	<div class="text-center">
		<h2 class="text-7xl">I'm Pete Grief</h2>
		<h2 class="text-7xl">As a {currentThing}</h2>
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
