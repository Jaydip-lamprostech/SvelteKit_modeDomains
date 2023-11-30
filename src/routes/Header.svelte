<script>
  import { page } from "$app/stores";
  import closeIcon from "$lib/images/closeIcon.svg";
  import menuIcon from "$lib/images/menuIcon.svg";
  import logo from "$lib/images/mode_logo.png";

  let showMenu = false;

  const toggleMenu = () => {
    showMenu = !showMenu;
  };

  /**
   * @param {{ key: string; }} event
   */
  function handleKeyPress(event) {
    // Check if the key pressed is the Enter key (key code 13)
    if (event.key === "Enter") {
      toggleMenu();
    }
  }
</script>

<header>
  <div class="navbar-parent">
    <div class="navbar">
      <a href="/">
        <div class="logo">
          <img src={logo} alt="modedomains logo" />
          DOMAINS
        </div>
      </a>
      <div
        class="mobile-menu-icon close"
        on:click={toggleMenu}
        on:keydown={handleKeyPress}
        tabindex="0"
        role="button"
      >
        {#if showMenu}
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="24"
            width="18"
            viewBox="0 0 384 512"
            ><path
              fill="#ffffff"
              d="M342.6 150.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L192 210.7 86.6 105.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L146.7 256 41.4 361.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0L192 301.3 297.4 406.6c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L237.3 256 342.6 150.6z"
            /></svg
          >
        {:else}
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="16"
            width="14"
            viewBox="0 0 448 512"
            fill="#ffffff"
            ><path
              d="M0 96C0 78.3 14.3 64 32 64H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32C14.3 128 0 113.7 0 96zM0 256c0-17.7 14.3-32 32-32H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32c-17.7 0-32-14.3-32-32zM448 416c0 17.7-14.3 32-32 32H32c-17.7 0-32-14.3-32-32s14.3-32 32-32H416c17.7 0 32 14.3 32 32z"
            /></svg
          >
        {/if}
      </div>
      <div class="nav-links">
        <a class="nav-link" href="https://docs.modedomains.xyz/"> Docs </a>
        <a class="nav-link" href="/"> Profile </a>
      </div>
      <div class="cta-button"><w3m-button /></div>
    </div>

    <div class={showMenu ? "mobile-menu show" : "mobile-menu"}>
      <div class="mobile_menu_link_parent">
        <a class="nav-link" href="https://docs.modedomains.xyz/">
          <span class="nav-text-animate">Docs</span>
        </a>
        <a class="nav-link" href="/">
          <span class="nav-text-animate">Profile</span>
        </a>
      </div>
    </div>
  </div>
</header>

<style>
  a {
    text-decoration: none;
  }
  /* Navbar.css */
  .navbar-parent {
    width: 100%;
    margin: auto;
    -webkit-backdrop-filter: blur(12px);
    backdrop-filter: blur(12px);
    background-color: rgba(0, 0, 0, 0.5);
    border-bottom: 1px solid white;
    position: sticky;
    top: 0;
    z-index: 50;
  }
  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
    width: 90%;
    height: 58px;
    margin: auto;
  }
  .logo {
    display: flex;
    align-items: center;
    flex-wrap: nowrap;
    gap: 1px;
    font-size: 20px;
    color: #fff;
    font-weight: 500;
    font-family: "Chakra Petch", sans-serif;
  }

  .nav-links {
    display: flex;
    gap: 20px;
    font-family: "IBM Plex Sans", sans-serif;
  }

  .nav-link {
    color: #fff;
    text-decoration: none;
    transition: color 0.3s;
  }

  .nav-link:hover {
    color: #dffe00;
  }

  .cta-button {
    order: 1;
    color: #000;
    padding: 8px;
    padding-right: 0;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .close {
    display: none;
  }

  .mobile-menu.show {
    display: flex;
    opacity: 1;
    transform: translateY(0);
    background: rgba(0, 0, 0, 0.4);
    -webkit-backdrop-filter: blur(12px);
    backdrop-filter: blur(12px);
    height: calc(100vh - 58px);
  }

  .mobile-menu a {
    padding: 15px;
    text-align: center;
    text-decoration: none;
    color: white;
  }
  .mobile-menu {
    display: none;
  }
  @media (max-width: 768px) {
    .navbar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 10px 20px;
      background-color: black;
      color: white;
      position: relative;
      z-index: 50;
    }
    .logo {
      order: 1;
      font-size: 1rem;
    }

    .mobile-menu-icon {
      order: 2;
      display: block;
    }

    .nav-links {
      display: none;
    }

    .nav-link {
      margin: 10px 0;
      padding: 10px;
      text-align: center;
    }

    .mobile-menu-icon.close {
      font-size: 24px;
      cursor: pointer;
      display: block;
    }
    .mobile-menu {
      display: flex;
      flex-direction: column;
      background-color: rgba(10, 10, 10, 1);
      position: absolute;
      top: 80px;
      width: 100%;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      z-index: 2;
      opacity: 0;
      transform: translateY(-20px);
      transition:
        opacity 0.5s cubic-bezier(0.23, 1, 0.32, 1) 0.5s,
        transform 1s cubic-bezier(0.23, 1, 0.32, 1) 0.5s,
        background-color 1s cubic-bezier(0.23, 1, 0.32, 1) 0.5s;
    }
    .mobile-menu.show {
      opacity: 1;
    }
    .mobile-menu a {
      z-index: -1;
      padding: 20px 15px;
      text-align: center;
      text-decoration: none;
      color: white;
      background-color: #000;
      margin: 0;
      font-size: larger;
      pointer-events: none;
      margin-left: 0;
      display: block;
      float: none;
      /* width: 100%; */
      height: 44px;
    }
    .mobile-menu a:first-of-type {
      border-bottom: 2px solid rgba(255, 255, 255, 0.18);
    }
    .nav-text-animate {
      display: flex;
      align-items: center;
      height: 100%;
      line-height: 1.3;
      opacity: 0;
      transform: translate3d(0, -25px, 0);
      transition: 0.5s ease;
      transition-property: transform, opacity;
    }
    .mobile-menu.show .nav-text-animate {
      transition-delay: 0.7s;
      transform: translateY(0);
      opacity: 1;
    }
    .mobile-menu.show a {
      z-index: 9999;
      pointer-events: all;
    }
    .mobile_menu_link_parent {
      width: 100%;
      height: 0;
      transition: height 0.1s cubic-bezier(0.23, 1, 0.32, 1);
      border-bottom: 2px solid rgba(255, 255, 255, 0.18);
    }
    .mobile-menu.show .mobile_menu_link_parent {
      height: max-content;
    }
    .cta-button {
      margin-left: auto;
      margin-right: 10px;
    }
  }
</style>
