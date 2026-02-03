<script lang="ts">
	import { onMount } from 'svelte';

	let weekNumber = $state<number | null>(null);
	let season = $state('');
	let year = $state(0);

	function calculateSeasonWeek() {
		const today = new Date();
		const month = today.getMonth();
		year = today.getFullYear();

		// Calculate the starting month for current season (0-January, 3-April, 6-July, or 9-October)
		const seasonStartMonth = Math.floor(month / 3) * 3;

		// Create Date object of the first day of the season
		const seasonStartDate = new Date(year, seasonStartMonth, 1, 0, 0, 0);

		// If the first day of the season is not Sunday (0), adjust to the next Sunday
		if (seasonStartDate.getDay() !== 0) {
			const daysUntilSunday = 7 - seasonStartDate.getDay();
			seasonStartDate.setDate(seasonStartDate.getDate() + daysUntilSunday);
		}

		// Calculate how many weeks since the first Sunday of the season
		weekNumber = Math.floor((today.getTime() - seasonStartDate.getTime()) / (1000 * 60 * 60 * 24 * 7)) + 1;

		// Determine season name
		if (month < 3) {
			season = 'Winter';
		} else if (month < 6) {
			season = 'Spring';
		} else if (month < 9) {
			season = 'Summer';
		} else {
			season = 'Fall';
		}
	}

	onMount(() => {
		calculateSeasonWeek();
	});
</script>

<div class="w-full text-center bg-transparent rounded-lg p-3 my-3 text-black dark:text-white">
	<h1 class="text-4xl font-semibold">
		It is Week <span class="text-white bg-red-900 inline-block rounded-lg p-1">{weekNumber ?? '?'}</span> of <span class="text-white bg-red-900 inline-block rounded-lg p-1">{season ? `${season} ${year}` : '?'}</span>
	</h1>
</div>
