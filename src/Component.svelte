<script>
  import { clickOutside } from "./ClickOutside.js";
  import { getContext } from "svelte";

  export let variant;
  export let size;
  export let direction;
  export let position;

  let active = false;

  const { styleable } = getContext("sdk");
  const component = getContext("component");

</script>

<div use:styleable={$component.styles}>
  <div use:clickOutside on:click_outside={() => (active = false)}>
    <button
      on:click={() => active = !active}
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

    {#if active}
      <div class={position === 'right' ? 'position-right dropdown-memnu-container' : 'dropdown-memnu-container'} style:flex-direction={direction}>
        <slot />
      </div>
    {/if}

  </div>
</div>

<style>
  .position-right {
    top: 4px;
    left: 92px;
  }
  
  .dropdown-memnu-container {
    display: flex;
    gap: 4px;
    z-index: 999;
    position: absolute;
    background-color: white;
    padding: 10px;
    margin-bottom: 5px;
    border-radius: 4px;
    border-style: solid;
    border-color: rgb(177, 177, 177);
    border-width: 1px;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
  }
</style>
