<script>
  import { onMount } from "svelte";
  let advice =
    "\"It's easy to sit up and take notice, what's difficult is getting up and taking action.\"";
  import css from "./assets/style.css";
  import dividerMobile from "./assets/divider-mobile.svg";
  import dividerDesktop from "./assets/divider-desktop.svg";
  import diceIcon from "./assets/icon-dice.svg";
  let responses = [];
  onMount(async () => {
    const response = await fetch("https://api.adviceslip.com/advice");
    const data = await response.json();
    responses[0] = data.slip.advice;
    responses[1] = data.slip.id;
  });
</script>

<main>
  <div class="holder">
    <h3>ADVICE #{responses[1]}</h3>
    <h2>{responses[0]}</h2>
    <img src={dividerDesktop} alt="divider" class="divider-desktop" />
    <button
      class="button-reload"
      on:click={() => {
        window.location.reload();
      }}
    >
      <img src={diceIcon} alt="dice" class="dice-icon" />
    </button>
  </div>
</main>
