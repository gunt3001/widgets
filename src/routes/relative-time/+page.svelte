<script lang="ts">
	import { page } from "$app/state";
	import { browser } from "$app/environment";

	const timeParam = getTimeParam();
	const timeSince = calculateTimeSince(timeParam);

	function isInIframe(): boolean {
		try {
			return window.self !== window.top;
		} catch (e) {
			return true;
		}
	}

	function getEmbedCode(): string {
		const url = page.url;

		return `<iframe src="${url.toString()}" allowTransparency="true" title="Relative Time Widget" frameborder="0" marginwidth="0" marginheight="0" scrolling="NO" width="100%" height="80"></iframe>`;
	}

	function setClipboard(text: string): void {
		navigator.clipboard.writeText(text);
	}

	function getTimeParam(): string | null {
		if (!browser) {
			return null;
		}
		const hash = window.location.hash.substring(1); // Remove the leading '#'
		if (hash.length != 7) {
			return null;
		}
		return hash;
	}

	function calculateTimeSince(
		dateString: string | null,
	): { years: number; months: number } | null {
		if (dateString === null) {
			return null;
		}

		const inputDate = new Date(dateString + "-01");
		const currentDate = new Date();

		if (inputDate > currentDate) {
			return null;
		}

		let years = currentDate.getFullYear() - inputDate.getFullYear();
		let months = currentDate.getMonth() - inputDate.getMonth();
		const day = currentDate.getDate() - inputDate.getDate();

		if (day < 0) {
			months--;
		}

		if (months < 0) {
			months += 12;
			years--;
		}

		return { years: years, months: months };
	}
</script>

<div class="w-screen py-2 bg-transparent">
	<div
		class="w-full border rounded-lg p-4 text-black bg-slate-50 dark:bg-slate-900 dark:text-white"
	>
		<b
			>📅
			{#if timeSince === null}
				The time is <a
					class="underline"
					href="https://www.youtube.com/watch?v=svjMiqVeiG8">NOW!</a
				>
			{:else}
				<span>
					{#if timeSince.years > 1}
						{timeSince.years} years
					{:else if timeSince.years == 1}
						A year
					{/if}
				</span>
				<span>
					{#if timeSince.years > 0 && timeSince.months > 1}
						and {timeSince.months} months
					{:else if timeSince.years > 0 && timeSince.months == 1}
						and a month
					{:else if timeSince.months > 1}
						{timeSince.months} months
					{:else if timeSince.months == 1}
						A month
					{/if}
				</span>
				{#if timeSince.years <= 0 && timeSince.months <= 0}
					<span>Less than a month </span>
				{/if}
				ago.
			{/if}
		</b>
	</div>

	{#if !isInIframe()}
		<div
			class="w-full border rounded-lg p-4 text-black dark:bg-slate-900 dark:text-white"
		>
			<div class="flex justify-between items-center mb-2">
				<span class="text-gray-400">Embed code:</span>
				<button
					on:click={(_) => setClipboard(getEmbedCode())}
					class="code bg-gray-800 hover:bg-gray-700 text-gray-300 px-3 py-1 rounded-md"
				>
					Copy
				</button>
			</div>
			<div class="overflow-x-auto">
				<pre class="text-gray-300">
<code>{getEmbedCode()}</code></pre>
			</div>
		</div>
	{/if}
</div>
