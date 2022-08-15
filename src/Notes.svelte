<script lang="ts">
    import { BaseDirectory, writeTextFile, readTextFile } from "@tauri-apps/api/fs";

    let value = '';
    let saveTimer: NodeJS.Timeout;

    readTextFile('notes.txt', { dir: BaseDirectory.App }).then((t) => value = t);

    const save = () => {
        clearTimeout(saveTimer);
        saveTimer = setTimeout(() => writeTextFile('notes.txt', value, { dir: BaseDirectory.App }), 300);
    }
</script>

<div>
	<textarea on:input={save} bind:value></textarea>
</div>

<style>

    div {
        height: 75%;
    }

    textarea {
        font-family: 'Anonymous Pro', monospace;
        color: lightgrey;
        border: 1px solid grey;
        height: 100%;
        width: 100%;
        background: #0006;
    }

</style>
