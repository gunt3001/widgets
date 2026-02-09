<script lang="ts">
	import "./layout.css";
	import favicon from "$lib/assets/favicon.svg";

	let { children } = $props();

	import { page } from "$app/state";

	let forceLightColorSchemeMode = page.url.searchParams.has("forceLightScheme");
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	{#if forceLightColorSchemeMode}
		<meta name="color-scheme" content="light" />
	{:else}
		<meta name="color-scheme" content="light dark" />
	{/if}
</svelte:head>
{@render children()}
