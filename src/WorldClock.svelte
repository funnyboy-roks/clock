<script lang="ts">
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';
	import { findTimeZone, getZonedTime, listTimeZones } from 'timezone-support';

	const timezones = ['UTC', 'America/New_York', 'America/Los_Angeles', 'America/Chicago'];
	const formatTime = (time) => time.hours.toString().padStart(2, '0') + ':' + time.minutes.toString().padStart(2, '0');

	let date = writable(new Date());
	onMount(() => setInterval(() => date.set(new Date()), 1000));
</script>

<main>
	{#each timezones as tz, i (i)}
		<div id="timezone">
			{tz.replace(/_/gi, ' ')} <span class="monospace">{formatTime(getZonedTime($date, findTimeZone(tz)))}</span>
		</div>
	{/each}
</main>

<style>
	.monospace {
		font-family: 'Anonymous Pro', monospace;
	}

	#timezone {
		color: var(--accent);
		font-size: 1.5rem;
		line-height: 3rem;
		width: 80%;
		margin: auto;
		display: flex;
		justify-content: space-between;
	}

	main {
		padding-bottom: 5rem;
	}
</style>
