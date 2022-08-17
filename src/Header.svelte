<script lang="ts">
	import { onMount } from 'svelte';
	import { derived, writable } from 'svelte/store';
	import { faCircleCheck, faNoteSticky, faClock } from '@fortawesome/free-solid-svg-icons';
	import { FontAwesomeIcon } from 'fontawesome-svelte';

	import Progress from './Progress.svelte';

	export let selectedTab: string;

	let date = writable(new Date());
	let progressbars = false;

	onMount(() => setInterval(() => date.set(new Date()), 500));

	let text = derived([date], ([date]) => ({
		time: date.toLocaleTimeString('en-gb'),
		date: date.toLocaleDateString('en-gb', {
			year: 'numeric',
			month: 'long',
			day: 'numeric',
		}),
	}));

	const tabs = [
		{
			name: 'Todo',
			value: 'todo',
			icon: faCircleCheck,
		},
		{
			name: 'Notes',
			value: 'notes',
			icon: faNoteSticky,
		},
		{
			name: 'Clocks',
			value: 'clocks',
			icon: faClock,
		},
	];
</script>

<div>
	<div on:click={() => (progressbars = !progressbars)}>
		{#if progressbars}
			<Progress {date} />
		{:else}
			<h1>{$text.time}</h1>
			<h2>{$text.date}</h2>
		{/if}
	</div>

	<div id="tabs">
		{#each tabs as tab, i (i)}
			<button on:click|preventDefault={() => (selectedTab = tab.value)} class:selected={selectedTab === tab.value} title={tab.name}>
				<FontAwesomeIcon icon={tab.icon} />
			</button>
		{/each}
	</div>
</div>

<style>
	#tabs button.selected {
		/* color: var(--accent); */
		color: #ff784b;
	}

	#tabs button {
		background: none;
		outline: none;
		border: none;
		color: white;
		cursor: pointer;
		font-size: 1.3rem;
	}
</style>
