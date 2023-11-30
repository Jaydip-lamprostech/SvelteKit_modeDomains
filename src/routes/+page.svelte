<script>
  import Counter from "./Counter.svelte";
  import welcome from "$lib/images/svelte-welcome.webp";
  import welcome_fallback from "$lib/images/svelte-welcome.png";
  import { onMount } from "svelte";

  import Wrapper from "$lib/components/wrapper.svelte";
  import Scene from "$lib/components/scene.svelte";

  let input = "";
  let isPremium = false;
  let isVip = false;
</script>

<svelte:head>
  <title>Home</title>
  <meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
  <!-- <w3m-button /> -->
  <h1>
    <!-- <span class="welcome">
      <picture>
        <source srcset={welcome} type="image/webp" />
        <img src={welcome_fallback} alt="Welcome" />
      </picture>
    </span> -->
  </h1>

  <!-- <h2>
    try editing <strong>src/routes/+page.svelte</strong>
  </h2> -->

  <!-- <Counter /> -->

  <!-- <Wrapper bind:input bind:isPremium bind:isVip>
    <Scene bind:input bind:isPremium bind:isVip />
  </Wrapper> -->
</section>

<style>
  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    flex: 0.6;
  }

  h1 {
    width: 100%;
  }
</style>
