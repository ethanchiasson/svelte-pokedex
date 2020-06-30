<script>
  export let name;
  import SearchBar from "../src/searchCom.svelte";
  import Pokemon from "../src/pokemonCom.svelte";
</script>

<style>
  main {
    text-align: center;
    padding: 0.5em;
    margin: 0 auto;
    background: linear-gradient(to left, white 50%, red 50%);
  }

  h1 {
    /* color: #ff000d; */
    color: white;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: bold;
    -webkit-text-stroke: 2px black;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<svelte:head>
  <style>
    body {
      background-color: red;
    }
  </style>
</svelte:head>
<main>
  <h1>Pokedex</h1>
  <!-- <SearchBar /> -->
  <Pokemon />
</main>
