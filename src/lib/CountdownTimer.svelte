<script lang="ts">
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';
  export let expires: Date;

  type TimeObject = {
    days: number;
    hours: number;
    minutes: number;
    seconds: number;
  };

  const now = new Date();
  const currentTime = now.getTime();
  const liveTime = expires.getTime();
  let timeRemaining = liveTime - currentTime;
  const slateCutoff = 15 * 1000 * 60;
  console.log({ timeRemaining });

  $: currentTimeObject = { ...getTime() };
  $: d = currentTimeObject.days;
  $: h = currentTimeObject.hours;
  $: m = currentTimeObject.minutes;
  $: s = currentTimeObject.seconds;
  $: showMessage = false;

  function format(t: number): string {
    return t < 10 ? '0' + t.toString() : t.toString();
  }

  function getTime(): TimeObject {
    return {
      days: Math.floor(timeRemaining / 1000 / 60 / 60 / 24),
      hours: Math.floor(timeRemaining / 1000 / 60 / 60) % 24,
      minutes: Math.floor(timeRemaining / 1000 / 60) % 60,
      seconds: Math.floor(timeRemaining / 1000) % 60,
    };
  }

  function update() {
    currentTimeObject = { ...getTime() };
  }

  function complete() {
    showMessage = true;
  }

  function start() {
    update();

    const intervalId = setInterval(() => {
      timeRemaining -= 1000;
      if (timeRemaining < 0) {
        complete();
        clearInterval(intervalId);
      } else {
        update();
      }
    }, 1000);
  }

  onMount(() => {
    start();
  });
</script>

{#if timeRemaining > slateCutoff}
  <img
    transition:fade={{ duration: 500 }}
    class="overlay-img"
    src="https://www.conchovalleyhomepage.com/wp-content/uploads/sites/83/2023/08/CMN_2023_FS.png"
    alt="2023 Childrens Miracle Network Telethon"
  />
{/if}

<div class="timer">
  {#if !showMessage}
    <div class="time">
      <!-- <span class="day">
          {expires.toLocaleDateString('en-US', { month: 'long', day: 'numeric', weekday: 'long' })}
          {expires.toLocaleTimeString('en-US', { hour: 'numeric', minute: 'numeric' })}
        </span> -->
      {#if h > 0}
        <span>
          {format(h)}:
        </span>
      {/if}
      <span>
        {format(m)}:
      </span>
      <span>
        {format(s)}
      </span>
    </div>
  {:else}
    <span class="message" in:fade={{ duration: 200 }}>Starting Soon!</span>
  {/if}
</div>

<style>
  .timer {
    font-family: 'Chivo Mono';
    align-self: stretch;
    font-size: 7rem;
    font-weight: 700;
    color: #000000;
    text-transform: uppercase;
    letter-spacing: 0.125em;
  }

  .time {
    display: flex;
    justify-content: center;
  }

  .message {
    font-family: 'Lato';
    font-weight: 900;
    /* font-family: 'Jost'; */
    letter-spacing: 0.05em;
  }

  span {
    display: block;
    text-align: center;
  }

  .overlay-img {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 1920px;
    height: 1080px;
    /* opacity: 0.1; */
  }
</style>
