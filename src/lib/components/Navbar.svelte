<script lang="ts">
	import { navigating } from '$app/stores';
	import { ProgressBar } from '@skeletonlabs/skeleton';
	import { writable } from 'svelte/store';
	import { page } from '$app/stores';
	import SearchBar from './SearchBar.svelte';

	const y = writable(0);

	$: isHome = $page.route.id === '/' ? true : false;
	$: isNavbarShow = $y < 220 ? true : false;

</script>

<svelte:window bind:scrollY={$y} />

<nav
	class={$y === 0
		? `nav-top transition-all ease-in-out duration-500`
		: `nav-class transition-all ease-in-out duration-300`}
>
	{#if $navigating}
		<ProgressBar rounded={'rounded-none'} height={'h-[3px]'} />
	{/if}
	<div class="flex items-center justify-between w-full px-8 py-3">
		<a href="/">
			<img class="h-8 w-8" src="favicon.svg" alt="" />
		</a>
		<div class="flex gap-4 items-center">
			<SearchBar />
		</div>
	</div>
</nav>

<style>
	.nav-class {
		@apply fixed  bg-surface-800 w-screen z-20;
	}
	.nav-top {
		@apply fixed  bg-transparent w-screen z-20;
	}
</style>
