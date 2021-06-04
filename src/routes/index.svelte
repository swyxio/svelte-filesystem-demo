<script>

import Comp from '../components/Comp.svelte'
let fileHandle
let contents = null

async function getTheFile() {
    // open file picker
//   [fileHandle] = await window.showOpenFilePicker(pickerOpts);
    [fileHandle] = await window.showOpenFilePicker();
    // get file contents
    const fileData = await fileHandle.getFile();
    contents = await fileData.text()
}

async function writeFile() {
    const writable = await fileHandle.createWritable();
    await writable.write(contents);
    await writable.close();
}
</script>


<h1>Welcome to SvelteKit</h1>

<hr />

<button on:click={getTheFile}>load</button>
<button on:click={writeFile}>save</button>

<Comp bind:contents />
