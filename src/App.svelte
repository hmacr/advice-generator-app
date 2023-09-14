<script lang="ts">
  import { onMount } from 'svelte';
  import IconDice from './assets/icon-dice.svg';
  import Loading from './lib/Loading.svelte';
  import Advice from './lib/Advice.svelte';

  class AdviceData {
    id!: number;
    advice!: string;
  }

  let adviceNum: number;
  let adviceContent: string;

  let isLoading: boolean;

  onMount(() => handleAdviceLoad());

  function handleAdviceLoad() {
    isLoading = true;
    setTimeout(getAdvice, 1000);
  }

  function getAdvice() {
    fetch('https://api.adviceslip.com/advice')
      .then(res => res.json())
      .then(data => {
        adviceNum = data.slip.id;
        adviceContent = data.slip.advice;
        isLoading = false;
      })
      .catch(err => console.log(err));
  }

  function handleButtonClick(e: Event) {
    handleAdviceLoad();
  }
</script>

<!-- Container -->
<div
  class="w-[500px] h-screen mx-auto flex flex-col justify-center items-center"
>
  <!-- Card -->
  <div
    class="w-full min-h-[300px] flex flex-col justify-center items-center gap-6 mx-auto py-12 px-12 text-light-cyan bg-dark-grayish-blue rounded-xl font-manrope"
  >
    {#if isLoading}
      <Loading />
    {:else}
      <Advice
        {adviceNum}
        {adviceContent}
      />
    {/if}
  </div>
  <!-- Dice -->
  <div class="relative -top-7 w-14 h-14">
    <button
      on:click={handleButtonClick}
      class="w-full h-full flex justify-center items-center bg-neon-green rounded-full
        hover:cursor-pointer hover:scale-110 hover:shadow-[0_0_30px] hover:shadow-neon-green transition-shadow"
    >
      <img
        src={IconDice}
        alt="icon-dice"
      />
    </button>
  </div>
</div>
