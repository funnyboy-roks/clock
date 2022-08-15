<script lang="ts">
	import Header from './Header.svelte';
	import Todo from './Todo.svelte';
	import Notes from './Notes.svelte';
	import WorldClock from './WorldClock.svelte';

	let selectedTab = 'todo';
</script>

<main>
	<Header bind:selectedTab />

	{#if selectedTab === 'todo'}
		<Todo />
	{:else if selectedTab === 'notes'}
		<Notes />
	{:else if selectedTab === 'clocks'}
		<WorldClock />
	{:else}
		<div>No Tab Selected</div>
	{/if}

</main>

<style>
	main {
		height: 100%;
		text-align: center;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}
</style>
