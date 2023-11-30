<script>
  // @ts-nocheck

  /**
   * @param {{ key: string; }} event
   */
  function handleSocialIconClick(event, text) {
    console.log(text, text === "twitter");
    // Check if the key pressed is the Enter key (key code 13)

    if (event && event.key === "Enter") {
      if (text === "twitter") {
        window.open("https://twitter.com/Mode_Domains");
      } else if (text === "discord") {
        window.open("https://discord.gg/XdmEgUDGGf");
      }
    }
    if (!event && text === "twitter") {
      window.open("https://twitter.com/Mode_Domains");
    } else if (!event && text === "discord") {
      window.open("https://discord.gg/XdmEgUDGGf");
    }
  }
</script>

<footer>
  <div class="footer-main">
    <footer class="footer">
      <span>
        <a
          target="_blank"
          href="https://bridge.mode.network/"
          rel="noopener noreferrer"
        >
          Bridge
        </a>
        <a
          target="_blank"
          href="https://faucet.modedomains.xyz/"
          rel="noopener noreferrer"
        >
          Faucet
        </a>
        <a
          target="_blank"
          href="https://www.mode.network/"
          rel="noopener noreferrer"
        >
          MODE
        </a>
        <a
          target="_blank"
          href="https://sepolia.explorer.mode.network/"
          rel="noopener noreferrer"
        >
          Explorer
        </a>
      </span>
      <div class="social-media">
        <svg
          viewBox="0,0,256,256"
          width="50px"
          height="50px"
          on:click={() => handleSocialIconClick(false, "twitter")}
          on:keydown={(e) => handleSocialIconClick(e, "twitter")}
          role="button"
          tabindex="0"
        >
          <g
            fill="#ffffff"
            fillRule="nonzero"
            stroke="none"
            strokeWidth="1"
            strokeLinecap="butt"
            strokeLinejoin="miter"
            strokeMiterlimit="10"
            strokeDasharray=""
            strokeDashoffset="0"
            fontFamily="none"
            fontWeight="none"
            fontSize="none"
            textAnchor="none"
          >
            <g transform="scale(5.12,5.12)">
              <path
                d="M5.91992,6l14.66211,21.375l-14.35156,16.625h3.17969l12.57617,-14.57812l10,14.57813h12.01367l-15.31836,-22.33008l13.51758,-15.66992h-3.16992l-11.75391,13.61719l-9.3418,-13.61719zM9.7168,8h7.16406l23.32227,34h-7.16406z"
              ></path>
            </g>
          </g>
        </svg>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 127.14 96.36"
          role="button"
          tabindex="0"
          on:click={() => handleSocialIconClick(false, "discord")}
          on:keydown={(e) => handleSocialIconClick(e, "discord")}
        >
          <path
            fill="#fff"
            d="M107.7,8.07A105.15,105.15,0,0,0,81.47,0a72.06,72.06,0,0,0-3.36,6.83A97.68,97.68,0,0,0,49,6.83,72.37,72.37,0,0,0,45.64,0,105.89,105.89,0,0,0,19.39,8.09C2.79,32.65-1.71,56.6.54,80.21h0A105.73,105.73,0,0,0,32.71,96.36,77.7,77.7,0,0,0,39.6,85.25a68.42,68.42,0,0,1-10.85-5.18c.91-.66,1.8-1.34,2.66-2a75.57,75.57,0,0,0,64.32,0c.87.71,1.76,1.39,2.66,2a68.68,68.68,0,0,1-10.87,5.19,77,77,0,0,0,6.89,11.1A105.25,105.25,0,0,0,126.6,80.22h0C129.24,52.84,122.09,29.11,107.7,8.07ZM42.45,65.69C36.18,65.69,31,60,31,53s5-12.74,11.43-12.74S54,46,53.89,53,48.84,65.69,42.45,65.69Zm42.24,0C78.41,65.69,73.25,60,73.25,53s5-12.74,11.44-12.74S96.23,46,96.12,53,91.08,65.69,84.69,65.69Z"
          />
        </svg>
      </div>
    </footer>
  </div>
</footer>

<style>
  .footer-main {
    margin: 10px 0px;
    border-top: 2px solid rgba(255, 255, 255, 0.18);
    padding: 10px 0px;
    text-align: center;
    margin-top: auto;
  }

  .footer {
    /* width: 80%; */
    display: flex;
    width: 95%;
    margin: auto;
    justify-content: space-between;
    align-items: center;
  }

  span a {
    font-family: "IBM Plex Sans", sans-serif;
    font-weight: 500;
    font-size: 1.1rem;
    color: #ffffff;
    margin-right: 20px;
    text-decoration: none;
  }
  span a:hover {
    color: #dffe00;
  }

  .social-media {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
  }
  .social-media > svg {
    cursor: pointer;
    width: 30px;
    height: 30px;
    padding: 6px;
    border-radius: 8px;
    background-color: rgba(10, 10, 10, 0.8);
    border: 2px solid rgba(255, 255, 255, 0.18);
  }
  .social-media > svg:hover {
    border-color: #dffe00;
  }

  @media (max-width: 768px) {
    .footer {
      flex-direction: column;
      gap: 20px;
    }
  }
</style>
