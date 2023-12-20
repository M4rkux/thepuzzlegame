<script lang="ts">
	let isFullScreen = false;
	function handleToggleFullScreen() {
		if (isFullScreen) {
			document.documentElement.requestFullscreen();
		} else {
			document.exitFullscreen();
		}
	}
</script>

<div class="flex w-full">
	<div class="m-auto">
		<h1 class="text-2xl">Welcome to the puzzle game</h1>
		<ul>
			<li>Criar página inicial</li>
			<li>Criar component de menu</li>
			<li>Criar home com o puzzle principal e os mini games pra conseguir informação</li>
			<li>Criar uma versão adaptada do "teste de QI de Einstein"</li>
			<li>
				Criar cada mini game
				<ul class="pl-4">
					<li><a href="/minigame/adjacent">Adjacent</a></li>
					<li><a href="/minigame/hanoi">Hanoi</a></li>
					<li><a href="/minigame/fox-and-chicken">Raposa e a galinha</a></li>
					<li><a href="/minigame/matchers">Palitos (5 + 9 = 9)</a></li>
					<li><a href="/minigame/console">Console</a></li>
				</ul>
			</li>
			<li>Salvar o progresso em local storage</li>
			<li>Botão para compartilhar a tela de vitória</li>
			<li>Criar tradução EN/PT</li>
			<li>
				<label
					><input type="checkbox" bind:checked={isFullScreen} on:change={handleToggleFullScreen} /> Full
					screen</label
				>
			</li>
		</ul>
	</div>
</div>
