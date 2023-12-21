<script lang="ts">
  let foxElement: HTMLButtonElement;
  let cornElement: HTMLButtonElement;
  let chickenElement: HTMLButtonElement;
  const foxObject = {
    top: "112px",
    leftSide: {
      left: "40px",
    },
    rightSide: {
      left: "600px",
    }
  }

  function toggleElementOnBoat(element: HTMLButtonElement) {
    element.style.top = element.style.top === "10rem" ? "5rem" : "10rem";
  }
</script>

<div class="container mx-auto">
	<div class="p-4 flex flex-col items-center">

    <h1 class="mb-4">Travessia</h1>
    <div class="mx-auto mb-10">
      <p>Seu objetivo é atravessar todo mundo para o lado direito do rio.</p>
      <p>Você só pode atravessar 1 por vêz</p>
      <p>Alguns desastres podem acontecer e você deve evitá-los.</p>
      <p>Se a galinha ficar só com o milho, ela irá comê-lo.</p>
      <p>Se a raposa ficar só com a galinha, ela irá comê-la.</p>
    </div>
    <div class="game">
      <button class="fox" bind:this={foxElement} on:click={() => toggleElementOnBoat(foxElement)}>R</button>
      <button class="corn" bind:this={cornElement} on:click={() => toggleElementOnBoat(cornElement)}>M</button>
      <button class="chicken" bind:this={chickenElement} on:click={() => toggleElementOnBoat(chickenElement)}>G</button>
      <div class="farmer"></div>
      <button class="btn-play">Navegar</button>
    </div>
  </div>
</div>

<style lang="scss">
  .chicken, .fox, .corn, .farmer {
    @apply absolute w-[48px] h-[48px] rounded-full z-10 text-black;
    transition-property: left, top, translate;
    transition-duration: 250ms;
    transition-timing-function: ease-in;
  }

  .chicken, .fox, .corn {
    &:hover {
      @apply border-2 border-black cursor-pointer;
    }
  }

  .fox {
    @apply left-10 top-28 bg-orange-500;
  }

  .corn {
    @apply left-10 top-44 bg-yellow-500;
  }

  .chicken {
    @apply left-10 top-60 bg-gray-100;
  }

  .farmer {
    @apply left-40 top-40 bg-amber-800;
  }

  .game {
    @apply relative w-[700px] h-[500px] rounded-sm mx-auto;

    background-image: url("/imgs/river.jpeg");
    background-position: center;
    background-size: auto;
  }

  .btn-play {
    @apply border-2 border-green-950 bg-green-900 text-white px-4 py-2 absolute left-0 right-0 mx-auto w-[200px] top-2/3 rounded-md;

    &:hover {
      @apply bg-green-800;
    }
  }
</style>