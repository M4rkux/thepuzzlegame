<script lang="ts">
  const disks = [...new Array(6).keys()];
  const poles = [
    [...disks],
    [],
    []
  ];
</script>

<div class="flex flex-col align-middle items-center w-[210px]">
  {#each poles as poleDisks}
    {#each poleDisks as disk, i}
      <div class="disk disk-{disk} {i === 0 && 'grabbable'}"></div>
    {/each}
  {/each}
</div>

<style lang="scss">
  .disk {
    @apply block h-[24px] rounded-lg border-black border-solid border-[1px];

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

  .grabbable {
    @apply cursor-grab;

    &:hover {
      @apply shadow-[0_0_2px_2px] shadow-sky-100;
    }

    &:active {
      @apply cursor-grabbing shadow-[0_0_2px_1px] shadow-sky-100;
    }
  }
</style>