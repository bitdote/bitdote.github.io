<script lang="ts">

  import SymbolOverviewWidget from "./SymbolOverviewWidget.svelte";

  let log: boolean = false;

  function toggle() {
    log = !log;
  }
</script>

<button on:click={toggle}>Toggle</button>
<div class="h-full">
    {#if log}
        Log
        <SymbolOverviewWidget scaleMode={'Logarithmic'} />
    {:else}
        Normal
        <SymbolOverviewWidget scaleMode={'Normal'} />
    {/if}
</div>

<style>

</style>