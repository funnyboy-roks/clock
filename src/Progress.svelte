<script lang="ts">
    import type { Writable } from "svelte/store";
    import { tweened } from 'svelte/motion';
    import { onDestroy } from "svelte";
    import { cubicOut } from 'svelte/easing';
    
    export let date: Writable<Date>;

    const seconds = tweened(0, { easing: cubicOut, });
    const minutes = tweened(0, { easing: cubicOut, });
    const hours = tweened(0, { easing: cubicOut, });
    const day = tweened(0, { easing: cubicOut, });
    const month = tweened(0, { easing: cubicOut, });

    onDestroy(date.subscribe((d) => {
        seconds.set(d.getSeconds());
        minutes.set(d.getMinutes());
        hours.set(d.getHours());
        day.set(d.getDate());
        month.set(d.getMonth());
    }));

</script>

<div>

<progress min="0" max="60" value={$seconds} />
<progress min="0" max="60" value={$minutes} />
<progress min="0" max="24" value={$hours} />
<progress min="0" max="32" value={$day} />
<progress min="0" max="12" value={$month} />

</div>

<style>

    div {
        display: flex;
        flex-direction: column;
        width: 100%;
    }

    progress::-webkit-progress-value {
        background-color: var(--accent);
    }

    progress {
        background-color: var(--accent);
        border-radius: 5rem;
        width: 80%;
        margin: .5rem auto;
    }

</style>