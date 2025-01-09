<script lang="ts">
	import '../app.css';
	import Rightsidebar from '../../components/rightsidebar.svelte';
	import Background from '../../components/background.svelte';
	let { children } = $props();
</script>

<div class="layout">
	<main>
		{@render children()}
		<Background />
		<Rightsidebar />
	</main>
</div>
