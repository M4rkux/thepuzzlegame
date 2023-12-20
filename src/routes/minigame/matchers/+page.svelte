<script lang="ts">
	import MatcherNumber from "../../../components/matcherNumber.svelte";

  const defaultNumbers = [
    [true, true, false, true, false, true, true],
    [true, true, true, true, false, true, true],
    [true, true, true, true, false, true, true],
  ];
  let number1 = [...defaultNumbers[0]];
  let number2 = [...defaultNumbers[1]];
  let numberResult = [...defaultNumbers[2]];
  let isGameComplete = false;
  let isRemoving = true;
  // fn check isRemoving e revert
  // fn check !isRemoving e completa o jogo

  function clickSegment(numberIndex: number, segmentIndex: number) {
    if (isGameComplete) return;
    if (!isRemoving) {
      isGameComplete = true;
    }
    isRemoving != isRemoving;
    switch (numberIndex) {
      case 0:
        number1[numberIndex] != number1[numberIndex];
        break;
      case 1:
        numberResult[numberIndex] != numberResult[numberIndex];
        break;
      case 2:
        numberResult[numberIndex] != numberResult[numberIndex];
        break;
    }
  }
</script>

<div class="flex flex-row text-9xl items-center gap-4">
  <MatcherNumber disabled={isGameComplete} isRemoving={isRemoving} numberSeguments={number1} on:click={clickSegment} />
  <span class="w-[72px] text-center">+</span>
  <MatcherNumber disabled={isGameComplete} isRemoving={isRemoving} numberSeguments={number2} on:click={clickSegment} />
  <span class="w-[72px] text-center">=</span>
  <MatcherNumber disabled={isGameComplete} isRemoving={isRemoving} numberSeguments={numberResult} on:click={clickSegment} />
</div>