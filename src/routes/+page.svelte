<script>
  // @ts-nocheck
  import Counter from "../layouts/Counter.svelte";
  import welcome from "$lib/images/svelte-welcome.webp";
  import welcome_fallback from "$lib/images/svelte-welcome.png";
  import { onMount } from "svelte";

  import Wrapper from "$lib/components/wrapper.svelte";
  import Scene from "$lib/components/scene.svelte";
  import RegistartionPopup from "../layouts/RegistartionPopup.svelte";

  let input = "";
  let isPremium = false;
  let isVip = false;

  // start of the registration popup script
  let popupContainer;
  let registrationForm = false;
  let domainNamePrice = "";
  let domainName = "";
  let transactionState = {
    waiting: false,
    msg: "",
  };
  let errorMessage = "";
  const openPopup = () => {
    registrationForm = true;
    document.body.classList.add("popup-open");
    popupContainer.classList.add("animate");
  };

  const closePopup = () => {
    transactionState = {
      waiting: false,
      msg: "",
    };

    errorMessage = "";
    registrationForm = false;
    document.body.classList.remove("popup-open");
    popupContainer.classList.add("animate");
  };
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

  <Wrapper bind:input bind:isPremium bind:isVip>
    <Scene bind:input bind:isPremium bind:isVip />
  </Wrapper>
  <!-- <button on:click={openPopup}>Open Popup</button> -->
  <RegistartionPopup
    {popupContainer}
    {closePopup}
    {domainName}
    {domainNamePrice}
    {errorMessage}
    {transactionState}
  />
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
