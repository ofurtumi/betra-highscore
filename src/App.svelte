<script lang="ts">
  import Stats from "./lib/Stats.svelte";
</script>

<main>
  {#each { length: 10 } as _, i}
    <Stats game_num={i} />
  {/each}
</main>

<style>
  body {
    background-color: #222;
    color: #eee;
    font-family: sans-serif;
    padding: 1rem;
  }

  main {
    width: 90vw;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1rem;
  }
</style>
