<script lang="ts">
	import { goto } from "$app/navigation";
	import { onMount } from "svelte";

  interface Commands {
    [key: string]: Function
  }

  const commands: Commands = {
    "help": helpCommand,
    "whoami": whoamiCommand,
    "birthday": birthdayCommand,
    "pizzatime": pizzatimeommand,
    "clear": clearCommand,
    "solve": solveCommand,
    "exit": exitCommand
  };
  const birthDate = new Date("1992-01-15T00:00:00");
  const password = "pizza1992";

  let consoleHistory: string[] = [];
  let commandHistory: string[] = [];
  let command: string = "";
  let commandElement: HTMLInputElement;
  let indexHistory: number = -1;
  let isSolving = false;

  $: commandHighlighted = () => {
    return isSolving ? "*".repeat(command.length) : `<span class="${command in commands ? "text-green-500" : "text-red-500"} font-semibold">${command}</span>`;
  }

  $: idade = calculateAge();

  onMount(() => {
    commandElement.focus();
  });

  function helpCommand() {
    addConsoleHistory(`Este são os possíveis comandos:
    <ul>
      <li><span class="font-semibold text-yellow-100">help</span> <span class="italic">para mostrar todos os comandos</span></li>
      <li><span class="font-semibold text-yellow-100">whoami</span> <span class="italic">para mostrar os dados do proprietário</span></li>
      <li><span class="font-semibold text-yellow-100">birthday</span> <span class="italic">para mostrar a data de aniversário</span></li>
      <li><span class="font-semibold text-yellow-100">pizzatime</span> <span class="italic">It's pizza time!</span></li>
      <li><span class="font-semibold text-yellow-100">clear</span> <span class="italic">para limpar os dados do console</span></li>
      <li><span class="font-semibold text-yellow-100">solve</span> <span class="italic">para resolver o puzzle</span></li>
      <li><span class="font-semibold text-yellow-100">exit</span> <span class="italic">para sair do console</span></li>
    </ul>
    `);
  }

  function calculateAge(): number {
    const currentDate = new Date();
    let age = currentDate.getFullYear() - birthDate.getFullYear();

    if (currentDate.getMonth() < birthDate.getMonth() || 
        (currentDate.getMonth() === birthDate.getMonth() && 
        currentDate.getDate() < birthDate.getDate())) {
      age--;
    }

    return age;
  }

  function whoamiCommand() {
    addConsoleHistory(`Meu nome é Marcus, sou programador e tenho ${idade} anos`);
  }

  function birthdayCommand() {
    const dateFormatter = new Intl.DateTimeFormat("pt-BR", {
      day: "numeric",
      month: "long"
    });
 
    const isBirthdayToday = dateFormatter.format(birthDate) === dateFormatter.format(new Date());
    addConsoleHistory(`Meu aniversário é ${dateFormatter.format(birthDate)}. ${isBirthdayToday ? "<br/>É hoje!!!</b>" : ""}`);
  }

  function clearCommand() {
    consoleHistory = [];
  }

  function pizzatimeommand() {
    addConsoleHistory(`🍕🍕🍕🍕🍕🍕🍕🍕🍕🍕<br/>🍕IT'S PIZZA TIME! 🍕<br/>🍕🍕🍕🍕🍕🍕🍕🍕🍕🍕`);
  }

  function solveCommand() {
    addConsoleHistory(`Dica: comida favorita + ano de nascimento`);
    isSolving = true;
  }

  function exitCommand() {
    addConsoleHistory(`Exiting...`);
    setTimeout(() => {
      goto("/");
    }, 500);
  }

  function addConsoleHistory(text: string = "") {
    consoleHistory = [...consoleHistory, `${!isSolving ? `<span class="mt-2 block">$ <span class="text-yellow-200 font-semibold">${command}</span></span>` : ""}${text}`];
  }

  function runCommand() {
    if (command in commands) {
      commands[command]();
    } else if (isSolving) {
      if (command === password) {
        addConsoleHistory(`<span class="text-yellow-100">Parabéns! Você desbloqueou o nível.</span>`);
      } else {
        addConsoleHistory(`<span class="text-red-200">Senha inválida.</span>`);
      }
      isSolving = false;
    } else {
      addConsoleHistory();
    }
  }

  function handleInput(e: KeyboardEvent) {
    switch (e.key) {
      case "ArrowUp":
        if (indexHistory < commandHistory.length - 1) {
          command = commandHistory[++indexHistory];
        }
        break;
      case "ArrowDown":
        if (indexHistory > 0) {
          command = commandHistory[--indexHistory];
        } else if (indexHistory === 0) {
          command = "";
          indexHistory = -1;
        }
        break;
      case "Enter":
        command = command.replaceAll(/<[^>]*>/g, "");
        if (!isSolving) {
          commandHistory = [command, ...commandHistory];
        }
        runCommand();
        command = "";
        indexHistory = -1;
        break;
      case "c":
        if (e.ctrlKey) {
          addConsoleHistory(isSolving ? "password:" : "");
          isSolving = false;
          command = "";
          indexHistory = -1;
        }
        break;
    }
  }
</script>
<h1>Console</h1>
<p>Você precisa digitar o comando correto para desbloquear o nível, tente digitar <b>help</b> para obter ajuda.</p>
<div class="mt-4 rounded-sm bg-gray-700 p-1 font-mono border-b-2 border-gray-500">
  <div class="flex flex-col justify-end min-h-[200px]">
    {#each consoleHistory as text}
      <p>{@html text}</p>
    {/each}
  </div>
  <div class="flex mt-1">
    <span class="mr-1 whitespace-nowrap">$ {isSolving ? " password:" : ""}</span>
    <div class="relative w-full">
      <input type="text" bind:value={command} class="bg-transparent caret-white border-transparent outline-0 absolute w-full text-transparent" bind:this={commandElement} on:keydown={handleInput} />
      <span class="absolute">{@html commandHighlighted()}</span>
    </div>
  </div>
</div>