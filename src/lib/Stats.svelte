<script lang="ts">
  export let game_num: Number;
  const url = new URL(`https://greining-highscore.onrender.com/${game_num}`);
  // const url = new URL(`http://localhost:3000/${game_num}`);

  const fetch_data = (async () => {
    const response = await fetch(url);
    return await response.json();
  })();

  let baseline = 0;

  const is_baseline = (player: string) => {
    if (player.includes("Random")) {
      baseline++;
      console.log(baseline);
      return true;
    }
  };

  function getBaseline() {
    let temp = baseline;
    return temp;
  }
</script>

<section class="game">
  {#await fetch_data}
    <h1>Sæki gögn fyrir leik {game_num}</h1>
  {:then data}
    <h1>Leikur {game_num}</h1>
    <ul>
      {#each data as player}
        {#if is_baseline(player)}
          <li class="baseline">{player}</li>
        {:else}
          <li>{player}</li>
        {/if}
      {/each}
    </ul>
  {:catch}
    <h1>Eitthvað fór úrskeiðis</h1>
    {#await fetch_data}
      <p>Reyni aftur...</p>
    {:then again}
      <h1>Leikur {game_num}</h1>
      <ul>
        {#each again as player}
          {#if is_baseline(player)}
            <li class="baseline">{player}</li>
          {:else}
            <li>{player}</li>
          {/if}
        {/each}
      </ul>
    {:catch}
      <h1>Tókst ekki að sækja gögn 😄</h1>
    {/await}
  {/await}
</section>

<style>
  section {
    padding: 1rem;
    background-color: gray;
    color: #222;
    border-radius: 10px;
  }

  h1 {
    font-size: 1.5rem;
  }

  ul {
    padding-inline-start: 0;
    list-style: none;
    display: flex;
    align-items: center;
    flex-direction: column;
  }

  li {
    flex-grow: 0;
    width: 100%;
    display: flex;
    justify-content: space-between;
  }

  li:not(.baseline) {
    background-color: gray;
  }

  li:not(.baseline)::after,
  li:not(.baseline)::before {
    content: " ✅ ";
    text-shadow: black 1px 1px 1px;
  }

  li:nth-child(1),
  li:nth-child(2),
  li:nth-child(3) {
    text-shadow: black 1px 1px 1px;
  }

  li:nth-child(1) {
    color: gold;
  }

  li:nth-child(1)::before,
  li:nth-child(1)::after {
    content: " 🥇 ";
  }

  li:nth-child(2) {
    color: silver;
  }

  li:nth-child(2)::before,
  li:nth-child(2)::after {
    content: " 🥈 ";
  }

  li:nth-child(3) {
    color: #cd7f32;
  }

  li:nth-child(3)::before,
  li:nth-child(3)::after {
    content: " 🥉 ";
  }

  .baseline {
    margin: 0.1rem 0;
    border: 2px solid black;
    border-radius: 20px;
    background-color: maroon;
    font-weight: bold;
    width: 100%;
    text-align: center;
    justify-content: center;
  }

  .baseline ~ li:not(.baseline)::before,
  .baseline ~ li:not(.baseline)::after {
    content: " ⚠️ ";
  }

  .baseline ~ .baseline ~ li::before,
  .baseline ~ .baseline ~ li::after {
    content: " 🚫 ";
  }
</style>
