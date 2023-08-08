<script lang="ts">
  import CountdownTimer from './lib/CountdownTimer.svelte';
  const live = new Date('August 10, 2023 18:30:00');
</script>

<main>
  <img
    class="slate"
    src="https://www.conchovalleyhomepage.com/wp-content/uploads/sites/83/2023/08/HSFBPS_Logo.png"
    alt="High School Football Preview Show"
  />
  <CountdownTimer expires={live} />
  <img
    class="logo"
    src="https://www.conchovalleyhomepage.com/wp-content/uploads/sites/83/2023/08/TwistedRootBurger_Logo_white.png"
    alt="Twisted Root Burger Company"
  />
</main>

<style>
  main {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
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
