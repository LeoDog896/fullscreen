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
<div class="fixed top-0 left-0 w-2/5 h-2/5" on:mouseenter={() => { visible = true }} ></div>
{#if visible}
  <div transition:fly={{y: -150, x: -150}} class="text-white fixed top-0 left-0 m-8 bg-gray-500/75 rounded-lg z-10 text-center">
    <input bind:this={fileInput} transition:fly={{y: -150, x: -150}} type="file" class="hidden" bind:files={files}>
    <button class="px-4 py-2 bg-gray-800 rounded-lg ring ring-gray-700 m-4" on:click={() => fileInput.click()}>Choose file</button>
  </div>
{/if}