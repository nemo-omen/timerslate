<script lang="ts">
  import CountdownTimer from './lib/CountdownTimer.svelte';
  const live = new Date('August 19, 2023 18:30:00');
  // const live = new Date('August 18, 2023 14:49:00');
</script>

<main>
  <!-- <img
    class="slate"
    src="https://www.conchovalleyhomepage.com/wp-content/uploads/sites/83/2023/08/CMN_2023_FS.png"
    alt="2023 Childrens Miracle Network Telethon"
  /> -->
  <CountdownTimer expires={live} />
</main>

<style>
  main {
    background-image: url('https://www.conchovalleyhomepage.com/wp-content/uploads/sites/83/2023/08/CMN_2023_FS.png');
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
    padding-bottom: 10rem;
    /* margin: 3rem 0 4rem 0; */
  }

  .slate {
    max-width: 46rem;
    margin-top: 3rem;
  }

  .logo {
    max-width: 11rem;
    margin-bottom: 8rem;
  }
</style>
