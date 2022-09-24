<script>
  import Character from "./Character.svelte";
  import combatMessages from "./messages.js";
  let charName1 = "";
  let charName2 = "";
  let hp1 = 30;
  let hp2 = 30;

  let messages = [];
  let winner = "";

  function randomCombatMsg() {
    // get random index value
    const randomIndex = Math.floor(Math.random() * combatMessages.length);

    // get random item
    const item = combatMessages[randomIndex];

    return item;
  }
  function startFight() {
    console.log("start fight");
    messages = [];
    winner = "";
    hp1 = 30;
    hp2 = 30;
    let turn = 0;

    while (hp1 > 0 && hp2 > 0) {
      turn++;
      let msg = randomCombatMsg();
      let formattedMsg;
      if (turn % 2 == 0) {
        // then it must be A's turn
        formattedMsg = String(msg[0])
          .replaceAll("$A1", charName1)
          .replaceAll("$A2", charName2)
          .concat(` (-${msg[1]} HP)`);
        hp2 -= Number(msg[1]);
      } else {
        // then it must be B's turn
        formattedMsg = String(msg[0])
          .replaceAll("$A1", charName2)
          .replaceAll("$A2", charName1)
          .concat(` (-${msg[1]} HP)`);
        hp1 -= Number(msg[1]);
      }
      messages = [...messages, formattedMsg];
    }
    if (hp1 > 0) {
      winner = charName1;
      console.log(`${charName1} wins`);
    }
    if (hp2 > 0) {
      winner = charName2;
      console.log(`${charName2} wins`);
    }
  }
</script>

<main class="m-4">
  <h1 class="text-3xl font-bold">simulated pvp battle v1.0</h1>
  <div class="flex flex-col sm:flex-row gap-4">
    <Character bind:name={charName1} />
    <Character bind:name={charName2} />
  </div>
  {#if charName1 && charName2}
    <h2 class="text-3xl mt-4 font-semibold">{charName1} vs {charName2}</h2>
    <button
      on:click={startFight}
      class="text-xl text-blue-700 hover:text-blue-400 py-2 px-4 rounded bg-gray-200 font-bold"
      >WHO WOULD WIN?</button
    >
    <ul class="list-disc list-inside">
      {#each messages as msg}
        <li>{msg}</li>
      {/each}
    </ul>

    {#if winner}
      <p class="text-xl font-semibold">
        {winner} is the winner!
      </p>
    {/if}
  {/if}
</main>
