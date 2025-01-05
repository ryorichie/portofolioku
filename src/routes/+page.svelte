<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	let myThing = ['Weeb', 'Programmer', 'Gamer', 'ML Engineer', 'PC Builder', 'Leader'];
	let currentThing = $state('');
	let currentIndex = $state(0);
	let charIndex = $state(0);
	let interval: number;
	let isTyping = $state(true);

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
				}, 1000); // Pause before starting the next word
			}
		}
	}

	onMount(() => {
		interval = setInterval(type, 100);
	});

	onDestroy(() => {
		clearInterval(interval);
	});
</script>

<div class="flex h-screen items-center justify-center text-white">
	<div class="absolute inset-0 -z-10 bg-black bg-gradient-to-t from-[#01112b] to-black"></div>
	<div class="text-center">
		<h2 class="text-7xl">I'm Ryo Richie</h2>
		<h2 class="text-7xl">As a {currentThing}</h2>
	</div>
</div>
