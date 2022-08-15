<script lang="ts">
	import { readText } from '@tauri-apps/api/clipboard';

	let clipboard = '';
	const f = async () => {
		clipboard = await readText();
		await f();
	};
	f();
</script>

<div>
	<pre>{clipboard.trim()}</pre>
</div>

<style>
	div {
		max-height: 25%;
		overflow: scroll;
	}

	pre {
        text-align: left;
		padding: 0.5rem;
		width: 100%;
		min-height: 100%;
		color: grey;
		background: none;
		border: none;
		outline: none;
		border-radius: 8px;
		font-family: 'Anonymous Pro', monospace;
	}
</style>
