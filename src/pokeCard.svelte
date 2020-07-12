<script>
  export let poke;
  import { fly } from "svelte/transition";
</script>

<style>
  main > div {
    border-radius: 0.4em;
    min-width: 200px;
    /* min-height: 350px; */
    -webkit-transition: -webkit-transform 0.8s ease-in-out;
    transition: transform 0.8s ease-in-out;
  }

  main > div:hover {
    box-shadow: 3px 3px 12px #474747;
    cursor: pointer;
    position: relative;
    bottom: 1em;
    bottom: 1em;
    -webkit-transform: rotate(5deg);
    transform: rotate(5deg);
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
  .dragon,
  .dark,
  .grass2,
  .poison2,
  .dark2,
  .fire2,
  .bug2,
  .water2,
  .electric2,
  .flying2,
  .normal2,
  .ground2,
  .fairy2,
  .fighting2,
  .rock2,
  .psychic2,
  .ghost2,
  .dragon2,
  .ice2,
  .steel2 {
    border-radius: 0.25em;
    color: black;
    font-weight: bold;
    padding: 0.25em;
    margin: 0.2em;
  }

  .dark {
    color: white;
    background-image: -webkit-linear-gradient(30deg, #121212 50%, #212121 50%);
  }

  .dark2 {
    background-color: #000000;
    color: white;
  }
  .grass {
    background-image: -webkit-linear-gradient(30deg, #28ad8e 50%, #2cdab1 50%);
  }
  .grass2 {
    background-color: #2cdab1;
  }

  .fire {
    background-image: -webkit-linear-gradient(30deg, #dd6153 50%, #f7786b 50%);
  }

  .fire2 {
    background: #f7786b;
  }

  .bug {
    background: greenyellow;
    background-image: -webkit-linear-gradient(
      30deg,
      rgb(147, 221, 37) 50%,
      greenyellow 50%
    );
  }

  .bug2 {
    background: greenyellow;
  }

  .poison {
    background-image: -webkit-linear-gradient(
      30deg,
      violet 50%,
      rgb(182, 88, 182) 50%
    );
  }

  .poison2 {
    background: violet;
  }
  .water {
    background-image: -webkit-linear-gradient(30deg, #3e91da 50%, #58abf6 50%);
  }

  .water2 {
    background-color: #58abf6;
  }

  .electric {
    background-image: -webkit-linear-gradient(
      30deg,
      #ffce4b 50%,
      rgb(241, 241, 69) 50%
    );
  }

  .electric2 {
    background: rgb(241, 241, 69);
  }

  .flying {
    background-image: -webkit-linear-gradient(30deg, #c9c9c9 50%, #c4c4c4 50%);
  }

  .flying2 {
    background: #c4c4c4;
  }

  .ground {
    background-image: -webkit-linear-gradient(30deg, #af6b63 50%, #c47e76 50%);
  }

  .ground2 {
    background-color: #c47e76;
  }

  .normal {
    background-image: -webkit-linear-gradient(30deg, dimgrey 50%, grey 50%);
  }
  .normal2 {
    background-color: grey;
  }

  .fairy {
    background-image: -webkit-linear-gradient(
      30deg,
      palevioletred 50%,
      pink 50%
    );
  }

  .fairy2 {
    background-color: pink;
  }

  .fighting {
    background-image: -webkit-linear-gradient(
      30deg,
      rgb(216, 58, 0) 50%,
      orangered 50%
    );
  }

  .fighting2 {
    background-color: orangered;
  }

  .rock {
    background-image: -webkit-linear-gradient(30deg, #757575 50%, #888888 50%);
  }

  .rock2 {
    background-color: #888888;
  }

  .ghost {
    background-image: -webkit-linear-gradient(
      30deg,
      rgb(233, 233, 233) 50%,
      whitesmoke 50%
    );
  }

  .ghost2 {
    background-color: whitesmoke;
  }

  .psychic {
    background-image: -webkit-linear-gradient(30deg, #843fa0 50%, #9f5bba 50%);
  }

  .psychic2 {
    background-color: #9f5bba;
  }

  .steel {
    background-image: -webkit-linear-gradient(30deg, gray 50%, slategray 50%);
  }

  .steel2 {
    background-color: slategrey;
  }

  .ice {
    background-image: -webkit-linear-gradient(30deg, #bbc7f5 50%, #cfd9ff 50%);
  }
  .ice2 {
    background-color: #cfd9ff;
  }

  .dragon {
    background-image: -webkit-linear-gradient(
      30deg,
      rgb(179, 9, 43) 50%,
      crimson 50%
    );
  }

  .dragon2 {
    background-color: crimson;
  }

  #abil {
    border-radius: 0.5em;
    background-color: white;
  }

  #poke_id {
    border-radius: 1em;
    padding: 0.2em;
    max-width: 3em;
    margin: auto;
    text-align: center;
    background-color: white;
  }

  h5 {
    font-weight: bold;
  }
</style>

<main>

  <div
    data-toggle="modal"
    data-target="#exampleModal"
    transition:fly={{ x: -300, duration: 1000 }}
    class={JSON.stringify(poke.types[0].type.name).replace(/\"/g, '')}>
    <div class="">
      <div>
        <img src={poke.sprites.front_default} class="mt-2" alt="" />
      </div>
    </div>
    <!-- Name -->
    <div class="text-center font-weight-bold">
      <div class="text-capitalize">
        <h5>{poke.name}</h5>
      </div>
      <p id="poke_id" class="mt-1">#{poke.id}</p>
    </div>
    <!-- End Name -->
    <!-- Type -->
    <div class="text-center">
      <div class="text-light mt-5 mb-5">
        {#each poke.types as types}
          <span class={types.type.name + '2'} style="filter: brightness(110%);">
            {types.type.name}
          </span>
        {/each}
      </div>
    </div>
    <!-- End Type -->
    <!-- Abilities -->
    <!-- <div class="mt-4">
      <div class="">
        <div class="">
          <div class="font-weight-bold">Abilities</div>
        </div>
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
    </div> -->
    <!-- End Abilities -->
  </div>
</main>
