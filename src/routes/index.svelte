<script lang="ts">

  import { fly } from "svelte/transition"

  let files: FileList = [];
  let fileInput: HTMLInputElement

  let visible = true;

  $: fileBlob = files.length === 1 ? window.URL.createObjectURL(files[0]) : null
</script>
<div 
  on:mouseenter|self={() => { visible = false }}
  style="{fileBlob ? `background-image: url('${fileBlob}')` : ""};" 
  class="w-screen h-screen bg-cover bg-no-repeat bg-center"
/>
<div class="fixed top-0 left-0 w-1/5 h-1/5" on:mouseenter={() => { visible = true }} ></div>
<input bind:this={fileInput} type="file" class="hidden" bind:files={files}>
{#if visible || files.length === 0}
  <button transition:fly={{y: -150, duration: 500}} class="fixed top-0 left-0 text-white px-4 py-2 bg-gray-800 rounded-lg ring ring-gray-700 m-4" on:click={() => fileInput.click()}>Choose file</button>
  {#if files.length === 0}
    <p class="text-black fixed top-1/2 left-1/2 translate-x-[-50%] translate-y-[-50%]">No file chosen. Choose one at the top left.</p>
  {/if}
{/if}