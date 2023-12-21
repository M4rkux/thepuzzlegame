<script lang="ts">
	import MatchNumber from "../../../components/matchNumber.svelte";

  const defaultNumbers = [5,9,9];
  let number1 = defaultNumbers[0];
  let number2 = defaultNumbers[1];
  let numberResult = defaultNumbers[2];
  let isGameComplete = false;
  let isRemoving = true;
  $: isResultCorrect = number1 + number2 === numberResult;

  function reset() {
    number1 = defaultNumbers[0];
    number2 = defaultNumbers[1];
    numberResult = defaultNumbers[2];
    isGameComplete = false;
    isRemoving = true;
  }
</script>

<div class="container mx-auto">
	<div class="p-4 flex flex-col items-center">

    <h1 class="mb-4">Palitos</h1>
    <div class="mx-auto mb-10">
      <p>Seu objetivo é fazer a conta ficar matematicamente correta</p>
      <p>Você só pode mover 1 único palito</p>
      <p>Clique em um palito para remover e depois em um espaço vazio para colocar</p>
    </div>
<div class="flex flex-row text-9xl items-center gap-4">
  <MatchNumber bind:isGameComplete={isGameComplete} bind:isRemoving={isRemoving} bind:number={number1} />
  <span class="w-[64px] text-center">+</span>
  <MatchNumber bind:isGameComplete={isGameComplete} bind:isRemoving={isRemoving} bind:number={number2} />
  <span class="w-[64px] text-center">=</span>
  <MatchNumber bind:isGameComplete={isGameComplete} bind:isRemoving={isRemoving} bind:number={numberResult} />
</div>
</div>
</div>

<div class="flex flex-col">
  {#if isGameComplete}
    {#if isResultCorrect}
      <h2 class="text-center mt-4 text-green-500">Parabéns, você completou o nível</h2>
    {:else}
      <h2 class="text-center">O resultado está incorreto</h2>
      <button on:click={reset} class="border-red-950 border-2 rounded-md bg-red-900 text-white px-4 py-2 mx-auto hover:bg-red-800">Jogar novamente</button>
    {/if}
  {/if}
</div>