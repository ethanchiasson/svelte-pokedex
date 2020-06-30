<script>
  import SearchBar from "../src/searchCom.svelte";

  let word = "ditto";
  let numPoke = 50;
  const pokemonTest = [];
  let list = [];
  let searchQuery;

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
  .container > div > div {
    background-color: #212121;
    border-radius: 0.4em;
    min-width: 200px;
  }

  main {
    /* background-color: cadetblue; */
  }

  #abil {
    border-radius: 0.5em;
    background-color: rgb(8, 63, 107);
  }
</style>

<main>
  <!-- <div>
    {#each pokemonTest as p}
      <p>{p.name}</p>
      <p>{p.base_experience}exp</p>
      <p>{p.weight}kg</p>
      <p>{p.height}m</p>
      {#each p.types as types}
        <p>{types.type.name}</p>
      {/each}
      {#each p.abilities as ab}
        <p>{ab.ability.name}</p>
      {/each}
    {/each}
  </div> -->
  <div class="container text-white">
    <div class="d-flex flex-wrap justify-content-center">
      <div class="input-group mb-3">
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
        <div class="m-1">
          <!-- Name -->
          <div class="text-center font-weight-bold">
            <div class="text-capitalize">{poke.name}</div>
          </div>
          <!-- End Name -->
          <div class="">
            <div>
              <img src={poke.sprites.front_default} alt="" />
            </div>
          </div>
          <!-- Type -->
          <div class="text-center">
            <div class="">
              {#each poke.types as types}
                <span class="badge badge-secondary m-1 p-2">
                  {types.type.name}
                </span>
              {/each}
            </div>
          </div>
          <!-- End Type -->
          <!-- Height / Weight -->
          <!-- <div class="text-center mt-2">
            <div class="">
              <p>Weight: {poke.weight}kg</p>
              <p>Height: {poke.height}m</p>
            </div>
          </div> -->
          <!-- End Height / Weight -->
          <!-- Abilities -->
          <div class="mt-4">
            <div class="">
              <!-- title -->
              <div class="">
                <div class="font-weight-bold">Abilities</div>
              </div>
              <!-- End title-->
              <div class="">
                <div class="">
                  {#each poke.abilities as abil}
                    <div class="">
                      <div class=" m-2 text-white" id="abil">
                        {abil.ability.name}
                      </div>
                    </div>
                  {/each}
                </div>
              </div>
            </div>
          </div>
          <!-- End Abilities -->
          <button class="btn-sm btn-primary m-2">View</button>
        </div>
      {/each}
    </div>
  </div>
</main>
