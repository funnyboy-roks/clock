<script lang="ts">
	import { onMount } from 'svelte';
	import { derived, writable } from 'svelte/store';
	import { faCircleCheck, faNoteSticky, faClock } from '@fortawesome/free-solid-svg-icons';
	import { FontAwesomeIcon } from 'fontawesome-svelte';

	export let selectedTab;

	let date = writable(new Date());

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
	<h1>{$text.time}</h1>
	<h2>{$text.date}</h2>

	<div id="tabs">
		{#each tabs as tab, i (i)}
			<button on:click|preventDefault={() => (selectedTab = tab.value)} class:selected={selectedTab === tab.value}>
				<!-- {tab.name} -->
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
