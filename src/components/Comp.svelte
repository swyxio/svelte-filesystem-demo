<script>
    export let contents
</script>

{#if contents === null}
<div> please load the file</div>
{:else}
<pre contenteditable="true" bind:textContent={contents}>
</pre>
{/if}

<hr />

<h2>hello Svelte</h2>