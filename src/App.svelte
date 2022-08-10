<script lang="ts">
	import Clock from './Clock.svelte';
	import Todo from './Todo.svelte';
</script>

<main>
	<Clock />

	<Todo />
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
