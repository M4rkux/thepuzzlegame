<script lang="ts">
  let foxElement: HTMLDivElement;
  let cornElement: HTMLDivElement;
  let chickenElement: HTMLDivElement;
  let leftSide = [
    {
      isPlaced: true,
      top: "2.5rem",
      left: "7rem"
    },
    {
      isPlaced: true,
      top: "2.5rem",
      left: "11rem"
    },
    {
      isPlaced: true,
      top: "2.5rem",
      left: "15rem"
    },
  ]

  function toggleElementOnBoat(element: HTMLDivElement) {
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
    <div class="relative w-[500px] h-[400px] bg-green-700 rounded-sm mx-auto">
      <div class="fox" bind:this={foxElement} on:click={() => toggleElementOnBoat(foxElement)}></div>
      <div class="corn" bind:this={cornElement} on:click={() => toggleElementOnBoat(cornElement)}></div>
      <div class="chicken" bind:this={chickenElement} on:click={() => toggleElementOnBoat(chickenElement)}></div>
      <div class="farmer"></div>
      <div class="river"></div>
      <button class="btn-play">Navegar</button>
    </div>
  </div>
</div>

<style lang="scss">
  .chicken, .fox, .corn, .farmer {
    @apply absolute w-[48px] h-[48px] rounded-full z-10;
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

  .river {
    @apply absolute w-[200px] h-full bg-blue-500 z-0 left-28 shadow-gray-500;

    box-shadow: inset 0px 0 4px 2px green;
  }

  .btn-play {
    @apply border-2 border-green-950 bg-green-900 text-white px-4 py-2 absolute left-1/3 top-2/3 rounded-md;

    &:hover {
      @apply bg-green-800;
    }
  }
</style>