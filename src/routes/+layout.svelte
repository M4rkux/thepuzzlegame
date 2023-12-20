<script>
	import "../app.scss";
</script>

<svelte:head>
	<title>The puzzle game</title>
</svelte:head>

<div class="content">
	<slot />
</div>

<style lang="scss">
	.content {
		@apply p-4;
	}
</style>