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
    max-width: 1000px;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  @media screen and (min-width: 700px) {
    main {
      display: grid;
      grid-template-columns: 1fr 1fr;
    }
  }

  @media screen and (min-width: 1000px) {
    main {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
</style>
