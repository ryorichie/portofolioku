<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import Branchtitle from '../../components/branchtitle.svelte';
	import Background from '../../components/background.svelte';

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

<div class="flex h-screen text-white">
	<Background />
	<div class="h-full w-full flex-row">
		<Branchtitle title="Specialization" />
		<div class="flex-col">
			<div class="flex-row">
				<div class="flex-col">
					<h1 class="text-[50px]">Machine Learning</h1>
					<p class="text-[20px]">
						I have experience in developing machine learning models for various applications such as
						image classification, object detection, and natural language processing.
					</p>
				</div>
			</div>
		</div>
	</div>
</div>
