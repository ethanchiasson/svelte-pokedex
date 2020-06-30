<script>
  import SearchBar from "../src/searchCom.svelte";

  let word = "ditto";
  let numPoke = 151;
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

  #abil {
    border-radius: 0.5em;
    background-color: white;
  }

  .grass,
  .fire,
  .bug,
  .poison,
  .flying,
  .electric,
  .water,
  .ground,
  .normal,
  .fairy,
  .fighting,
  .rock,
  .steel,
  .psychic,
  .ghost,
  .ice,
  .dragon {
    border-radius: 0.25em;
    color: black;
    font-weight: bold;
    padding: 0.25em;
    margin: 0.2em;
  }
  .grass {
    background: greenyellow;
  }
  .fire {
    background: red;
  }
  .bug {
    background: lightcoral;
  }
  .poison {
    background: violet;
  }
  .water {
    background-color: lightskyblue;
  }
  .electric {
    background: yellow;
  }
  .flying {
    background: #c4c4c4;
  }
  .electric {
    background: yellow;
  }

  .ground {
    background-color: chocolate;
  }

  .normal {
    background-color: dimgrey;
  }

  .fairy {
    background-color: palevioletred;
  }

  .fighting {
    background-color: orangered;
  }

  .rock {
    background-color: silver;
  }

  .ghost {
    background-color: whitesmoke;
  }

  .psychic {
    background-color: darkorchid;
  }

  .steel {
    background-color: slategrey;
  }

  .ice {
    background-color: aquamarine;
  }

  .dragon {
    background-color: crimson;
  }
</style>

<main>
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
                <span
                  class={types.type.name}
                  style="background-color={types.type.name}">
                  {types.type.name}
                </span>
              {/each}
            </div>
          </div>
          <!-- End Type -->
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
                      <div class=" m-2 bg-dark text-white" id="abil">
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
