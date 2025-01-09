<script lang="ts">
	import type { NavItem, SocialLink } from '../lib/types';
	import Icon from '@iconify/svelte';

	let isNavOpen = $state(true);

	const navItems: NavItem[] = [
		{ path: '/', label: 'Home' },
		{ path: '/specialization', label: 'Specialization' },
		{ path: '/resume', label: 'Resume' },
		{ path: '/projects', label: 'Projects' },
		{ path: '/contact', label: 'Contact' }
	];

	const socialLinks: SocialLink[] = [
		{ url: 'https://github.com/ryorichie', alt: 'GitHub', icon: 'entypo-social:github' },
		{
			url: 'https://www.facebook.com/ryo.richie.1',
			alt: 'Facebook',
			icon: 'entypo-social:facebook'
		},
		{
			url: 'https://www.instagram.com/ryo_richiee/',
			alt: 'Instagram',
			icon: 'entypo-social:instagram'
		},
		{
			url: 'https://www.youtube.com/channel/UCc3BiBjA9_6_E95aH5IbKgA',
			alt: 'YouTube',
			icon: 'entypo-social:youtube'
		},
		{
			url: 'https://www.linkedin.com/in/ryorichie/',
			alt: 'LinkedIn',
			icon: 'entypo-social:linkedin'
		}
	];
</script>

<button
	class="absolute right-4 top-4 z-10 p-2 text-gray-500 transition-colors duration-200 hover:text-white"
	onclick={() => (isNavOpen = !isNavOpen)}
>
	{#if isNavOpen}
		<Icon icon="mdi:close" width="32" />
	{:else}
		<Icon icon="mdi:menu" width="32" />
	{/if}
</button>
<nav
	class="fixed right-0 top-0 flex h-screen w-full transform flex-col overflow-hidden text-white transition-all duration-300 sm:w-1/2 md:w-2/5 lg:w-[25%] xl:w-[20%] 2xl:w-[15%] {isNavOpen
		? 'translate-x-0'
		: 'translate-x-full'}"
>
	<div class="flex h-screen w-full flex-grow items-center">
		<ul class="m-0 w-full p-0 text-4xl">
			{#each navItems as { path, label }}
				<li class="group w-full rounded-3xl">
					<a
						href={path}
						class="block w-full p-8 py-8 pr-14 text-right transition-transform duration-200 group-hover:scale-125"
						>{label}</a
					>
				</li>
			{/each}
		</ul>
	</div>
	<div title="logo" class="mt-auto flex justify-around">
		{#each socialLinks as { url, alt, icon }}
			<a href={url} target="_blank">
				<Icon
					{icon}
					width="40"
					class="p-1 text-white transition-transform duration-200 hover:scale-110"
					aria-label={alt}
				/>
			</a>
		{/each}
	</div>
</nav>

<style>
</style>
