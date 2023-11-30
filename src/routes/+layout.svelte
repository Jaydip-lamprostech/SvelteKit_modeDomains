<script>
  import Header from "./Header.svelte";
  import "./styles.css";
  import { createWeb3Modal, defaultWagmiConfig } from "@web3modal/wagmi";
  import { modeTestnet } from "viem/chains";
  import { modalStore } from "$lib/stores/modalStore";

  const projectId = "5bc831dcf02437ce75e6b2cce2099ae0";
  const metadata = {
    name: "Web3Modal",
    description: "Web3Modal Example",
    url: "https://web3modal.com",
    icons: ["https://avatars.githubusercontent.com/u/37784886"],
  };
  const chains = [modeTestnet];
  const wagmiConfig = defaultWagmiConfig({ chains, projectId, metadata });
  const modal = createWeb3Modal({ wagmiConfig, projectId, chains });
  modal.setThemeMode("dark");
  modalStore.set(modal);
</script>

<div class="app">
  <Header />

  <main>
    <slot />
  </main>

  <footer>
    <p>
      visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to learn SvelteKit
    </p>
  </footer>
</div>

<style>
  .app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  main {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    width: 100%;
    max-width: 64rem;
    margin: 0 auto;
    box-sizing: border-box;
  }

  footer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 12px;
  }

  footer a {
    font-weight: bold;
  }

  @media (min-width: 480px) {
    footer {
      padding: 12px 0;
    }
  }
</style>
