<script lang="ts">
	import '../app.css';
	import Rightsidebar from '../lib/rightsidebar.svelte';
	let { children } = $props();
</script>

<div class="layout">
	<main>
		{@render children()}
		<Rightsidebar />
	</main>
</div>
