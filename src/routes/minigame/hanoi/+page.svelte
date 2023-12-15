<script lang="ts">
  const disks = [...new Array(6).keys()];
  let poles = [
    [...disks],
    [],
    []
  ];
  let currentDisk: number = -1;
  let hoverPole: number = 0;
  const poleElements: HTMLButtonElement[] = [];

  function handleClickDisk(poleIndex: number) {
    if (currentDisk < 0) {
      currentDisk = poles[poleIndex].shift() as number;
    }
    poles = poles;
    hoverPole = poleIndex;
  }
  
  function handleClickPole(poleIndex: number) {
    if (currentDisk > -1 && (!poles[poleIndex].length || currentDisk < poles[poleIndex][0])) {
      poles[poleIndex].unshift(currentDisk);
      currentDisk = -1;
      poles = poles;
    }
  }

  function handleHoverPole(poleIndex: number) {
    hoverPole = poleIndex;
  }

  function handleKeyPress(e: KeyboardEvent) {
    const element = document.activeElement;
    const clickableElements = Array.from(document.querySelectorAll("button:not([disabled])")) as HTMLButtonElement[];
    if (element?.classList.contains("pole")) {
      hoverPole = Number(((element as HTMLButtonElement).name));
    }
    switch (e.code) {
      case "ArrowUp":
        if (currentDisk === -1) {
          (document.activeElement as HTMLButtonElement).click();
        }
        break;
      case "ArrowRight":
        focusNext(clickableElements);
        break;
      case "ArrowDown":
        if (currentDisk > -1) {
          handleClickPole(hoverPole);
        }
        break;
      case "ArrowLeft":
        focusPrev(clickableElements);
        break;
    }
  }

  function focusNext(clickableElements: HTMLButtonElement[]) {
    
    if (currentDisk > -1) {
      if (hoverPole < poleElements.length - 1) {
        hoverPole++;
      } else {
        hoverPole = 0;
      }
      poleElements[hoverPole].focus();
    } else {
      const selectedIndex = clickableElements.indexOf(document.activeElement as HTMLButtonElement);
      if (selectedIndex < clickableElements.length - 1) {
        clickableElements[selectedIndex + 1].focus();
      } else {
        clickableElements[0].focus();
      }
    }
  }

  function focusPrev(clickableElements: HTMLButtonElement[]) {
    if (currentDisk > -1) {
      if (hoverPole > 0) {
        hoverPole--;
      } else {
        hoverPole = poleElements.length - 1;
      }
      poleElements[hoverPole].focus();
    } else {
      const selectedIndex = clickableElements.indexOf(document.activeElement as HTMLButtonElement);
      if (selectedIndex > 0) {
        clickableElements[selectedIndex - 1].focus();
      } else {
        clickableElements[clickableElements.length - 1].focus();
      }
    }
  }
</script>

<div class="w-full flex">
  <div class="mx-auto flex flex-row relative">
    {#if currentDisk > -1}
      <div class="w-[230px] floating floating-{hoverPole}">
        <button class="disk disk-{currentDisk}" />
      </div>
    {/if}
    {#each poles as poleDisks, poleIndex}
      <!-- svelte-ignore a11y-no-static-element-interactions -->
      <div class="flex flex-col justify-end items-center w-[230px] h-[230px] border-b-2 border-black pt-4 px-auto relative" on:mouseenter={() => handleHoverPole(poleIndex)}>
        <button class="pole {poleIndex === poles.length - 1 && 'pole-goal'} {currentDisk > -1 && 'clickable'}" name={`${poleIndex}`} disabled={currentDisk === -1} on:click={() => handleClickPole(poleIndex)} bind:this={poleElements[poleIndex]} />
        {#each poleDisks as disk, i}
          <button class="disk disk-{disk} {currentDisk === -1 && i === 0 && 'clickable'}" disabled={currentDisk > -1 || i > 0} on:click={() => handleClickDisk(poleIndex)} />
        {/each}
      </div>
    {/each}
  </div>
</div>

<svelte:window on:keyup={handleKeyPress} />

<style lang="scss">
  .disk {
    @apply block h-[24px] rounded-lg border-black border-solid border-[1px] z-10 cursor-default transition-transform;

    &-0 {
      @apply bg-purple-700 w-[60px];
    }

    &-1 {
      @apply bg-blue-600 w-[90px];
    }

    &-2 {
      @apply bg-green-600 w-[120px];
    }

    &-3 {
      @apply bg-yellow-500 w-[150px];
    }

    &-4 {
      @apply bg-orange-500 w-[180px];
    }

    &-5 {
      @apply bg-red-800 w-[210px];
    }
  }

  .floating {
    @apply absolute flex justify-center transition-all;

    button {
      @apply shadow-[0_0_2px_1px];
    }

    &-0 {
      @apply translate-x-0;
    }
    &-1 {
      @apply translate-x-[230px];
    }
    &-2 {
      @apply translate-x-[460px];
    }
  }

  .pole {
    @apply bg-amber-800 w-[20px] h-[160px] block rounded-t-lg border-black border-solid border-[1px] absolute z-0 bottom-0 cursor-default;

    &-goal {
      @apply bg-yellow-700;
    }
  }

  .clickable {
    @apply cursor-pointer;

    &:hover, &:active {
      @apply shadow-sky-100;
    }

    &.disk {
      &:hover {
        @apply shadow-[0_0_2px_2px] -translate-y-px rotate-3;
      }

      &:active {
        @apply shadow-[0_0_2px_1px];
      }
    }

    &.pole {
      &:hover, &:active, &:focus {
        @apply shadow-[0_-3px_2px_2px];
      }
    }
  }
</style>