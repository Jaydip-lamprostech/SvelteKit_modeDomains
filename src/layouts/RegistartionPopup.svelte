<script>
  export function closePopup() {}
  export let domainName = "";
  export let domainNamePrice = "";
  export let errorMessage = "";
  export let transactionState = { waiting: false, msg: "" };
  export function registerName() {}
  export function openConnectModal() {}
  let address = "";
  export let popupContainer;
</script>

<div class="registration_popup" bind:this={popupContainer}>
  <div class="registration_popup_inside">
    <div class="registration_form">
      <div class="registration_popup_close_icon">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          height="24px"
          viewBox="0 0 24 24"
          width="24px"
          fill="#000000"
          on:click={closePopup}
          on:keydown={closePopup}
          role="button"
          tabindex="0"
        >
          <path d="M0 0h24v24H0V0z" fill="none" />
          <path
            d="M18.3 5.71c-.39-.39-1.02-.39-1.41 0L12 10.59 7.11 5.7c-.39-.39-1.02-.39-1.41 0-.39.39-.39 1.02 0 1.41L10.59 12 5.7 16.89c-.39.39-.39 1.02 0 1.41.39.39 1.02.39 1.41 0L12 13.41l4.89 4.89c.39.39 1.02.39 1.41 0 .39-.39.39-1.02 0-1.41L13.41 12l4.89-4.89c.38-.38.38-1.02 0-1.4z"
          />
        </svg>
      </div>
      <div class="registration_form_inside">
        <h1>
          Register
          <span class="mode_name">{domainName}.mode</span>
        </h1>
        <div class="registartion_fields">
          <div class="registration_field_item">
            <div class="registration_field_title">
              <span class="field_title">Registration Period</span>
              <span
                class="field_info"
                data-tooltip-id="registration-period"
                data-tooltip-content="The number of years you will have right over this domain"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  enable-background="new 0 0 24 24"
                  height="24px"
                  viewBox="0 0 24 24"
                  width="24px"
                  fill="#000000"
                >
                  <g>
                    <path d="M0,0h24v24H0V0z" fill="none" />
                  </g>
                  <g>
                    <g>
                      <g>
                        <path
                          d="M12,22c1.1,0,2-0.9,2-2h-4C10,21.1,10.9,22,12,22z"
                        />
                      </g>
                      <g>
                        <path
                          d="M9,19h6c0.55,0,1-0.45,1-1v0c0-0.55-0.45-1-1-1H9c-0.55,0-1,0.45-1,1v0C8,18.55,8.45,19,9,19z"
                        />
                      </g>
                      <g>
                        <path
                          d="M12,2C7.86,2,4.5,5.36,4.5,9.5c0,3.82,2.66,5.86,3.77,6.5h7.46c1.11-0.64,3.77-2.68,3.77-6.5C19.5,5.36,16.14,2,12,2z"
                        />
                      </g>
                    </g>
                  </g>
                </svg>
              </span>
            </div>
            <div class="registartion_field_input registration_period">
              <span class="registration_period_time">
                <span>1</span> Year
              </span>
              <div
                class="registration_period_modification"
                data-tooltip-id="increase-decrease-period"
                data-tooltip-content="On testnet period is fixed for 1 year right now."
              >
                <span class="period_decrease opacity_low">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    height="24px"
                    viewBox="0 0 24 24"
                    width="24px"
                    fill="#000000"
                  >
                    <path d="M0 0h24v24H0V0z" fill="none" />
                    <path
                      d="M18 13H6c-.55 0-1-.45-1-1s.45-1 1-1h12c.55 0 1 .45 1 1s-.45 1-1 1z"
                    />
                  </svg>
                </span>
                <span class="period_increase opacity_low">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    height="24px"
                    viewBox="0 0 24 24"
                    width="24px"
                    fill="#000000"
                  >
                    <path d="M0 0h24v24H0V0z" fill="none" />
                    <path
                      d="M18 13h-5v5c0 .55-.45 1-1 1s-1-.45-1-1v-5H6c-.55 0-1-.45-1-1s.45-1 1-1h5V6c0-.55.45-1 1-1s1 .45 1 1v5h5c.55 0 1 .45 1 1s-.45 1-1 1z"
                    />
                  </svg>
                </span>
              </div>
            </div>
          </div>
          <div class="registration_field_item">
            <div class="registration_field_title">
              <span class="field_title">
                Domain Cost{" "}
                <span class="field-sub-title"> (Excluding Gas Fees) </span>
              </span>
              <span
                class="field_info"
                data-tooltip-id="domain-cost"
                data-tooltip-content="The cost is for the period selected."
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  enable-background="new 0 0 24 24"
                  height="24px"
                  viewBox="0 0 24 24"
                  width="24px"
                  fill="#000000"
                >
                  <g>
                    <path d="M0,0h24v24H0V0z" fill="none" />
                  </g>
                  <g>
                    <g>
                      <g>
                        <path
                          d="M12,22c1.1,0,2-0.9,2-2h-4C10,21.1,10.9,22,12,22z"
                        />
                      </g>
                      <g>
                        <path
                          d="M9,19h6c0.55,0,1-0.45,1-1v0c0-0.55-0.45-1-1-1H9c-0.55,0-1,0.45-1,1v0C8,18.55,8.45,19,9,19z"
                        />
                      </g>
                      <g>
                        <path
                          d="M12,2C7.86,2,4.5,5.36,4.5,9.5c0,3.82,2.66,5.86,3.77,6.5h7.46c1.11-0.64,3.77-2.68,3.77-6.5C19.5,5.36,16.14,2,12,2z"
                        />
                      </g>
                    </g>
                  </g>
                </svg>
              </span>
            </div>
            <div class="registartion_field_input">
              <span class="registration_domain_cost">
                {domainNamePrice} ETH
              </span>
            </div>
          </div>
          <div class="registration_field_item">
            <div class="registration_field_title">
              <span class="field_title">Payment Mode</span>
              <span
                class="field_info"
                data-tooltip-id="payment-mode"
                data-tooltip-content="The chain on which domain will be purchased"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  enable-background="new 0 0 24 24"
                  height="24px"
                  viewBox="0 0 24 24"
                  width="24px"
                  fill="#000000"
                >
                  <g>
                    <path d="M0,0h24v24H0V0z" fill="none" />
                  </g>
                  <g>
                    <g>
                      <g>
                        <path
                          d="M12,22c1.1,0,2-0.9,2-2h-4C10,21.1,10.9,22,12,22z"
                        />
                      </g>
                      <g>
                        <path
                          d="M9,19h6c0.55,0,1-0.45,1-1v0c0-0.55-0.45-1-1-1H9c-0.55,0-1,0.45-1,1v0C8,18.55,8.45,19,9,19z"
                        />
                      </g>
                      <g>
                        <path
                          d="M12,2C7.86,2,4.5,5.36,4.5,9.5c0,3.82,2.66,5.86,3.77,6.5h7.46c1.11-0.64,3.77-2.68,3.77-6.5C19.5,5.36,16.14,2,12,2z"
                        />
                      </g>
                    </g>
                  </g>
                </svg>
              </span>
            </div>
            <div class="registartion_field_input payment-mode">
              <div>
                <label>
                  <input
                    type="radio"
                    name="option"
                    value="option1"
                    readOnly
                    class="custom-radio"
                    checked
                  />
                  Mode Testnet
                </label>
              </div>
              <div>
                <p class="registration_field_information">
                  We aim to contribute 75% of the fees collected to Optimism
                  Collective & Mode. The rest 25% will be used in
                  development,maintenance & integration of the project.
                </p>
              </div>
              <div>
                <a
                  class="claim-mode-testnet"
                  href="https://faucet.modedomains.xyz/"
                  target="_blanck"
                >
                  Mode Testnet Faucet
                </a>
              </div>
            </div>
          </div>
          <div class="registration_field_item transaction-err">
            {#if errorMessage}
              <div class="registartion_field_input">
                <p>Error</p>
                <div class="error-msg">
                  {errorMessage}
                </div>
              </div>
            {/if}
          </div>
          <div class="registration_field_item">
            <span class="only-one-claim-info">
              For testnet, only one handle can be claimed by the user, choose
              wisely.
            </span>
          </div>
          <div class="registration_field_item">
            {#if transactionState.waiting}
              <div class="register loader">
                {transactionState.msg}
                <div class="sp sp-wave"></div>
              </div>
            {:else}
              <button
                class="register"
                on:click={() => {
                  if (address) registerName();
                  else openConnectModal();
                }}
              >
                Register
              </button>
            {/if}
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .registration_popup {
    position: fixed;
    /* top: 0; */
    bottom: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(10, 10, 10, 0.8);
    transition:
      opacity 0.3s,
      visibility 0.3s;
    opacity: 0;
    visibility: hidden;
    overflow: hidden;
    z-index: 60;
  }
  .animate {
    opacity: 1;
    visibility: visible;
    overflow: auto;
  }
  .registration_form {
    width: 80%;
    max-width: 700px;
    min-height: 100vh;
    margin: auto;
    margin-top: 120px;
    padding: 30px;
    border: 1px solid rgb(45, 45, 45);
    background-color: rgb(21, 22, 25);
    border-radius: 20px;
    position: relative;
    transform-origin: bottom center;
    transition:
      transform 0.5s,
      opacity 0.5s;
    transform: translate(0%, 100%) scale(0.8);
    opacity: 0;
  }
  .registration_popup.animate .registration_form {
    transform: scale(1);
    opacity: 1;
  }
  .registration_popup_close_icon {
    position: sticky;
    top: 20px;
    right: 20px;
    max-width: max-content;
  }
  .registration_popup_close_icon svg {
    width: 25px;
    height: 25px;
    background-color: transparent;
    fill: #dffe00;
    border-radius: 100px;
    padding: 5px;
  }

  .registration_popup_close_icon svg:hover {
    background-color: #000;
  }

  .registration_form_inside {
    padding-left: 40px;
    padding-right: 40px;
  }

  .registration_form_inside h1 > span {
    color: #000;
    font-family: "Chakra Petch", sans-serif;
    line-height: 100%;
    word-break: break-all;
    padding: 10px 20px;
    margin-left: 20px;
    border-radius: 10px;
    color: #dffe00;
    /* background-color: #dffe00; */
    border: 1px solid #dffe00;
  }

  .registration_form_inside > h1 {
    font-family: "IBM Plex Sans", sans-serif;
    margin-top: 20px;
  }

  .registartion_fields {
    display: flex;
    flex-direction: column;
    width: 100%;
    margin-top: 60px;
  }

  .registration_field_item {
    margin-bottom: 30px;
  }

  .registration_field_title {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: rgb(255, 255, 255, 0.5);
  }

  .registration_field_title .field_title {
    padding: 0px;
    position: relative;
    font-size: 1.5rem;
    font-weight: 600;
    line-height: 150%;
    letter-spacing: 0.15px;
    font-family: "IBM Plex Sans", sans-serif;
    color: inherit;
    display: inline-block;
    margin-left: 10px;
    margin-bottom: 10px;
  }
  .field-sub-title {
    font-size: 14px;
    font-weight: 400;
  }
  .registartion_field_input {
    border: 1px solid rgb(45, 45, 45);
    padding: 20px 30px;
    border-radius: 10px;
    font-size: x-large;
    font-weight: 600;
    line-height: 150%;
    letter-spacing: 0.15px;
    font-family: "IBM Plex Sans", sans-serif;
  }
  .transaction-err .registartion_field_input {
    font-size: 1rem;
    background-color: rgb(242, 104, 91, 0.08);
    color: rgb(242, 104, 91);
    border: 1px solid rgb(242, 104, 91);
  }
  .field_info > svg {
    width: 18px;
    height: 18px;
    background-color: transparent;
    fill: rgb(255, 255, 255, 0.5);
    border-radius: 100px;
    padding: 5px;
  }
  .field_info > svg:hover {
    /* background-color: #000; */
    fill: #dffe00;
  }

  .registration_period {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .registration_period_time {
    text-transform: uppercase;
  }
  .registration_period_modification {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .registration_period_modification > span {
    background-color: rgb(255, 255, 255, 0.05);
    border-radius: 5px;
    display: flex;
    align-items: center;
    /* padding: 6px; */
  }
  .registration_period_modification > span:hover {
    background-color: rgb(255, 255, 255, 0.1);
  }
  .registration_period_modification > span > svg {
    fill: #dffe00;
    padding: 6px;
  }
  .register {
    cursor: pointer;
    font-size: x-large;
    width: 100%;
    text-align: center;
    padding: 10px 0;
    border-radius: 10px;
    border: none;
    background-color: #dffe00;
    color: #000;
    font-family: "Chakra Petch", sans-serif;
  }
  .register:hover {
    background-color: #ceea00;
  }
  .register.loader {
    pointer-events: none;
    opacity: 0.89;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 5px;
    height: 40px;
    width: 100%;
  }
  .register.loader > div {
    margin-left: 10px;
  }
  .registration_popup::-webkit-scrollbar {
    width: 5px !important;
  }

  .registration_popup::-webkit-scrollbar-track {
    box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3) !important;
  }

  .registration_popup::-webkit-scrollbar-thumb {
    background-color: #dffe00 !important;
    outline: none !important;
    border-radius: 10px !important;
  }

  .opacity_low {
    opacity: 0.3;
    pointer-events: none;
  }

  /* Style for the custom radio input */
  .custom-radio {
    appearance: none;
    -webkit-appearance: none;
    -moz-appearance: none;
    width: 15px; /* Adjust the size of the radio button */
    height: 15px; /* Adjust the size of the radio button */
    border: none; /* Border color */
    border-radius: 50%; /* Make it circular */
    outline: 2px solid rgba(255, 255, 255, 0.18);
    cursor: pointer;
    outline-offset: 2px;
    margin-right: 15px;
    background-color: white; /* Unselected background color */
  }

  /* Style for the custom radio input when selected */
  .custom-radio:checked {
    background-color: #dffe00; /* Selected background color */
  }

  .registration_field_information {
    font-size: 1rem;
    font-weight: 400;
    line-height: 150%;
    letter-spacing: 0.15px;
    font-family: "IBM Plex Sans", sans-serif;
  }
  .claim-mode-testnet {
    font-size: 0.86rem;
    font-weight: normal;
    cursor: pointer;
    background-color: transparent;
    border: 1px solid #dffe00;
    color: #dffe00;
    border-radius: 5px;
    padding: 8px 15px;
    text-decoration: none;
  }
  .claim-mode-testnet:hover {
    background-color: #dffe00;
    border: 1px solid #dffe00;
    color: #000;
  }
  .only-one-claim-info {
    font-size: 1rem;
    font-weight: 400;
    letter-spacing: 0.15px;
    font-family: "IBM Plex Sans", sans-serif;
    color: rgb(255, 255, 255, 0.5);
    margin-left: 10px;
    margin-bottom: 10px;
  }
  #custom-tooltip {
    font-size: 1rem;
    font-weight: 400;
    letter-spacing: 0.15px;
    font-family: "IBM Plex Sans", sans-serif;
  }
  .error-msg {
    display: -webkit-box;
    max-width: 100%;
    -webkit-line-clamp: 4;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  @media (max-width: 768px) {
    .registration_popup_close_icon {
      display: flex;
      justify-content: flex-end;
      align-items: center;
      max-width: 100%;
      margin-top: 10px;
    }
    .registration_form {
      width: 90%;
      min-height: 90vh;
      padding: 10px;
      padding-bottom: 50px;
    }
    .registration_form_inside {
      padding-left: 10px;
      padding-right: 20px;
    }
    .registration_form_inside h1 > span {
      padding: 8px 10px;
      margin-left: 10px;
    }
    .registration_form_inside > h1 {
      font-size: large;
      margin-left: 5px;
    }
    .registartion_fields {
      margin-top: 50px;
    }
    .registration_field_title .field_title {
      padding: 0px;
      position: relative;
      font-size: 1.1rem;
      font-weight: 600;
      line-height: 150%;
      letter-spacing: 0.15px;
      font-family: "IBM Plex Sans", sans-serif;
      color: inherit;
      display: inline-block;
      margin-left: 5px;
      margin-bottom: 5px;
    }
    .registartion_field_input {
      padding: 10px 15px;
      border-radius: 10px;
      font-size: large;
    }
    .registration_field_information {
      font-size: 0.865rem;
      font-weight: 400;
      line-height: 120%;
    }
    .payment-mode {
      padding-bottom: 20px;
    }
    .claim-mode-testnet {
      padding: 8px 10px;
      font-size: small;
    }
    .register {
      font-size: medium;
    }
    .field_info > svg {
      width: 12px;
      height: 12px;
    }
  }
</style>
