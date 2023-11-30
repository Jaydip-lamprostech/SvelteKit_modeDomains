<script>
  import { onMount } from "svelte";
  import { modalStore } from "$lib/stores/modalStore";
  import { getAccount, fetchBalance } from "@wagmi/core";

  /**
   * @type {{
     connect(): unknown; open: () => void; 
}}
   */
  let modal;
  /**
   * @type {any}
   */
  let walletStatus = "connect";

  onMount(() => {
    // Access the modal instance from the store
    modal = $modalStore;
  });
  const account = getAccount();
  if (account.isConnected) {
    console.log(account.isConnected);
    walletStatus = "connected";
  } else if (account.isConnecting) {
    console.log(account.isConnecting);
    walletStatus = "connecting...";
  } else if (account.isDisconnected) {
    console.log(account.isDisconnected);
    walletStatus = "Connect";
  }
  function clicked() {
    const account = getAccount();
    console.log("clicked");
    console.log(account);
    // @ts-ignore
    modal.open();
  }

  async function balance() {
    const account = getAccount();
    const balance = await fetchBalance({
      // @ts-ignore
      address: account ? account.address : "",
    });
    console.log(balance);
  }
</script>

<svelte:head>
  <title>About</title>
  <meta name="description" content="About this app" />
</svelte:head>
<div class="text-column">
  <h1>About this app</h1>
  <!-- <w3m-button />
  <w3m-network-button /> -->
  <button on:click={clicked}>{walletStatus}</button>

  <button on:click={clicked}>Clicked</button>
  <button on:click={balance}>balance</button>
  <p>
    This is a <a href="https://kit.svelte.dev">SvelteKit</a> app. You can make your
    own by typing the following into your command line and following the prompts:
  </p>

  <pre>npm create svelte@latest</pre>

  <p>
    The page you're looking at is purely static HTML, with no client-side
    interactivity needed. Because of that, we don't need to load any JavaScript.
    Try viewing the page's source, or opening the devtools network panel and
    reloading.
  </p>

  <p>
    The <a href="/sverdle">Sverdle</a> page illustrates SvelteKit's data loading
    and form handling. Try using it with JavaScript disabled!
  </p>
</div>
