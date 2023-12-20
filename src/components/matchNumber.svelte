<script lang="ts">
  export let isRemoving = false;
  export let isGameComplete = false;
  export let number = 8;
  
  const numbersSegments = [
    [true, true, true, false, true, true, true], // 0
    [false, false, true, false, false, true, false], // 1
    [true, false, true, true, true, false, true], // 2
    [true, false, true, true, false, true, true], // 3
    [false, true, true, true, false, true, false], // 4
    [true, true, false, true, false, true, true], // 5
    [false, true, false, true, true, true, true], // 6
    [true, true, true, false, false, true, false], // 7
    [true, true, true, true, true, true, true], // 8
    [true, true, true, true, false, true, true], // 9
  ];

  let numberSeguments: Array<boolean> = [...numbersSegments[8]];
  $: numberSeguments = number >=0 && number < numbersSegments.length ? [...numbersSegments[number]] : numberSeguments;
  $: isValidNumber = numbersSegments.some((nss) => nss.every((ns, i) => ns === numberSeguments[i]));

  function handleClick(segmentIndex: number) {
    if (isGameComplete) return;
    if (!isRemoving) {
      isGameComplete = true;
    }
    isRemoving = !isRemoving;
    numberSeguments[segmentIndex] = !numberSeguments[segmentIndex];
    
    number = numbersSegments.findIndex((nss) => nss.every((ns, i) => ns === numberSeguments[i]));
  }
</script>

<div class="seven-segment {isGameComplete && 'isGameComplete'} {!isValidNumber ? 'animate-pulse' : ''}">
  <button
    on:click={() => handleClick(0)}
    disabled={isGameComplete || ((!numberSeguments[0] && isRemoving) || (numberSeguments[0] && !isRemoving))}
    class="{numberSeguments[0] ? 'present' : 'absent'} {!isGameComplete && ((!numberSeguments[0] && !isRemoving) || (numberSeguments[0] && isRemoving)) ? 'clickable' : ''} col-start-2 col-end-2 segment segment-horizontal"
  />
  <button
    on:click={() => handleClick(1)}
    disabled={isGameComplete || ((!numberSeguments[1] && isRemoving) || (numberSeguments[1] && !isRemoving))}
    class="{numberSeguments[1] ? 'present' : 'absent'} {!isGameComplete && ((!numberSeguments[1] && !isRemoving) || (numberSeguments[1] && isRemoving)) ? 'clickable' : ''} col-start-1 col-end-1 segment segment-vertical"
  />
  <button
    on:click={() => handleClick(2)}
    disabled={isGameComplete || ((!numberSeguments[2] && isRemoving) || (numberSeguments[2] && !isRemoving))}
    class="{numberSeguments[2] ? 'present' : 'absent'} {!isGameComplete && ((!numberSeguments[2] && !isRemoving) || (numberSeguments[2] && isRemoving)) ? 'clickable' : ''} col-start-3 col-end-3 segment segment-vertical"
  />
  <button
    on:click={() => handleClick(3)}
    disabled={isGameComplete || ((!numberSeguments[3] && isRemoving) || (numberSeguments[3] && !isRemoving))}
    class="{numberSeguments[3] ? 'present' : 'absent'} {!isGameComplete && ((!numberSeguments[3] && !isRemoving) || (numberSeguments[3] && isRemoving)) ? 'clickable' : ''} col-start-2 col-end-2 segment segment-horizontal"
  />
  <button
    on:click={() => handleClick(4)}
    disabled={isGameComplete || ((!numberSeguments[4] && isRemoving) || (numberSeguments[4] && !isRemoving))}
    class="{numberSeguments[4] ? 'present' : 'absent'} {!isGameComplete && ((!numberSeguments[4] && !isRemoving) || (numberSeguments[4] && isRemoving)) ? 'clickable' : ''} col-start-1 col-end-1 segment segment-vertical"
  />
  <button
    on:click={() => handleClick(5)}
    disabled={isGameComplete || ((!numberSeguments[5] && isRemoving) || (numberSeguments[5] && !isRemoving))}
    class="{numberSeguments[5] ? 'present' : 'absent'} {!isGameComplete && ((!numberSeguments[5] && !isRemoving) || (numberSeguments[5] && isRemoving)) ? 'clickable' : ''} col-start-3 col-end-3 segment segment-vertical"
  />
  <button
    on:click={() => handleClick(6)}
    disabled={isGameComplete || ((!numberSeguments[6] && isRemoving) || (numberSeguments[6] && !isRemoving))}
    class="{numberSeguments[6] ? 'present' : 'absent'} {!isGameComplete && ((!numberSeguments[6] && !isRemoving) || (numberSeguments[6] && isRemoving)) ? 'clickable' : ''} col-start-2 col-end-2 segment segment-horizontal"
  />
</div>

<style lang="scss">
.seven-segment {
  @apply grid w-[72px] h-[136px] gap-1;
}

.segment {
  @apply rounded-sm cursor-default;

  &.clickable {
    @apply cursor-pointer;
    &:hover {
      @apply bg-red-400 shadow-red-100 shadow-sm;
    }
  }

  &.present {
    @apply bg-stone-100;
  }

  &.absent {
    @apply bg-stone-800;
  }

  &-vertical {
    @apply h-[48px] w-2;
  }

  &-horizontal {
    @apply h-2 w-[48px];
  }
}
</style>