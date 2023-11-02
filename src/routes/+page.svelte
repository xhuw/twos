
<script lang="ts">
import { tick } from 'svelte';
import { fade, fly } from 'svelte/transition';

let text_input;
let show_res = false;
let res = 0

function bin_to_num(b) {
    if(!b.length) {
        return 0;
    }
    let accum = -1 * (Math.pow(2, (b.length - 1))) * parseInt(b[0]);
    for(let i = 1; i < b.length; i++) {
        accum += Math.pow(2, b.length - (i + 1)) * parseInt(b[i]);
    }
    return accum;
}

async function update_res() {
    show_res = false;
    await tick();
    res = bin_to_num(text_input);
    show_res = true;
}

</script>


<h1>Converting twos complement for people in need</h1>
<input bind:value={text_input} placeholder="101011"/>
<button on:click={update_res}>Convert</button>
{#if show_res}
<p in:fly={{ y: 200, duration: 2000 }} out:fade>{res}</p>
{/if}
