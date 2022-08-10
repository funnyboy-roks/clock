<script lang="ts">
	import { onMount } from 'svelte';
	import { derived, writable } from 'svelte/store';

	let date = writable(new Date());
	let seconds = true;

	onMount(() => setInterval(() => date.set(new Date()), 500));

	const toggleSeconds = () => {
		seconds = !seconds;
		date.set(new Date());
	};

	let text = derived([date], ([date]) => ({
		time: seconds
			? date.toLocaleTimeString('en-gb')
			: date.toLocaleTimeString('en-gb', {
					hour: '2-digit',
					minute: '2-digit',
			  }),
		date: date.toLocaleDateString('en-gb', {
			year: 'numeric',
			month: 'long',
			day: 'numeric',
		}),
	}));
</script>

<div>
	<h1 on:click={toggleSeconds}>{$text.time}</h1>
	<h2>{$text.date}</h2>
</div>

<style>
</style>
