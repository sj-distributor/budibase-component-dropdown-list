<script>
  import { clickOutside } from "./ClickOutside.js";
  import { getContext } from "svelte";

  export let variant;
  export let size;
  export let direction;

  let active = false;

  const { styleable } = getContext("sdk");
  const component = getContext("component");
</script>

<div use:styleable={$component.styles}>
  <div use:clickOutside on:click_outside={() => (active = false)}>
    <button
      on:click={() => (active = !active)}
      type="button"
      class="spectrum-Button 
      spectrum-Button--{variant ?? 'primary'} 
      spectrum-Button--size{size ?? 'M'}"
    >
      <svg
        class="spectrum-Icon spectrum-UIIcon-ChevronDown100 spectrum-Accordion-itemIndicator"
        focusable="false"
        aria-hidden="true"
      >
        <use xlink:href="#spectrum-css-icon-Chevron100" />
      </svg>
    </button>

    {#if active === true}
      <div class="dropdown-memnu-container" style:flex-direction={direction}>
        {#if !!$$slots['slot']}
          <div>
            <h2>Custom content:</h2>
            <slot name="slot" />
          </div>
        {:else}
          <span>Item not found.</span>
        {/if}
      </div>
    {/if}
  </div>
</div>

<style>
  .dropdown-memnu-container {
    display: flex;
    gap: 4px;
    z-index: 9999;
    position: absolute;
    background-color: white;
    padding: 10px;
    margin-top: 5px;
    border-radius: 4px;
    border-style: solid;
    border-color: rgb(177, 177, 177);
    border-width: 1px;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
  }
</style>
