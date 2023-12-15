<script lang="ts">
	let squares = new Array(3).fill(null).map(() => new Array(3).fill(false));

  $: isWinner = squares.every(row => row.every(col => col));

	/**
	 * @param {number} row
	 * @param {number} col
	 */
	function clickSquare(row: number, col: number) {
    updateSquareState(row, col);
    updateSquareState(row-1, col);
    updateSquareState(row+1, col);
    updateSquareState(row, col-1);
    updateSquareState(row, col+1);
	}

  /**
	 * @param {number} row
	 * @param {number} col
	 */
  function updateSquareState(row: number, col: number) {
    if (isWinner) return;
    if (row < 0 || row >= 3 || col < 0 || col >= 3) return;

    squares[row][col] = !squares[row][col];
  }
</script>

<div class="container mx-auto">
  <div class="p-4 flex flex-col text-center items-center">
    <h1 class="text-3xl font-bold">Acenda todos os blocos</h1>
    <p class="mb-4">O quadrado clicado acende os adjacentes</p>
    
    <div>
      <table class="table">
        {#each Array(3) as _, row}
        <tr>
          {#each Array(3) as _, col}
          <td class="w-1/3 h-1/3 p-2">
            <button 
              disabled={isWinner}
              on:click={() => clickSquare(row, col)} 
              class="square {!isWinner ? 'clickable' : 'cursor-default'} {squares[row][col] ? 'glow' : ''}"
            ></button>
          </td>
        {/each}
        </tr>
        {/each}
      </table>
    </div>

    {#if isWinner}
    <h4 class="mt-4 text-green-500 text-3xl">
      Parabéns, você conseguiu!
    </h4>
    {/if}
  </div>
</div>

<style lang="scss">
  .table {
    @apply min-w-[375px] min-h-[375px] w-full h-full p-4;

    @screen sm {
      @apply min-w-[500px] min-h-[500px];
    }

    @screen md {
      @apply min-w-[700px] min-h-[700px];
    }
  }
  
  .square {
    @apply w-full h-full rounded-md bg-gray-600;
  }

  .clickable {
    @apply cursor-pointer;

    &:hover {
      @apply bg-green-800 shadow-[inset_0_0_4px_4px_rgba(0,0,0,0.6)];
    }
  }

  .glow {
    @apply bg-green-700;
  }
</style>