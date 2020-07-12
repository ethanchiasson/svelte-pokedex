<script>
  import SearchBar from "../src/searchCom.svelte";
  import PokeCard from "../src/pokeCard.svelte";
  import Modal from "../src/modal.svelte";
  import { onMount } from "svelte";

  let numPoke = 151;
  const pokemonTest = [];
  let list = [];
  let searchQuery;
  let selectedPokemon = {};

  // let pokemon = [];

  // onMount(async () => {
  //   const res = await fetch("./db.json");
  //   pokemon = await res.json();
  //   console.log(pokemon);
  // });

  // function fetchItemIDs() {
  //   fetch("./db.json")
  //     .then(function(resp) {
  //       return resp.json();
  //     })
  //     .then(function(pokes) {
  //       console.log(pokes);
  //       const pokemon = pokes;
  //     });
  // }

  const getPokemon = async id => {
    const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
    const res = await fetch(url);
    const pokemon = await res.json();
    pokemonTest.push(pokemon);
    console.log(pokemonTest);
  };

  const fetchPokes = async () => {
    for (let i = 1; i <= numPoke; i++) {
      await getPokemon(i);
    }
  };

  fetchPokes().then(function() {
    console.log(pokemonTest);
    pokemonTest = pokemonTest;
    list = list;
  });

  $: searchQuery
    ? (list = pokemonTest.filter(({ name }) => {
        return name.toLowerCase().indexOf(searchQuery.toLowerCase()) !== -1;
      }))
    : (list = pokemonTest);
</script>

<style>
  /* .container > div > div {
    border-radius: 0.4em;
    min-width: 200px;
  }
  .container > div > div:hover {
    box-shadow: 3px 3px 12px #474747;
    cursor: pointer;
  } */

  #input {
    box-shadow: 3px 3px 12px #474747;
    cursor: pointer;
  }

  input:focus {
    outline: 0px !important;
    -webkit-appearance: none;
    box-shadow: none !important;
  }
</style>

<main>
  <div class="container text-dark">
    <div class="d-flex flex-wrap justify-content-center">
      <div class="input-group mb-3" id="input">
        <div class="input-group-prepend">
          <span class="input-group-text" id="basic-addon1">
            <img src="pokeball.png" alt="" width="20" />
          </span>
        </div>
        <input
          type="text"
          class="form-control"
          placeholder="Search Pokemon, type, abilities, etc.."
          aria-label="pokemon"
          aria-describedby=""
          bind:value={searchQuery} />
      </div>
      {#each list as poke}
        <PokeCard {poke} on:click={() => (selectedPokemon = poke)} />
      {/each}
      <Modal poke={selectedPokemon} />
    </div>
  </div>
</main>
