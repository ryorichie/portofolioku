<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	let myThing = ['Weeb', 'Programmer', 'Gamer', 'ML Engineer', 'PC Builder', 'Leader'];
	let currentThing = $state('');
	let currentIndex = $state(0);
	let charIndex = $state(0);
	let typingInterval: number;
	let isTyping = $state(true);

	// Array to hold our stars
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

	onMount(() => {
		typingInterval = setInterval(type, 100);
		// Create new stars every 150ms
	});

	onDestroy(() => {
		clearInterval(typingInterval);
	});
</script>

<div class="flex h-screen items-center justify-center text-white">
	<div class="text-center">
		<h2 class="text-7xl">I'm Pete Grief</h2>
		<h2 class="text-7xl">As a {currentThing}</h2>
	</div>
</div>
